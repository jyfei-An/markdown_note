# C++之父给C程序的建议

## 1.慎用宏

#define PAI 3.14 ==》const double PAI = 3.14；

#define STATE_SLEEP  0 
#define STATE_RUN    1
#define STATE_STOP   2
==>
  enum STATE{SLEEP,RUN,STOP}

#define max(a,b) ((a)>(b)?(a):(b))
==>inline int max(int a,int b){
   return a >b?a:b;
}

## 2 变量随用随声明同时初始化

## 3 尽量使用new/delete取带malloc/free

## 4 少用void*,指针计算、联合体、强制转换

## 5 尽量用string表示字符串，少用C风格的char*

# 一 C++语言概述

## 1 历史背景

### 1.1 C++的江湖地位

TIOBE：java、C、C++、python、C#

### 1.2 C++之父，Bjarne Stroustrup(1950--)

1979,Cpre,为C语言提供类的机制
1983,发布全新编程语言：C with class，后来命令为C++
1985,CFront1.0,《The C++ Programming Language》

### 1.3 C++发展过程

1987年，GNU C++
1990年，Borland C++(BC)
1992年，microsoft C++(VC)
1998年，ISO C++98
2003年，对C++98进行修订，C++03
2011年，ISO C++11/C++0x
2014年，ISO 对C++11做了部分扩展,C++14
*2017年，据说C++17

## 2 应用领域

### 2.1 游戏

### 2.2 科学计算

### 2.3 网络通信(ACE)

### 2.4 操作系统和设备驱动

### 2.5 其它...

## 3 C和C++

### 3.1 都是编译型语言

### 3.2 都是强类型语言，C++更强

### 3.2 C++其去除了C中不好的特性

### 3.3 C++增加很多好的特性：

​    面向对象
​    操作符重载
​    继承与多态
​    异常
​    泛型编程(STL)

### 3.4 C++比C更适合大型软件的开发

# 二 第一个C++程序

## 1 编译方式

1）gcc xx.cpp -lstdc++
2）g++ xx.cpp

## 2 文件扩展名

1) .cpp,最常用
2) .cc
3) .C
4) .cxx

## 3 头文件

#include <iostream>
#include <cstdio>==等价==> #include<stdio.h>

## 4 输入和输出

用cin表示标准输入，用cout表示标准输出

//printf("hello world\n");
cout << "hello world" << endl;

"<<":插入运算符

int a=10；
double d=3.14；
char* str="abcdef";

//printf("%d,%lf,%s\n",a,d,str);
cout << a << ',' << d << ',' << str << endl;


">>":提取运算符
int number;
int number2;
//scanf("%d%d",&number,&number2);
cin >> number >> number2;

## 5 "std::"标准名字空间

## 6 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/cout_namespce_struct_enum_union/main.cpp



# 三 名字空间

## 1 名字空间作用

1）避免名字冲突
2）划分逻辑作用域

## 2 定义

namespace 名字空间名{
   int x;
   void foo(void){}
   struct Stduent{};
   namespace ns2{}
}
eg:
namespace ns1{
   char name[20] = "limu";
   namespace ns2{
	char name[20] = "limu";
   	namespace ns3{
		char name[20] = "limu";
	}
   }
}
ns1::name;
ns1::ns2::name;
ns1::ns2::ns3::name;

## 3 名字空间的使用

1）通过作用域限定符"::"
  名字空间名::要访问的成员;

## 2）名字空间指令

  using namespace 名字空间名;
  在该条指令以后的代码中，指定名字空间中的成员都可以见，访问其中的成员可以省略作用域限定.
  eg:
  namespace ns1{
     char name[20] = "limu";
  }
  int main(void){
     strcpy(name,"lilin");//error
     using namespace ns1;
     strcpy(name,"lilin");//ok
     //...
  }

## 3)名字空间声明

  using 名字空间名::名字空间成员；
  将名子空间的特定成员引入当前作用域，在该作用域中访问这个成员如同访问自己的成员一样，可以省略作用域限定。
  eg:
  namespace ns1{
   	int x;
   	void foo(void){}
  }
  int main(void){
     	using ns1::x;
     	x = 10;//ok
 	foo(); //error 
  }

