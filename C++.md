

# 函数查询手册：zeal



# std::sort的使用方法

The new C++11 standard requires that the complexity of sort to be O(Nlog(N)) in the worst case. Previous versions of C++ such as C++03 allow possible worst case scenario of O(N^2). Only average complexity was required to be O(N log N).

https://www.geeksforgeeks.org/c-qsort-vs-c-sort/

https://www.geeksforgeeks.org/sort-c-stl/



# C++类型转换

## static_cast

任何具有明确定义的类型转换，只要不包含底层const,都可以使用static_cast

example:

```c++
int j=10;
double value=static_cast<double>(j)/2; 
```

```c++
void *p =&d;
//必须确保d是double类型，否则类型不符合，会产生未定义的结果
double *dp=static_cast<double *>(p);
```



## const_cast

const_cast只能改变运算对象的底层const，即将常量对象转换成非常量对象。去掉const性质

const_cast常常用于函数重载种，如一个函数是常函数，一个是普通函数，则可以直接复用一份代码

注：如果对象是常量，再使用const_cast执行操作就会产生未定义的行为

```c++
const volatile int ci = 100;
int* pci = const_cast<int*>(&ci);
```

## reinterpret_cast

reinterpret_cast通常为运算对象的位模式提供较低层次上的重新解释

```c++
int *ip;
char *pc = reinterpret_cast<char *>(ip); //编译器不会报错
string str(pc);//可能在运行时发生错误，pc所值的真实对象是一个int而非字符
```

使用reinterpret_cast非常危险，一般不建议使用

## dynamic_cast

dynamic_cast用于将基类的指针或引用安全的转换成派生类的指针或引用

使用场景：

想使用基类的指针或者引用执行子类的某个函数并且该函数不是虚函数（一般情况，我们应该尽量使用虚函数）

当基类指针指向子类对象时，dynamic_cast是安全的并且可以执行转换，否则会执行失败或则抛出异常

```c++
//A是基类，B是子类
B b;
A* pa = &b;
B* pb = dynamic_cast<B*>(pa);
```



# 递归函数

编写递归函数步骤：

1 明确你这个函数想要干什么，函数功能是什么，要完成什么样的一件事

2 寻找递归结束条件，所谓递归，就是会在函数内部代码中，调用这个函数本身，
所以，我们必须要找出递归的结束条件，不然的话，会一直调用自己，进入无底洞。
也就是说，我们需要找出当参数为啥时，递归结束，之后直接把结果返回，请注意，
这个时候我们必须能根据这个参数的值，能够直接知道函数的结果是什么。

3 所谓递归，就是会在函数内部代码中，调用这个函数本身，所以，
我们必须要找出递归的结束条件，不然的话，会一直调用自己，
进入无底洞。也就是说，我们需要找出当参数为啥时，递归结束，之后直接把结果返回，
请注意，这个时候我们必须能根据这个参数的值，能够直接知道函数的结果是什么。

关于递归结束条件是否够严谨问题，有很多人在使用递归的时候，由于结束条件不够严谨，
导致出现死循环。也就是说，当我们在第二步找出了一个递归结束条件的时候，
可以把结束条件写进代码，然后进行第三步，但是请注意，当我们第三步找出等价函数之后，
还得再返回去第二步，根据第三步函数的调用关系，会不会出现一些漏掉的结束条件。
就像上面，f(n-2)这个函数的调用，有可能出现 f(0) 的情况，导致死循环，所以我们把它补上

4 考虑优化，是否有重复计算
如何优化？一般我们可以把我们计算的结果保证起来
可以用数组或者 HashMap 保存，我们用数组来保存把，把 n 作为我们的数组下标，f(n) 作为值，
例如 arr[n] = f(n)。f(n) 还没有计算过的时候，我们让 arr[n] 等于一个特殊值，例如 arr[n] = -1。
当我们要判断的时候，如果 arr[n] = -1，则证明 f(n) 没有计算过，否则， f(n) 就已经计算过了，且 f(n) = arr[n]。
直接把值取出来就行了

参考资料：
https://www.zhihu.com/search?type=content&q=%E9%80%92%E5%BD%92%E5%87%BD%E6%95%B0

