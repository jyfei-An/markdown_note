# 继承/多态

```c#
class Product
{
    public virtual void Make()
    {
        Console.WriteLine("无进货需求");
    }
}
class Television:Product
{
    public override void Make()
    {
        Console.WriteLine("生产电视");
    }
}

```





# 字典用法

``` c#
Dictionary<string,string> students=new Dictionary<string,string>();
//插入
students.Add ("S001","张三");
students.Add ("S002","李四");
students["S003"]="王五";

//删除
students.Remove ("S000"); //直接删除key即可

//修改
students["S003"]="王五"; 	//直接赋值即可
```





# 数组用法

```
double[] balance = new double[10];
double[] balance = { 2340.0, 4523.69, 3421.0};
int [] marks = new int[5]  { 99,  98, 92, 97, 95};
int [] marks = new int[]  { 99,  98, 92, 97, 95};
int [] marks = new int[]  { 99,  98, 92, 97, 95};
int[] score = marks;
```

```c#
//遍历数组元素  
foreach (var num in nums )
{
   Console.WriteLine(num);
}

//获取数组长度,注意Length不加括号
 int length = numbers.Length;
```





# list用法

```C#
 List<int> li = new List<int>();
li.Add(10);
```





# 接收用户输入

```C#
int num;
num = Convert.ToInt32(Console.ReadLine());
```

# 程序输出

```C#
Console.WriteLine("hello world");//输出
```





# VS开发C#一般步骤

1. 文件->新建->项目
2. 左侧选择Visual C#，然后右侧选择控制台应用程序
3. 选项目位置，填写项目名称，点击确定即可

# helloworld



```c#
namespace helloworld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("hello world");//输出
            Console.ReadKey();              //暂停
        }
    }
}
```

# 代码折叠



```c#
#region
int num = 10;
string s="hello world";
#endregion
```

# VS快捷键

Ctrl+R+E 自动生成属性访问方法