## 4 无名名字空间

  不属于任何名字空间的标识符，将会被编译器自动放入无名名字空间中。
  使用无名名字空间的成员"::标识符"

## 5 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/cout_namespce_struct_enum_union/main.cpp

# 四 C++的结构体、联合体和枚举

## 1 C++结构体

1）定义结构体变量时，可以省略struct关键字
eg:
struct Student{//声明Student结构体类型
   char name[20];
   int age;
};
int main(){
   //struct Student s={"limu",18};//C风格写法
   Student s={"limu",18};//C++风格写法
}

2）C++结构体里面可以直接定义函数，称为成员函数，在成员函数中可以直接访问成员变量；
struct Student{//声明Student结构体类型
   char name[20];//成员变量
   int age;//成员变量
   void who(void){//成员函数
	cout << name << ',' << age << endl;
   }
};
int main(){
   Student s={"limu",18};//C++风格写法
   s.age++;
   s.who();
}

## 2 C++联合体(了解)

1）定义联合体变量可以省略union关键
2）支持匿名联合

## 3 C++枚举

1）enum关键字可以省略
2）C++枚举是一种独立的数据类型，而C中的枚举本质就是整型数。
  enum COLOR{RED,GREEN,BLUE};
  COLOR c;//RED,GREEN,BLUE
  c = RED;//c:ok c++:ok
  c = 0;//c:ok   c++:error

## 4 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/cout_namespce_struct_enum_union/main.cpp

# 五 C++字符串string 

## 1 C中表示字符串

1）双引号:"hello world";
2）字符指针：char* p=字符串；
3）字符数组: char arr[] = "hello world"； 

char* p = "hello world";
strcpy(p,"abcdef");//error
p = "abcdef";//ok

char arr[5] = "aBcD";
//strcpy(arr,p);//ok,风险

arr = "hello world!";//error
p = arr;//ok
cout << *(p++) << endl;//B

## 2  string 类型

C++兼容C字符串的同时，增加了string类型，专门表示字符串；
eg:
string s = "hello";
s = "world";//拷贝
cout << s << endl;//world

s += "！";//字符串连接
cout << s << endl;//world!

if(s >= "hello"){}...

## 3 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/stringtest/main.cpp

# 六 C++布尔类型

1 bool类型是C++中基本数据类型，表示逻辑值：true/false
2 bool内存占1个字节：1表表示true，0表示false
3 bool类型变量可以接收任意类型的变量或表达式，其值非0则为true，零则为false；

## 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/cout_namespce_struct_enum_union/main.cpp



# 七 C++字符串形式的运算符(了解)

&&  -- and
||  -- or
^   -- xor
{   -- <%
}   -- %>
！  -- not
!=  -- not_eq



# 八 C++的函数

## 1 函数重载

eg：图形库中画图函数

C：
void drawCircle(int x,int y,int r){}
void drawRect(int x,int y,int w,int h){}
......
C++:
void draw(int x,int y,int r){}
void draw(int x,int y,int w,int h){}
......
1）函数重载的定义
   在相同作用域中，定义同名的函数，但是它们的参数表有所区别，这样的函数构成重载关系。
   注：重载与函数返回类型无关，与参数名也无关。

2）函数重载的匹配
   调用重载关系的函数时，编译器将根据实参与形参匹配度，自动选择最优的重载版本。
   当前编译器(g++ v4.4.7)的一般匹配规则：
   完全匹配>常量装换>升级转换>降级转换>省略号匹配	

3）重载实现原理
  C++编译器是通过对函数进行换名，将参数表的类型信息整合到新的名字中，实现解决函数重载与名字冲突的矛盾。

  笔试题：extern "C"声明的作用？
  函数声明前加入extern "C"要求C++编译不对函数做换名，便于C的程序调用该函数。
  注：这样函数无法重载

  语法：
  extern "C" void func(void){...}
  extern "C"{
	void func1(void){...}
	void func2(void){...}
	...
  }	

## 2 C++函数的缺省参数

1)可以为函数的部分或者全部形参指定缺省值，调用该函数时，如果不给实参，就取缺省值作为相应形参的值。  
eg1:
  void func(int a,int flags=缺省值){}
  int main(void){
      	func(10);
	func(10,20);
  }