```c++
/*给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数*/

#include <stdio.h>
#include <windows.h>
#include<algorithm>

  struct TreeNode {
      int val;
      TreeNode *left;
      TreeNode *right;
      TreeNode() : val(0), left(nullptr), right(nullptr) {}
      TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
      TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
  };


class Solution {
public:
	//1 明确函数功能，计算二叉树的最大深度
	int maxDepth(TreeNode* root) {
		//2 寻找递归结束条件
		if (!root)
		{
			return 0;
		}
		int leftheight = maxDepth(root->left);
		int rightheight = maxDepth(root->right);

		//3 最大深度 = max{左子树深度，右子树深度}+1
		//max函数在windows.h中定义
		return max(leftheight, rightheight)+1;
	
		//4 递归优化，每个节点只计算了一次，不用进行优化
	}

};

```



# 获取本机IP地址(Win+linux)

```c++
#include <iostream>
#include <optional>
#include <string>

#ifdef _WIN32
#include <winsock2.h>
#include <iphlpapi.h>
#include <stdio.h>
#include <stdlib.h>
#pragma comment(lib, "IPHLPAPI.lib")
#else
#include <sys/types.h>
#include <ifaddrs.h>
#include <netinet/in.h>
#include <string.h>
#include <arpa/inet.h>
#endif

using namespace std;

#define MALLOC(x) HeapAlloc(GetProcessHeap(), 0, (x))
#define FREE(x) HeapFree(GetProcessHeap(), 0, (x))

std::optional<std::string> GetIpAddress()
{
#ifdef _WIN32
	PIP_ADAPTER_INFO pAdapterInfo;
	PIP_ADAPTER_INFO pAdapter = NULL;
	DWORD dwRetVal = 0;

	ULONG ulOutBufLen = sizeof(IP_ADAPTER_INFO);
	pAdapterInfo = (IP_ADAPTER_INFO *)MALLOC(sizeof(IP_ADAPTER_INFO));
	if (pAdapterInfo == NULL) {
		return std::nullopt;
	}
	
	if (GetAdaptersInfo(pAdapterInfo, &ulOutBufLen) == ERROR_BUFFER_OVERFLOW) {
		FREE(pAdapterInfo);
		pAdapterInfo = (IP_ADAPTER_INFO *)MALLOC(ulOutBufLen);
		if (pAdapterInfo == NULL) {
			return std::nullopt;
		}
	}
	
	std::string ip_address;
	if ((dwRetVal = GetAdaptersInfo(pAdapterInfo, &ulOutBufLen)) == NO_ERROR) {
		pAdapter = pAdapterInfo;
		if (pAdapter) {
			ip_address = pAdapter->IpAddressList.IpAddress.String;
		}
	}
	
	if (pAdapterInfo) {
		FREE(pAdapterInfo);
	}
	
	if (!ip_address.empty()) {
		return ip_address;
	}
	return std::nullopt;

#else
	struct ifaddrs * ifAddrStruct = NULL;
	struct ifaddrs * ifa = NULL;
	void * tmpAddrPtr = NULL;

	getifaddrs(&ifAddrStruct);
	std::string ip_address;
	for (ifa = ifAddrStruct; ifa != NULL; ifa = ifa->ifa_next) {
		if (!ifa->ifa_addr) {
			continue;
		}
		if (ifa->ifa_addr->sa_family == AF_INET) { // check it is IP4
		  // is a valid IP4 Address
			tmpAddrPtr = &((struct sockaddr_in *)ifa->ifa_addr)->sin_addr;
			char addressBuffer[INET_ADDRSTRLEN];
			inet_ntop(AF_INET, tmpAddrPtr, addressBuffer, INET_ADDRSTRLEN);
	
			if (strcmp(ifa->ifa_name, "lo")) {
				continue;
			}
			else {
				ip_address = addressBuffer;
				if (!ip_address.empty()) {
					break;
				}
			}
		}
	}
	if (ifAddrStruct != NULL) freeifaddrs(ifAddrStruct);
	if (!ip_address.empty()) {
		return ip_address;
	}
	else {
		return std::nullopt;
	}

#endif
}

int main()
{
	auto res =  GetIpAddress();
	if (res.has_value())
	{
		auto ip = res.value();
		std::cout << ip << std::endl;
	}
    std::cout << "Hello World!\n";
}
```

