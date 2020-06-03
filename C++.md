

# 常见问题

## linux

### /usr/local/bin/cmake/cmake 不存在（远程调试）

```
sudo ln -s /usr/bin/cmake /usr/local/bin/cmake
```

### usr/bin/ld: cannot find -l

```
https://stackoverflow.com/questions/16710047/usr-bin-ld-cannot-find-lnameofthelibrary
```

example：

```cpp
/usr/bin/ld: cannot find -lzlib
ld -lzlib --verbose
```

### undefined reference to dlopen

```
https://stackoverflow.com/questions/16710047/usr-bin-ld-cannot-find-lnameofthelibrary
```

```
All you need to do is add ${CMAKE_DL_LIBS} to the target_link_libraries() call:
target_link_libraries(testlink ${CMAKE_DL_LIBS}
```

```
gcc dlopentest.c -ldl
```



# 计算函数调用时间

```cpp
#include <iostream>
#include <chrono>

void function()
{
    long long number = 0;

    for( long long i = 0; i != 2000000; ++i )
    {
       number += 5;
    }
}

int main()
{
    auto t1 = std::chrono::high_resolution_clock::now();
    function();
    auto t2 = std::chrono::high_resolution_clock::now();

    auto duration = std::chrono::duration_cast<std::chrono::microseconds>( t2 - t1 ).count();

    std::cout << duration;
    return 0;
}
```



# 获取环境变量的值

```c++
std::string java_home;
char *pathvar;
pathvar = getenv("JAVA_HOME");
java_home = pathvar;
std::cout << "java_home:" << java_home << std::endl;
```


# 获取当前目录

```
#ifdef _WIN32
#include <direct.h>
#define GetCurrentDir _getcwd
#else
#include <unistd.h>
#define GetCurrentDir getcwd
#endif


GetCurrentDir(buf, 100);
```

# goto

```
for(...) {
   for(...) {
      while(...) {
         if(...) goto stop;
         .
         .
         .
      }
   }
}
stop:
cout << "Error in program.\n";
```



# std::string的使用

## Split

```c++
#include <sstream>
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<string> strings;
    istringstream f("denmark;sweden;india;us");
    string s;    
    while (getline(f, s, ';')) {
        cout << s << endl;
        strings.push_back(s);
    }
}
```

# std::thread的使用

1 添加头文件#include <thread>

2 使用全局函数作为线程函数

```
#include <iostream>
#include <thread>
#include <string>
using namespace  std;

void ThreadFunc1()
{
    std::cout << "ThreadFunc1" << std::endl;
}

void ThreadFunc2(int data)
{
    std::cout << "ThreadFunc2"<<" "<<data << std::endl;
}

void ThreadFunc3(int data1,int data2,string str)
{
    std::cout << "ThreadFunc3" << " "<< data1 << " "<< data2 << " "<< str << std::endl;
}

int main()
{
    thread th1(ThreadFunc1);
    th1.join();
    int data1 = 10;
    thread th2(ThreadFunc2,data1);
    th2.join();
    int data2 = 100;
    string str = "StrTest";
    thread th3(ThreadFunc3, data1,data2,str);
    th3.join();
    return 0;
}
```

3 使用类成员函数作为线程函数

```
#include <iostream>
#include <thread>
#include <string>
using namespace  std;


class Foo
{
public:
    void ThreadFunc1() {
        std::cout << "ThreadFunc1" << std::endl;
    }

    void ThreadFunc2(int data1,int data2) {
        std::cout << "ThreadFunc2" << " " << data1 << " " << data2 << std::endl;
    }
};

int main()
{
    Foo foo;
    thread th1(&Foo::ThreadFunc1,foo);
    th1.join();
    int data1 = 10,data2 = 100;
     thread th2(&Foo::ThreadFunc2, foo,data1,data2);
     th2.join();
    return 0;
}
```

4 使用lambda表达式作为线程函数

```
int main()
{
    thread th([] {while (1)
    {
        std::cout << "lambda" << endl;
    }
    });
    while (1)
    {
        std::cout << "main" << endl;
    }
    th.join();
    return 0;
}
```

 