2）缺省值必须靠右，如果一个参数带有缺省值，那么这个参数的右侧的所有形参都必须带有缺省值；
eg2:
  void func(int a=100,int b=200,int c){}//error
  void func(int a,int b=200,int c){}//error
  void func(int a,int b,int c=300){}//ok
  void func(int a,int b=200,int c=300){}//ok

3）如果函数的定义和声明分开，缺省参数应该写到函数的声明部分，而定义部分不写，但最好加注释，提高代码可读性。
   void func(){}-->函数的定义
   void func();-->函数的声明 

## 3 C++函数的哑元参数

1)定义：只有类型没有变量名的形参称为哑元
void func(int/*哑元参数*/){
   ...
}  
int main(void)
{
   func(100);
}
2)为了兼容旧代码
eg：
算法库：void math_func(int a,int b){...}
使用者：
   int main(void){
	math_func(10,20);
	math_func(20,50);
	math_func(30,50);
 	//...

}

升级算法库：void math_func(int a，哑元){...}
使用者：
   int main(void){
	math_func(10,20);
	math_func(20,50);
	math_func(30,50);
 	//...
   }

3)运算符重载，区分前后++/--（后面讲）

## 4 内联函数inline

//笔试题：inline关键的作用
使用inline关键修饰的函数，表示这个函数是内联函数，编译器会尝试做内联优化，避免函数调用的开销。

1)多次的调用的小而简单的函数适合内联
2)调用次数极少或者大而复杂的函数不适合内联
3)递归函数不能内联
4)内联只是一种建议而不是一种强制要求，能否内联主要取决于编译器，有些函数不加inline关键字也会以内联的方式展开，有些函数即便加了inline关键字也不会处理为内联。

## 5 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/overload/main.cpp

# 九 C++的引用(Reference)

## 1定义 

定义引用就是给某个变量起别名，对引用的操作与对该变量的操作完全相同。
int a = 10;
int& b = a;//定义引用“b”，b就是a的别名
b++;
cout << a << endl;//11

## 2 常引用

1）定义引用的时候加const修饰，即为常引用，不能通过常引用修改引用的目标
eg：
int a = 10;
const int& b = a;//b就是a的常引用
b = 20;//error

2)普通的引用过只能引用左值(变量)，常引用也叫万能引用，既可以引用左值也可以引用右值。
eg:
int& r = 100;//error
const int& r = 100;//ok

## 3 左值和右值

1）左值：可以放在赋值运算符的左边，可以被修改，可以被取地址。
  int i;
  i = 100;
  ++i;
  &i;
常见左值：
  --》变量
  --》前++/--表达式值、赋值表达式的值
eg1:
  int number = 1;
  cout << (++number) << endl;//2
  cout << (number) << endl;//2
  ++number = 10;//ok
  ++++++number;
eg2：  
  int a = 10;
  int b = 20;
  (a = b) = 30;
  cout << a << endl;//30
  cout << b << endl;//20

2）右值：只能放在赋值运算符右边，不可以被修改，不可以被取地址。
常见右值：
   --》字面值：
	10 = i;//error
	++10;//error
	&10;//error
   --》大部分表达式的值	
eg1:
     int number = 1;
     cout << (number++) << endl;//1
     cout << (number) << endl;//2
     number++ = 20;//error
     number++++;//error
eg2:
     int a = 3;
     int b = 5;
     (a + b) = 10;//error

   --》函数返回值：
     int func(void){
	int a = 100;
	return a;//将a保存到一个临时变量中：temp=a
     }
     int main(void){
	int res = func();//int res = temp
	foo() = 200;//error
  	++foo();//error
     }

## 4 引用型的参数

1)可以将引用用于函数的参数，可以直接修改实参变量的值，同时可以减少函数调用的开销；
eg：
  void func(int& a = x){
	a++;
	cout << a << endl;//2
  }
  int main(void){
	int x = 1;
	func(x);
	cout << x << endl;//2
	return 0;
  }
2）引用参数有可能意外修改实参变量的值，如果不希望修改实参本身，可以将形参定义为常引用，在提高传参效率的同时还可以接收常量型的实参。

## 5 引用型函数返回值