## 参考链接

https://docs.microsoft.com/en-us/windows/win32/api/iphlpapi/nf-iphlpapi-getadaptersinfo

https://www.cnblogs.com/LuckCoder/p/14310539.html

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



# 容器

## 1 堆栈

栈，容器，适用于后进先出的数据结构

tack容器不支持随机访问，你能通过top()从栈顶获取元素，通过pop()从栈顶删除元素
不支持迭代器，不能遍历，输出时只能top()一个，然后，pop()一个

常用函数：

构造函数：stack<元素类型[,底层容器类型]> 堆栈对象(构造实参表);
　　　　　底层容器：vector/deque(默认)/list

　　　　    stack<string, vector<string> > ss;

　　　　　　stack<string, list<string> > ss;

　　　　　　stack<string> ss;

push(elem);//向栈顶添加元素，只能通过栈顶添加元素
void pop();//从栈顶移除第一个元素,不返回栈顶元素
top();//返回栈顶元素的引用，不删除元素,可通过赋值改变栈内元素，不能直接获取栈底元素
empty();//判断堆栈是否为空
size();//返回堆栈的大小

push -> push_back
pop -> pop_back
top -> back
size -> size
empty -> empty
clear -> clear

 

![img](https://i.loli.net/2021/01/04/1XTDs6JYVq8gM2z.png)

 

 

测试代码

```
void StackTest1()
{
    std::stack<std::string> ss;
    ss.push("C++!");
    ss.push("喜欢");
    ss.push("我们");
    //没有迭代器，只能通过循环遍历元素
    //输出:我们喜欢C++
    while (!ss.empty()) {
        std::cout << ss.top() << std::flush;
        ss.pop();
    }
    std::cout << std::endl;

}

void StackTest2()
{
    std::stack<std::string> ss;
    ss.push("C++!");
    ss.push("喜欢");
    ss.push("我们");

    //可通过赋值改变栈内元素的值
    ss.top() = "测试";
    //输出:测试喜欢C++
    while (!ss.empty()) {
        std::cout << ss.top() << std::flush;
        ss.pop();
    }
    std::cout << std::endl;
}
```

 

## 2 队列

队列，容器，适用于先进先出的数据结构

 queue 队列也是一个线性存储表，元素数据的插入在表的一端进行，在另一端删除，从而构成了一个先进先出FIFO（First In First Out）表。

插入一端称为队尾，删除一端称为队首。 

 默认使用双端队列deque来实现，queue也可看成一个容器适配器，将 deque 容器转换为 queue 容器。当然，也可以利用其他合适的序列容器作为底层实现queue容器。

 ![img](https://i.loli.net/2021/01/04/HdxikCzp3J5nbS6.png)

 

 

 

 C++ STL对queue队列的泛化，是通过模板类型，将默认的deque双端队列类型导入，在内部创建一个序列容器对象，来处理 queue队列的数据存储和操作，包括queue队列是否为空、取队首元素、取队尾元素、元素入队和元素出队等。由于仅需要取队首和队尾元素的操作，因此queue队列容器并不提供任何类型的迭代器。

 

常用函数：

构造函数：queue<元素类型[,底层容器类型]> 队列对象(构造实参表);

　　　　　底层容器：deque(默认)/list

　　　　    queue<string, list<string> > qs;

　　　　　　queue<string> qs;

push(elem);//向队列尾部添加元素
void pop();//删除队首元素

front(); //获取队首元素的引用

back();//获取队尾元素的引用

*empty();//判断队列是否为空
size();//返回队列的大小*

push -> push_back
pop -> pop_front
back -> back
front -> front
size -> size
empty -> empty
clear -> clear

测试代码

```
void QueueTest()
{
    //queue<string, list<string> > qs;
    queue<string> qs;
    qs.push("我们");
    qs.push("喜欢");
    qs.push("C++!");
    //输出:我们喜欢C++
    /*while (!qs.empty()) {
        cout << qs.front() << std::endl;
        qs.pop();
    }*/
    //获取队首元素
    cout << qs.front() << endl;
    //获取队尾元素
    cout << qs.back() << endl;

    //删除队首元素
    qs.pop();
    //获取队首元素
    cout << qs.front() << endl;
    cout << endl;
}
```

 

# const 限定符

## 1 const 对象必须初始化

```c++
//error,const 对象必须初始化
//const int num1;
```

## 2 const修饰后值不能改变

```C
const int num = 100;
//error,const 对象一旦创建就不能再改变
//num = 1000;
```

默认情况下，const对象仅在该文件内使用

如果想在多个文件之间共享const对象，必须在变量的定义之前添加extern关键字

```c++
//file_1.c定义并初始化了一个常量，该常量能被其他文件访问
extern const int bufsize = 100;
//file_2.h头文件
extern const int bufsize;//与file_1.c中定义的bufsize是同一个
```

## 3 const的引用

```c++
const int ci = 1024;
//正确，引用及其对应的对象都是常量
const int &ri = ci;

//错误，ri是对常量的引用，不能修改其值
//ri = 42;

//错误，试图让一个非常量引用指向一个常量对象
//int &ri2 = ci;

int i = 42;
//允许一个常量引用指向一个非常量对象
const int &ri3 = i;
```



## 4 指向常量的指针

指针指向的内存值不能改变，但可以使指针指向其他内存块

```c++
const double pi = 3.14;
//错误，pi是个常量，值不能被改变
//double *ptr = &pi;

//正确，指向常量的指针不能用于改变其所指对象的值
const double *cptr = &pi;
//错误，不能给*cptr赋值
//*cptr = 42;
```

## 5 常量指针

指针指向不能改变，但指向的内存块值可以改变

	int errnum = 0;
	//正确，curerr是一个常量指针，curerr将一直指向errnum，不能改变指针的值
	int *const curerr = &errnum;
	int num = 100;
	//错误，不能改变指针的指向
	//curerr = &num;
	
	const double pi = 3.14;
	//错误，常量指针指向常量对象
	//double *const pip = &pi;
	//pip是一个指向常量对象的常量指针
	const double *const pip = &pi;

# constexpr 限定符

常量表达式是指值不会改变并且在编译过程就能得到计算结果的表达式

## 1 声明数组维数

```c++
constexpr int size = 100;
int arr[size] = { 0 };
```

```c++
/*
 错误，函数调用在常量表达式中必须具有常量值
const int func() {
	return 10;
}

int main()
{
	int arr[func()];

}
*/
```

```c++
//正确，在编译期就确定了func计算出的值10而无需等到运行时再去计算。
constexpr int func() {
	return 10;
}

int main()
{
	int arr[func()];

}
```



## 2 constexpr函数

- 任何声明，除了：
  - `static`或`thread_local`变量。
  - 没有初始化的变量声明。
- 条件分支语句`if`和`switch`。
- 所有的循环语句，包括基于范围的`for`循环。
- 表达式可以改变一个对象的值，只需该对象的生命期在声明为constexpr的函数内部开始。包括对有`constexpr`声明的任何非`const`非静态成员函数的调用。

`goto`仍然不允许在constexpr函数中出现。



# future

## std::async创建简单异步任务

```c++
void Test1()
{
	//使用std::async创建简单异步任务
	auto future = std::async(std::launch::async, []() {
		//while(1)
		std::cout << "I'm a thread" << std::endl;
	});

	std::cout << "waiting0..." << std::endl;
	//阻塞当前线程，直至异步任务完成并返回结果
	//如果创建的线程中存在死循环，则永远不会执行下一步
	future.get();
	std::cout << "waiting1..." << std::endl;
	//get方法不能调用两次，一旦调用get方法获取线程结果，再次获取将会报错
	//future.get();

}
```

## std::async获取线程结果

```c++
void Test2()
{
	auto future = std::async(std::launch::async, []() {
		std::this_thread::sleep_for(std::chrono::seconds(5));
		return 42;
	});

	std::cout << "waiting0..." << std::endl;
	//blocking阻塞
	std::cout << future.get() << std::endl;
	std::cout << "waiting1..." << std::endl;

}
```

## 参考资料

https://baptiste-wicht.com/posts/2017/09/cpp11-concurrency-tutorial-futures.html

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



# 获取环境变量

```
https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/getenv-s-wgetenv-s?view=vs-2019
```

example：

```
// crt_getenv_s.c
// This program uses getenv_s to retrieve
// the LIB environment variable and then uses
// _putenv to change it to a new value.

#include <stdlib.h>
#include <stdio.h>

int main( void )
{
   char* libvar;
   size_t requiredSize;

   getenv_s( &requiredSize, NULL, 0, "LIB");
   if (requiredSize == 0)
   {
      printf("LIB doesn't exist!\n");
      exit(1);
   }

   libvar = (char*) malloc(requiredSize * sizeof(char));
   if (!libvar)
   {
      printf("Failed to allocate memory!\n");
      exit(1);
   }

   // Get the value of the LIB environment variable.
   getenv_s( &requiredSize, libvar, requiredSize, "LIB" );

   printf( "Original LIB variable is: %s\n", libvar );

   // Attempt to change path. Note that this only affects
   // the environment variable of the current process. The command
   // processor's environment is not changed.
   _putenv_s( "LIB", "c:\\mylib;c:\\yourlib" );

   getenv_s( &requiredSize, NULL, 0, "LIB");

   libvar = (char*) realloc(libvar, requiredSize * sizeof(char));
   if (!libvar)
   {
      printf("Failed to allocate memory!\n");
      exit(1);
   }

   // Get the new value of the LIB environment variable.
   getenv_s( &requiredSize, libvar, requiredSize, "LIB" );

   printf( "New LIB variable is: %s\n", libvar );

   free(libvar);
}
```



# 随机数生成

## rand函数

在函数的开始处调用下面语句设置随机数种子

```c++
#include <cstdlib>
#include <ctime>
srand (static_cast <unsigned> (time(0)));
```

```cpp
double randMToN(double M, double N)
{
    return M + (rand() / ( RAND_MAX / (N-M) ) ) ;  
}
```

缺点：rand函数精度较低，最大随机数为65536，随机浮点数精度可能不足

![image-20200618231527979](.images/image-20200618231527979.png)

## C++11random

```cpp
#include <random>
#include <iostream>
 
int main()
{
    std::random_device rd;  // 将用于获得随机数引擎的种子
    std::mt19937 gen(rd()); // 以 rd() 播种的标准 mersenne_twister_engine
    //随机浮点数生成器
    std::uniform_real_distribution<> dis(1, 2);
    for (int n = 0; n < 10; ++n) {
        // 用 dis 变换 gen 生成的随机 unsigned int 为 [1, 2) 中的 double
        std::cout << dis(gen) << ' '; // 每次调用 dis(gen) 都生成新的随机 double
    }
    std::cout << '\n';
}
```

![image-20200618231419676](.images/image-20200618231419676.png)





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



## double 转string

1. tostring

   std:to_string()方法只能精确到6位小数点

       double d = 3.1415926535897932384;
       std::string str = std::to_string(d);
       std::cout << str << std::endl; // 3.141593

2. 使用stringstream，在输入流时使用setprecision设置精度（精度为15位）。

   ```c++
   #include <sstream>
   #include <iomanip>
   
   double d = 3.1415926535897932384;
   std::string str;
   std::stringstream ss;
   ss << std::setprecision(15) << d;
   str = ss.str();  // 3.14159265358979
   ```

   



# C风格的split

```c
#include<stdio.h>
#include <string.h>

int main() {
   char string[50] = "Hello! We are learning about strtok";
   // Extract the first token
   char * token = strtok(string, " ");
   // loop through the string to extract all other tokens
   while( token != NULL ) {
      printf( " %s\n", token ); //printing each token
      token = strtok(NULL, " ");
   }
   return 0;
}
```

# lambda表达式

https://www.cnblogs.com/LuckCoder/p/8668125.html

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