结果如下：

![img](https://img2018.cnblogs.com/blog/1317399/201908/1317399-20190830174251237-598140311.png)

 5 leetcode练习

题目描述：

```
public class Foo {
  public void one() { print("one"); }
  public void two() { print("two"); }
  public void three() { print("three"); }
}

三个不同的线程将会共用一个 Foo 实例。

线程 A 将会调用 one() 方法
线程 B 将会调用 two() 方法
线程 C 将会调用 three() 方法
请设计修改程序，以确保 two() 方法在 one() 方法之后被执行，three() 方法在 two() 方法之后被执行。
```

 

```
class Foo {
public:
    Foo() {
        
    }

    void first(function<void()> printFirst) {
        
        // printFirst() outputs "first". Do not change or remove this line.
     std::lock_guard<std::mutex> lock(mx_);
      printFirst();
      number_ = 1;
    }

    void second(function<void()> printSecond) {
        
        // printSecond() outputs "second". Do not change or remove this line.
        while (1)
      {
          if (number_ == 1)
          {
              std::lock_guard<std::mutex> lock(mx_);
              printSecond();
              number_ = 2;
              break;
          }
      }
    }

    void third(function<void()> printThird) {
        
        // printThird() outputs "third". Do not change or remove this line.
       while (1)
      {
          if (number_ == 2)
          {
             std::lock_guard<std::mutex> lock(mx_);
              printThird();
              number_ = 3;
              break;
          }
         
      }
    }
    
    std::mutex mx_;
    int number_ = 0;
};
class Foo
{
public:
    Foo(){}

    void first(function<void()> printFirst)
    {
        // printFirst() outputs "first". Do not change or remove this line.
        mx_.lock();
        printFirst();
        number_ = 1;
        mx_.unlock();
    }

    void second(function<void()> printSecond)
    {
        // printSecond() outputs "second". Do not change or remove this line.
        while (1)
        {
            if (number_ == 1)
            {
                mx_.lock();
                printSecond();
                number_ = 2;
                mx_.unlock();
                break;
            }
        }
    }

    void third(function<void()> printThird) 
    {
        // printThird() outputs "third". Do not change or remove this line.
        while (1)
        {
            if (number_ == 2)
            {
                mx_.lock();
                printThird();
                number_ = 3;
                mx_.unlock();
                break;

            }

        }
    }

    std::mutex mx_;
    int number_ = 0;
};
```

 

```
class Foo
{//三个线程分别有各自的函数，可以不用加锁
public:
    Foo() {}

    void first(function<void()> printFirst)
    {
        // printFirst() outputs "first". Do not change or remove this line.
        printFirst();
        number_ = 1;
    }

    void second(function<void()> printSecond)
    {
        // printSecond() outputs "second". Do not change or remove this line.
        while (1)
        {
            if (number_ == 1)
            {
                printSecond();
                number_ = 2;
                break;
            }
        }
    }

    void third(function<void()> printThird)
    {
        // printThird() outputs "third". Do not change or remove this line.
        while (1)
        {
            if (number_ == 2)
            {
                printThird();
                number_ = 3;
                break;

            }

        }
    }

    int number_ = 0;
};
```

 

# 文件操作

## 判断文件夹是否存在并创建文件夹

```
#include <experimental/filesystem>

namespace fs = std::experimental::filesystem::v1;

fs::path log_dir(fs::current_path().generic_string() +u8"\\Logs");
if (!fs::exists(log_dir) || !fs::is_directory(log_dir))
{
    fs::create_directory(log_dir);
}
```



# 区分系统是windows还是ubuntu

```
#ifdef _WIN32
#else
#endif
```



# linux和windows导出动态库

```
https://stackoverflow.com/questions/2164827/explicitly-exporting-shared-library-functions-in-linux
```

```cpp
#if defined(_MSC_VER)
    //  Microsoft 
    #define EXPORT __declspec(dllexport)
    #define IMPORT __declspec(dllimport)
#elif defined(__GNUC__)
    //  GCC
    #define EXPORT __attribute__((visibility("default")))
    #define IMPORT
#else
    //  do nothing and hope for the best?
    #define EXPORT
    #define IMPORT
    #pragma warning Unknown dynamic link import/export semantics.
#endif
```

# 加载动态库

## linux加载动态库

```
http://manpages.courier-mta.org/htmlman3/dlopen.3.html
```

```C++
#include <stdio.h>
#include <stdlib.h>
#include <dlfcn.h>
#include <gnu/lib-names.h>  /* Defines LIBM_SO (which will be a
                               string such as "libm.so.6") */
int
main(void)
{
    void *handle;
    double (*cosine)(double);
    char *error;

    handle = dlopen(LIBM_SO, RTLD_LAZY);
    if (!handle) {
        fprintf(stderr, "%s\n", dlerror());
        exit(EXIT_FAILURE);
    }

    dlerror();    /* Clear any existing error */

    cosine = (double (*)(double)) dlsym(handle, "cos");

    /* According to the ISO C standard, casting between function
       pointers and 'void *', as done above, produces undefined results.
       POSIX.1-2003 and POSIX.1-2008 accepted this state of affairs and
       proposed the following workaround:

           *(void **) (&cosine) = dlsym(handle, "cos");

       This (clumsy) cast conforms with the ISO C standard and will
       avoid any compiler warnings.

       The 2013 Technical Corrigendum to POSIX.1-2008 (a.k.a.
       POSIX.1-2013) improved matters by requiring that conforming
       implementations support casting 'void *' to a function pointer.
       Nevertheless, some compilers (e.g., gcc with the '-pedantic'
       option) may complain about the cast used in this program. */

    error = dlerror();
    if (error != NULL) {
        fprintf(stderr, "%s\n", error);
        exit(EXIT_FAILURE);
    }

    printf("%f\n", (*cosine)(2.0));
    dlclose(handle);
    exit(EXIT_SUCCESS);
}
```

## windows加载动态库

动态库静态库使用方法详解

```
https://www.cnblogs.com/LuckCoder/p/11208158.html
```

```
#include "stdafx.h"
#include <windows.h>

int main()
{
    HMODULE hmodule  = LoadLibrary("deftest.dll");
    if (hmodule)
    {
        typedef void(*LoadProc)();
        LoadProc loadproc = (LoadProc)GetProcAddress(hmodule, "MyPrint");
        if (loadproc)
        {
            loadproc();
            FreeLibrary(hmodule);
        }
        else
        {
            FreeLibrary(hmodule);
        }
    }
    return 0;
}
```

## 

# 基本函数

## scanf

```c++
//单个数字
scanf("%d", &num);
//两个数字
int num = 0, num1 = 0;
printf("请输入两个数字：");
scanf("%d%d", &num, &num1);
```

## for 循环

```
当for循环正常结束的时候循环变量一定落在数字范围之外

如果循环是采用break;语句结束的则循环结束，之后循环变量落在数字范围内

可以在循环里使用continue;语句直接跳到循环大括号的末尾，中间的语句这次循环都不执行

注：break跳出单层循环
```



## switch_case

```
int num = 0;
printf("请输入一个整数：");
scanf("%d", &num);
switch (num) 
{
case 0:
	printf("假\n");
	break;
default:
	printf("真\n");
	break;
}
```



# 基本知识

## 隐式类型转换

```
如果一个表达式里的数字类型不同就必须首先把这些数字转换成同一个类型然后再进行计算这个转换过程叫隐式类型转换，完全由计算机完成

隐式类型转换过程中一定把占地小的类型转换成占地大的类型

如果不同数字的类型占地大小一样就把整数类型转换成浮点类型，把有符号类型转换成无符号类型
```

## 强制类型转换

```
C语言里可以临时给数字任意指定类型,这叫做强制类型转换
强制类型转换的格式如下(char)300，强制类型转换有可能造成数据丢失

类型转换不会修改现有存储区的内容，只是用一个新的存储区记录转换后的结果，然后用这个新存储区里的内容做后面的计算
```