1)可以将函数的返回类型声明为引用，避免函数返回值带来的内存开销，如果一个函数的返回类型被声明为引用，那么该函数返回的值可能是一个左值。

2）为了避免在函数外部修改 引用的目标变量，可以为返回一个常引用。

int g_data = 100;
int& func(void){
    g_data = 200;
    return g_data;
}
int main(void)
{
    func() = 300;//ok ==>g_data = 300
}
3）不要从函数中返回局部变量的引用，因为引用的变量的内存会在函数返回以后被释放。

4）可以在函数中返回成员变量、静态变量、全局变量的引用。

## 6 引用和指针

1）引用的本质就是指针，但是建议尽量使用引用而不是指针。
double d = 1.23；
double& rd = d;
double* const pd = &d;
rd = 100;//==等价==> *pd = 100

2）指针可以不初始化，指针指向的目标可以随意改变(除了指针常量)，而引用的必须初始化，初始化以后目标不能修改。
  int a，b；
  int* p;//ok
  p = &a;//p-->a
  p = &b;//p-->b

  int& r;//error
  int& r = a;//r引用a
  r = b;//把b的值赋值给a

3）可以定义指针的指针(二级指针)，但是不能定义引用的指针
eg：
  int a=100；
  int* p = &a;  
  int** pp = &p;//ok

  int& r=a;
  int&* pr = &r;//error

4）可以定义指针的引用,不能定义引用的引用
eg：
  int a；
  int* p = &a;
  int*& rp = p;//ok 

  int& r = a；
  int&& rr = r;//error,c++11这个东西叫右值引用

5）可以定义指针数组，但是不能定义引用数组,可以定义数组引用。
eg：
  int a，b，c；
  int* parr[3]={&a,&b,&c};
  int& rarr[3]={a,b,c};//error
eg2：
  int arr[3] = {1,2,3};
  int (&r)[3] = arr;//ok

6)函数指针和函数引用语法基本一样。
void func(int a,double d){...}
int main(void)
{
   //函数指针
   void (*pfunc)(int,double) = func;
   pfunc(100,3.14);
   //函数引用
   void (&rfunc)(int,double) = func;
   rfunc(200,4.13);
}



## 测试代码

https://github.com/Mr-jiayunfei/code_learn/blob/main/C%2B%2B/reference/main.cpp

# 十 C++动态内存分配

C语言：malloc()/free()
C++中：new/delete运算符
  new运算符用于分配内存，delete运算符用于释放内存
eg
C中:
  int* p = (int*)malloc(4);
  *p = 100;
  free(p);
  p = NULL;

C++中：
  //int* p = new int;
  //*p = 200;
  int* p = new int(200);//分配内存同时初始化
  delete p;
  p = NULL:

  int* pa = new int[10];//分配10个int空间
  pa[0] = 10;
  pa[1] = 20;
  ...
  delete[] pa;
  pa = NULL;

# 十一 类型转换

## 1 隐式类型转换

char c = 'A';
int i = c;//隐式转换

int foo(int n){
   char ch = 'A';
   return ch;//隐式转换
}
int main(void)
{
   foo('A');//隐式转换
}

## 2 显示类型转换

### 2.1 C语言 显示类型转换(强制类型转换)

  //内存地址：0x12345678
  int* pi = (int*)0x12345678;
  *pi = 100；

  char c = 'A';
  int i = (int)c;//C中形式
  int i = int(c);//C++中形式

  int* pc = (int*)c;//语法ok，逻辑不合理

### 2.2 C++兼容C的强制转换，同时增加了四种操作符的形式

1）静态类型转换
目标类型变量 = static_cast<目标类型>(源类型变量);
主要用于将void*转换为其它类型的指针
int a = 100；
void* pv = &a;//int* -> void*
int* pi = static_cast<int*>(pv); //ok

double d = 3.14;
pi = static_cast<int*>(&d);//逻辑不合理，error

2）动态类型转换（后面讲）
目标类型变量 = dynamic_cast<目标类型>(源类型变量);

3）常类型转换
目标类型变量 = const_cast<目标类型>(源类型变量);
用于去除一个指针或引用的常属性。
int main(void){
   int a = 10;
   const int* p = &a;
   //*p = 20;//error
   int* p2 = const_cast<int*>(p);
   p2 = 20;//ok

   const int& r = a;
   r = 30;//error
   int& r2 = const_cast<int&>(r);
   r2 = 30;//ok
}

