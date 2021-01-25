# 什么是JSP

## jsp简介

  jsp 的全换是java server pages。Java 的服务器页面。

  jsp 的主要作用是代替Servlet 程序回传html 页面的数据。

  因为Servlet 程序回传html 页面数据是一件非常繁锁的事情。开发成本和维护成本都极高。

**扩展：** servlet直接回传html页面是多么麻烦

```java
public class PringHtml extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,IOException {
    // 通过响应的回传流回传html 页面数据
    resp.setContentType("text/html; charset=UTF-8");
    PrintWriter writer = resp.getWriter();
    writer.write("<!DOCTYPE html>\r\n");
    writer.write(" <html lang=\"en\">\r\n");
    writer.write(" <head>\r\n");
    writer.write(" <meta charset=\"UTF-8\">\r\n");
    writer.write(" <title>Title</title>\r\n");
    writer.write(" </head>\r\n");
    writer.write(" <body>\r\n");
    writer.write(" 这是html 页面数据\r\n");
    writer.write(" </body>\r\n");
    writer.write("</html>\r\n");
    writer.write("\r\n");
  }
}
```

## 创建JSP页面

web目录 New—JSP/JSPX

![img](https://i.loli.net/2021/01/25/XxosavJ7NMVBudF.jpg)

## 访问JSP

jsp 页面和html 页面一样，都是存放在web 目录下。访问也跟访问html 页面一样。

比如：

在web 目录下有如下的文件：
web 目录
a.html 页面访问地址是=======>>>>>> http://ip:port/工程路径/a.html
b.jsp 页面访问地址是=======>>>>>> http://ip:port/工程路径/b.jsp

# JSP的本质

  jsp 页面本质上是一个Servlet 程序。当我们第一次访问jsp 页面的时候。Tomcat 服务器会帮我们把jsp 页面翻译成为一个java 源文件。并且对它进行编译成为.class 字节码程序。我们在文件夹中找打JSP生成的java 源文件不难发现其里面的内容是：

![img](https://img-blog.csdnimg.cn/20210102163117176.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NoZW5ncWluZ3NoaWh1aXNodWk=,size_16,color_FFFFFF,t_70)

  我们跟踪原代码发现，HttpJspBase 类。它直接地继承了HttpServlet 类。也就是说。jsp 翻译出来的java 类，它间接了继承了HttpServlet 类。也就是说，翻译出来的是一个Servlet 程序

**总结：**通过翻译的java 源代码我们就可以得到结果：jsp 就是Servlet 程序。其底层实现，也是通过输出流。把html 页面数据回传给客户端。

# JSP的语法

## JSP头部的page指令 

  jsp 的page 指令可以修改jsp 页面中一些重要的属性，或者行为。

**语法：**

> <%@ page contentType="text/html;charset=UTF-8" language="java" **%>**
>
> //contentType，language可以在一条语句中设置多个，也可以多条语句分别设置

**扩展：常用属性说明：**

| 序号                          | 属性名       | 效果                                                         | 特别说明                                                     |
| ----------------------------- | ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1                             | language     | 表示jsp 翻译后是什么语言文件                                 | 只支持JAVA                                                   |
| 2                             | contentType  | 表示jsp 返回的数据类型是什么。即设置客户端的字符编码集       | 相当于源码中response.setContentType()参数值                  |
| 3                             | pageEncoding | 表示当前jsp 页面文件本身的字符集                             |                                                              |
| 4                             | import       | 跟java 源代码中一样。用于导包，导类。                        |                                                              |
| 以下两个属性是给out输出流使用 |              |                                                              |                                                              |
| 5                             | autoFlush    | 设置当out 输出流缓冲区满了之后，是否自动刷新冲级区。默认值是true。 | 如果为false，内存满了就报缓冲区溢出错误                      |
| 6                             | buffer       | 设置out 缓冲区的大小。默认是8kb                              | 阿帕奇公司经过科学实验，发现8kb最合理                        |
|                               |              |                                                              |                                                              |
| 7                             | errorPage    | 设置当jsp 页面运行时出错，自动跳转去的一个页面（该页面一般也是jsp，可以在该页面写“程序员哥哥努力修复中”） | 这个路径一般都是以斜杠打头，它表示请求地址为http://ip:port/工程路径/映射到代码的Web 目录 |
| 8                             | isErrorPage  | 设置当前jsp 页面是否是错误信息页面。默认是false。如果是true 可以 获取异常信息。 | 一般就用false，不用管                                        |
| 9                             | session      | 设置访问当前jsp 页面，是否会创建HttpSession 对象。默认是true。 |                                                              |
| 10                            | extends      | 设置jsp 翻译出来的java 类（servlet接口实现类）默认继承谁。   |                                                              |

## Jsp中的常用脚本

### 声明脚本（极少使用）

   相当于我们自己写一个servlet接口实现类的时候，在类里面声明类的属性，static静态代码块，类方法以及内部类。我们在JSP里面写的声明脚本，都会被“翻译到”真正的servlet接口实现类里面去。

**语法：**

> <%! 声明java 代码%>

exp: JSP中的声明和“翻译”出的类，对比

![img](https://i.loli.net/2021/01/25/BoR67lhvzjsPUGM.jpg)

 

### 表达式脚本（常用）

**（1）表达式脚本的作用是：**

​    在jsp 页面上输出数据。

**（2）表达式脚本的特点：**

① 所有的表达式脚本都会被翻译到_jspService() 方法中 ，所以_jspService()方法中的对象都可以直接使用（比如jsp九大内置对象等等一堆）

② 表达式脚本都会被翻译成为out.print()输出到页面上（所以不能以**;**结束）

**（3）表达式脚本的语法**

> **<%=**表达式**%>**

![img](https://i.loli.net/2021/01/25/tDuQemyTahYGsKw.jpg)

### 代码脚本

   就是在JSP里面写Java代码，这些代码会被“翻译”到真正的servlet接口实现类中去。

**（1）代码脚本的作用是：**

可以在jsp 页面中，编写我们自己需要的功能（写的是java 语句）。

**（2）代码脚本的特点：**

① 代码脚本翻译之后都在_jspService ()方法中，因此在_jspService()方法中的现有对象都可以直接使用。

② 代码脚本还可以和表达式脚本一起组合使用，在jsp 页面上输出数据（这个，非常爽）

**（3）代码脚本的格式是：**

> **<%
>   java 语句
> %>**

**（4）翻译后的对比**

![img](https://i.loli.net/2021/01/25/wuBqXQFdtsRN2GS.jpg)

### Jsp中的三种注释

**（1）html 注释**


> <!-- 这是html 注释-->

**说明：** html 注释会被翻译到java 源代码中。在_jspService 方法里，以out.writer 输出到客户端。

**（2） java 注释**

> <%
>   // 单行java 注释
>   /* 多行java 注释*/
> %>

**说明：**java 注释会被翻译到java 源代码中。


**（3）jsp 注释**

> <%-- 这是jsp 注释--%>

**说明：**jsp 注释可以注掉，jsp 页面中所有代码。

# Jsp九大内置对象

（不是类，是已经被类造好的对象）

  jsp 中的内置对象，是指Tomcat 在***\*翻译jsp 页面成为Servlet 源代码后\****，内部提供的九大对象，叫内置对象。

| **request**           | 请求对象            |
| --------------------- | ------------------- |
| response              | 响应对象            |
| ***\*pageContext\**** | jsp上下文对象       |
| **session**           | 会话对象            |
| **application**       | ServletContext对象  |
| config                | ServletConfig对象   |
| out                   | jsp输出流对象       |
| page                  | 指向当前的jsp的对象 |
| exception             | 异常对象            |

 

源码参考以下：

![img](https://i.loli.net/2021/01/25/aN8Tim1pYs5QPgV.jpg)

# Jsp四大域对象

​    域对象是可以像Map 一样存取数据的对象。四个域对象功能一样。不同的是它们对数据的存取范围。

| 域对象      | 所属类             | 说明                                                       |
| ----------- | ------------------ | ---------------------------------------------------------- |
| pageContext | PageContexImpl     | 当前jsp页面范围内有效                                      |
| request     | HttpServletRequest | 一次请求有效                                               |
| session     | HttpSession类      | 一个会话范围内有效（打开浏览器访问服务器，直到关闭浏览器） |
| application | ServletContext     | 整个web工程范围内都有效（只要web工程不停止，数据都在）     |

   虽然四个域对象都可以存取数据。在使用上它们是有优先顺序的。四个域在使用的时候，优先顺序分别是，他们从小到大的范围的顺序。

pageContext ====>>> request ====>>> session ====>>> application

**演示：**

工程下创建一个scope.jsp页面

```java
<body>
<h1>scope.jsp 页面</h1>
<%
// 往四个域中都分别保存了数据，看看后面哪些可以获取到值
pageContext.setAttribute("key", "pageContext");
request.setAttribute("key", "request");
session.setAttribute("key", "session");
application.setAttribute("key", "application");
%>

<%-- 同一个JSP页面，4个都能获取到值--%>
pageContext 域是否有值：<%=pageContext.getAttribute("key")%> <br>
request 域是否有值：<%=request.getAttribute("key")%> <br>
session 域是否有值：<%=session.getAttribute("key")%> <br>
application 域是否有值：<%=application.getAttribute("key")%> <br>

<% //现在做一个请求转发，转发给另一个Servlet处理（jsp本质就是Servlet）
request.getRequestDispatcher("/scope2.jsp").forward(request,response);
%>
</body>
```

```java
scope2.jsp 页面
<body>

<h1>scope2.jsp 页面</h1>

  <%--离开scope1.jsp  pageContext 已经没法获取到值了--%>
  pageContext 域是否有值：<%=pageContext.getAttribute("key")%> <br>

  <%--如果用浏览器，再次请求scope2.jpg，request也没法获取到值了--%>
  request 域是否有值：<%=request.getAttribute("key")%> <br>

  <%--客户端关闭浏览器后，这个也会没得值--%>
  session 域是否有值：<%=session.getAttribute("key")%> <br>

  <%--重启服务器，才会没得值去‘’--%0

A
  application 域是否有值：<%=application.getAttribute("key")%> <br>
</body>
```

# jsp的输出

可以统一使用out.print()来进行输出

jsp中的out输出和response.getWriter输出的区别

out输出底层代码是让out缓冲区的数据先追加到response缓冲区以后，再开始从response缓冲区输出数据。所以，即使out输出的代码在前面，也会先输出response的数据。

![img](https://img-blog.csdnimg.cn/20210103124354151.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NoZW5ncWluZ3NoaWh1aXNodWk=,size_16,color_FFFFFF,t_70)

**总结：**

① 由于jsp 翻译之后，底层源代码都是使用out 来进行输出，所以一般情况下。我们在jsp 页面中统一使用out 来进行输出。避免打乱页面输出内容的顺序。

② out.write() 输出字符串没有问题，但由于底层问题，导致，没法输出数值型，因此舍弃

③ out.print() 输出任意数据都没有问题（都转换成为字符串后调用的write 输出）

**深入源码，浅出结论**：在jsp 页面中，可以统一使用out.print()来进行输出

# Jsp的常用标签

##  静态包含（实际常用）

​    一个网站的很多页面，某些模块很可能是重复的。比如最底下一般都是（加入我们，联系方式等等），每个页面都写一份，太麻烦了，因此JSP给我们准备了静态包含功能。

![img](https://i.loli.net/2021/01/25/sfhnU3zr79x8AKZ.jpg)

**（1）语法：**

> **<%@** include file="/"%> 
>
> file 属性指定你要包含的jsp 页面的路径
>
> 地址中第一个斜杠/ 表示为http://ip:port/工程路径/ 映射到代码的web 目录
>
> **复习：**由于JSP也是Servlet页面，由服务端解析，因此/可以到工程路径
>
> **exp：**让当前页面显示include文件夹下，footer.jsp的数据
>
> <%@ include file="/include/footer.jsp"%>

**（2）静态包含的特点：**

① 静态包含不会翻译被包含的jsp 页面。

② 静态包含其实是把被包含的jsp 页面的代码拷贝到包含的位置执行输出。 （在哪个位置用包含，就在哪里显示引用页面的内容）

## 动态包含

  动态包含也可以像静态包含一样。把被包含的内容执行输出到包含位置

### 动态包含的特点

① 动态包含会把包含的jsp 页面也翻译成为java 代码，然后在准备调用包含页面的jsp页面中使用如下代码去调用被包含的jsp 页面执行输出。

   JspRuntimeLibrary.include(request, response, "/include/footer.jsp", out, false);

**说明：**该方法把把自己jsp页面的几个对象作为实参，通过以上方法，给调用的jsp页面使用，输出他的内容。

② 动态包含，还可以传递参数，从main.jsp传递给被调用的footer.jsp

### 语法

> <jsp:include page=""> 【要传递的参数】  </jsp:include> 
>
> page 属性是指定你要包含的jsp 页面的路径
>
> exp:
>
> <jsp:include page="/include/footer.jsp">
>     <jsp:param name="username" value="bbj"/>
>     <jsp:param name="password" value="root"/>
> </jsp:include>
>
> **说明：**这些参数可以再传给被调用的footer.jsp。

### 动态包含底层原理

![img](https://img-blog.csdnimg.cn/20210103133112928.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NoZW5ncWluZ3NoaWh1aXNodWk=,size_16,color_FFFFFF,t_70)

## Jsp标签转发 （请求转发标签）

  就是通过jsp来实现原来servlet里面的请求转发功能

**语法：**

> <jsp:forward page=""></jsp:forward>
>
> **说明：**是请求转发标签，它的功能就是请求转发
>
> page 属性设置请求转发的路径
>
> exp:将请求转发给scop2.jsp处理
>
> <jsp:forward page="/scope2.jsp"></jsp:forward>

**exp：**输出一个表格，里面有10个学生成绩

![img](https://img-blog.csdnimg.cn/20210103210957708.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NoZW5ncWluZ3NoaWh1aXNodWk=,size_16,color_FFFFFF,t_70)

 

```java
public class Student {
  private Integer id;
  private String name;
  private Integer age;
  private String phone;
}
 
 
public class SearchStudentServlet extends HttpServlet{
  @Override
  protected void doGet() throws ServletException,IOException{
    //获取请求参数（代码略）
    //发sql语句查询学生信息（代码略）
    //使用for循环生成查询到的数据模拟
    List<Student> studentList= new ArrayList<Student>();
    for(int i=0; i<10; i++){
      int t= i+1;
      studentList.add(new Student(t,"name"+t,18+t,"phone"+t));
    }
    //保存查询到的结果（学生信息）到request域中
    req.setAttribute("stuList",studentList);
    //请求转发到showStudent.jsp页面
    req.getRequestDispatcher("/test/showStudent.jsp").forward(req,resp);
  }
}
```

 

# 参考资料

https://blog.csdn.net/chengqingshihuishui/article/details/112094816