4）重解释类型转换
目标类型变量 = reinterpret_cast<目标类型>(源类型变量);
-->任意类型指针或引用之间的转换
-->在指针和整型数之间的转换
eg:
int a;
int* pa = &a;
double* pd = reinterpret_cast<double*)(pa);
eg:向内存“0x23e00000”存放数据100
C: *((int*)0x23e00000) = 100；
C++:
  int p = 0x23e00000;
  int* paddr = reinterpret_cast<int*>(p);
  *paddr = 100;

# 十二 类和对象

## 1 对象

  万物皆对象，任何一种事物都可以看做是一个对象

## 2 面向对象

### 2.1 描述和表达对象

  通过对象的属性(名词、数量词、形容词)和行为(动词)来描述和表达对象。
“冰箱”
冰箱属性：品牌、容量、颜色、功耗
冰箱行为：装东西、冷冻、冷藏

### 2.2 面向对象程序设计

对自然世界的观察引入到编程实践的一种理念和方法;
数据抽象：在描述对象时，把细节东西剥离出去，只考虑一般性的、有规律性的、统一的东西。

## 3 类

  类是将对个多想的共性提取出来定义的一种新的数据类型，是对 对象的属性和行为的抽象描述，对象是类的实例化。


学生：
现实世界 	    类		   虚拟世界(编程模拟)	
具体对象--抽象--> 属性/行为 --实例化-->具体对象

struct Student{//类
   string name;
   int age;
   int id;
   void eat(...){}
   void sleep(...){}
};

Student s；//对象实例化
s.name = "limu"
s.age = 19;
s.id  = 10086;
s.eat(..);
s.sleep(...);

# 十三 类的定义和实例化

## 1 类的语法形式

class/struct 类名:继承表{
访问控制限定符:
   类名(形参表):初始化{..}//构造函数
   ~类名(void){...}//析构函数
   返回类型 函数名(形参表){...}//成员函数
   数据类型 变量名;//成员变量
};

## 2 访问控制限定符

public：公有成员，在类的内部和外部都可以访问的成员
private：私有成员，只有在类的内部才能访问
protected：保护成员（后面讲）

注：class定义的类默认的访问控制属性为private，而struct定义的类默认访问属性是public

## 3 构造函数(Constructors)

类名(构造形参表):[初始化表]{...}
1）函数名与类名相同，而且没有返回类型
2）构造函数在对象创建时自动被调用
3）构造函数主要工作是负责对象的初始化(初始化成员变量)
4）构造函数在对象被创建时一定会被调用，而且只被调用一次
class A{
public:
   A(int i=0){
  	cout << "构造函数" << endl;
	m_i = i;
   }
   void print(void){
	cout << m_i << endl;
   }
private:
   int m_i;
};
int main(void)
{
   A a(100);//自动调用构造函数
   a.print();//100
}

## 4 对象的创建和销毁

1）在栈区创建单个对象
类名 对象(构造实参表);
类名 对象 = 类名(构造实参表);

注：如果不需要构造实参
类名 对象;
类名 对象 = 类名();

2）在栈区创建多个对象
类名 对象数组[元素个数]={类名(构造实参表),...};


3）在堆区创建/销毁单个对象
创建：
   类名* 对象指针
 = new 类名(构造实参表);
销毁：
   delete 对象指针;


4)在堆区创建/销毁多个对象

创建：
   类名* 对象指针
 = new 类名[元素个数]{类名(构造实参表),..}
销毁：
   delete[] 对象指针;

练习：实现一个电子时钟类，用构造函数初始化时钟对象,构造参数为当前的系统时间，以秒为单位运行；
class Clock{
构造函数：
Clock(time_t t){
   //将日历时间转换成本地时间，结果保存在tm结构体中
   tm *local = localtime(&t)；
   时 = local->tm_hour;
   分 = local->tm_min;
   秒 = local->tm->sec;
}
成员函数：
  void run(void){
     while(1){
	//打印当前时间
	//秒+1
 	//sleep(1);
     }
  }
属性：时、分、秒
};
int main(void){
   Clock(time(0));
}
提示：
time(0);
//获取日历时间(time_t),从1970-1-1 0:0:0到现在经历的秒数

## 5 类的声明和定义分别放在不同的文件中

类的声明放在 xx.h文件中
类的实现放在 xx.cpp文件中
类的使用通常在其它的XX.cpp文件中使用

# 十四 构造函数和初始化表

## 1 构造函数可以重载

  构造函数通过参数表的差异化形成重载，创建对象是通过构造实参选择匹配，表示不同的对象创建方式。

## 2 缺省构造函数

1）如果一个没有定义构造函数，编译器会为其提供一个缺省的构造函数(无参构造函数)。
2）对于基本类型的成员变量不做初始化
3）对类类型的成员变量，用相应类型的无参构造函数初始化
eg:
class A{
public：
  A(void){m_i = 0;}
  int m_i;
}；
class B{
public:
  int m_j;
  A a;//成员子对象
};
int main(void)
{
    B b;
    cout << b.m_j << endl;//未初始化的值
    cout << b.a.m_i << endl;//0
}
4)如果定义构造函数，无论是否有参数，编译器都不会再提供无参构造函数。

## 3 类型转换构造函数（单参构造函数）

class 目标类型{
   目标类型(const 源类型& src){...}
};
在目标类型中，可以接收单个源类型对象实参的构造函数，支持从源类型到目标类型的隐式转换。

explicit关键字：使用该关键字修饰，可以强制这种转换必须显示的进行。
class 目标类型{
   [explicit] 目标类型(const 源类型& src){...}
};

## 4 拷贝构造函数

1)用一个已存在对象构造同类型的副本对象时，会调用拷贝构造函数。
class 类名{
public:
  类名(const 类名& that){...}
};
eg:
class A{...};
A a1;//调用无参构造函数
A a2(a1);//调用拷贝构造函数

2）如果一个类没有定义拷贝构造函数，那么编译器会为其提供一个缺省拷贝构造函数
  --》对基本类型的成员变量，按字节复制
  --》对类类型的成员变量，调用相应类型的拷贝构造函数

3）如果自己定义了拷贝构造函数，编译器将不再提供缺省的拷贝构造函数，这时要实现成员的复制操作，必须在自己定义的拷贝构造函数中编写代码完成。

注：一般情况不需要自定义拷贝构造函数，因为缺省的已经很好用了。

4）拷贝构造函数调用的时机
--》用已定义的对象作为同类型对象的构造实参
--》以对象的形式向函数传递参数
--》从函数中返回对象（有时会被编译器优化掉）
eg：
class A{...};
void func(A a){}
A func2(void){
   A a;
   return a;//调用拷贝构造函数
}
int main(){
  A a1;
  A a2 = a1;
  //A a2(a1);//调用拷贝构造函数
  func(a1);//调用拷贝构造函数
  A a3 = func2();//调用拷贝构造函数

}

自己定义构造函数		  编译器提供构造函数

不定义任何构造函数       缺省(无参)构造函数 缺省拷贝构造函数

非拷贝构造函数	        缺省拷贝构造函数

缺省拷贝构造函数		无

## 5 初始化表

1）指定类中成员变量的初始化方式
类名(形参表):成员变量1(初值),成员变量2(初值){
	//构造函数体
}
eg:
class A{
   /*A(int i=0){
   	m_data = i;
   }*/
   A(int i=0):m_data(i){}
   int m_data;
};

2）必须要使用初始化表的地方：
--》如果有类 类型的成员变量，而该类又没有无参构造函数，则必须通过初始化表来初始化该变量。
--》如果类中包含“const"或"引用&"成员变量，必须在初始表中进行初始化。



# 十五 this指针与常函数

## 1 this指针

1）类的成员函数中都隐藏一个该类类型的指针参数，名为this --》对于普通成员函数，this指针指向调用该函数的对象
--》对于构造函数，this指针指向正在被构造的对象
class A{
public:
   /*void print(void){
	cout << m_data << endl;
   }*/
   void print(A* this){
	cout << this->m_data << endl;
   }
   int m_data;
}; 
int main(){
   A a;
   A a2;
   a.print();//print(&a);
   a2.print();
}
2）this指针可以显示的使用，一般直接忽略，但是有些场景必须要显示的使用this指针：

--》区分作用域
--》从成员函数中返回对象自身（返回自引用）
--》从类的内部销毁对象自身（对象自毁）
class A{
public;
   void destroy(void){
	delete this;//自销毁
   }
};
int main(void){
   A* pa = new A;
   //...
   //delete pa;
   pa->destroy();
}
--》this指针作为函数的实参，实现对象之间的交互(了解)

## 2 常函数

1）在一个成员函数的参数后面加上const，这个成员函数就称为常函数。
  返回类型 函数名(形参表)const{函数体}

2)常函数中的this指针是一个常指针，不能在常函数中修改成员变量的值。
class A{
public:
   void set(int data)const{
	m_data = data;//error
   }
   /*
   void set(int data, A const* this){
	this->m_data = data;
   }
   */
   int m_data;
};
3）被mutable关键字修饰的成员变量可以在常函数中被修改

4）非常对象既可以调用非常函数，也可以调用常函数，但是常对象只能调用常函数，不能调用非常函数。
注：常对象包含常指针和常引用
class A{
public:
  //void set(int data,A* this) 
  void set(int data){
 	this->m_data = data;
  }
  int m_data;
};
void func(const A& a)
{
   a.set(100);//set(100,&a);&a:const A*
}
5）函数名和形参表相同的成员函数，其常版本和非常版本，可以构成重载关系，常对象调用常版本，非常调用调用非常版本。

# 十六 析构函数(Destructor)

## 1 析构函数和构造函数类似，是类中的特殊的成员函数

  class 类名{
  public:
	~类名(void){...}
  };
1）函数名必须是" ~类名 "
2）没有返回类型，也没有参数
3）析构函数不能被重载，一个类只能有一个析构函数
4）析构函数的功能一般和构造函数相反，主要负责清理对象生命周期内动态产生的资源。

## 2 当对象被销毁时，该对象的析构函数将被自动执行

1）栈对象离开作用域时，其析构函数被作用域终止右花括号"}"调用；
2）堆对象的析构函数被delete运算符调用。

## 3 如果一个类没有显示定义析构函数，那么编译器会为该类提供一个缺省的析构函数；

1）对基本类型的成员变量，什么也不做
2）对类类型的成员变量，调用相应类型的析构函数

## 4 对象的创建和销毁的过程

1）对象的创建
  --》为对象分配内存
  --》调用成员子对象的构造函数(声明顺序)
  --》执行构造函数的代码
2）对象的销毁
  --》执行析构函数的代码
  --》调用成员子对象的析构函数(声明逆序)
  --》释放对象的内存空间

笔试题：
class MyClass{
public:
   MyClass(){cout << "A";}
   MyClass(char c){cout << c;}
   ~MyClass(){cout << "B";}
};
int main(void)
{
   MyClass p1,*p2;
   p2 = new MyClass('X');
   delete p2;
   return 0;
}

# 十七 拷贝构造和拷贝赋值

## 1 浅拷贝和深拷贝(笔试题)

   如果一个类包含指针形式的成员变量，缺省拷贝构造函数只是复制了指针成员变量本身，而没有复制指针所指向数据，这种拷贝称为浅拷贝。
   浅拷贝将导致不同对象间的数据共享，如果数据在堆区，会在析构时引发“double free”异常.
   为此必须自己定义一个支持复制指针所指向内容的拷贝构造函数，即深拷贝。

练习：
class String{
public:
   //构造函数（无参/有参）
   /*String(const char* str = ""){
	m_str = new char[strlen(str)+1];
	strcpy(m_str,str);
   }*/
   String(const char* str = ""):m_str(
        strcpy(new char[strlen(str)+1],str)){}
   //析构函数
   ~String(void){
	delete[] m_str;
   }
   //深拷贝构造
   String(const String& that){
        //....
   }
   //访问接口
   const char* c_str(void){
	return m_str; 
   }
private:
   char* m_str;
};
int main(void)
{
    String s1("hello world");
    cout << s1.c_str() << endl;//hello world
    String s2 = s1;//拷贝构造
    cout << s2.c_str() << endl;//hello world
}