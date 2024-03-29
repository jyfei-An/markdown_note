# 参考资料

tomcat源码及安装包

链接：https://pan.baidu.com/s/1OdJppvTkXTc_1UknCh3MnQ 
提取码：bf33 

# JavaWeb

## JavaWeb 的概念

### **a)什么是 JavaWeb**

JavaWeb 是指，所有通过 Java 语言编写可以通过浏览器访问的程序的总称，叫 JavaWeb。 JavaWeb 是基于请求和响应来开发的。

### **b)什么是请求**

请求是指客户端给服务器发送数据，叫请求 Request。

### **c)什么是响应**

响应是指服务器给客户端回传数据，叫响应 Response。

### **d)请求和响应的关系**

请求和响应是成对出现的，有请求就有响应
![在这里插入图片描述](https://i.loli.net/2021/01/30/9ehoxOIXqSbvLtN.png)

## 2.Web 资源的分类

web 资源按实现的技术和呈现的效果的不同，又分为静态资源和动态资源两种。
**静态资源：** html、css、js、txt、mp4 视频 ,jpg 图片
**动态资源**： jsp 页面、Servlet 程序

## 3.常用的 Web 服务器

- **Tomcat：** 由 Apache 组织提供的一种 Web 服务器，提供对 jsp 和 Servlet 的支持。它是一种轻量级的 javaWeb 容器（服务 器），也是当前应用最广的 JavaWeb 服务器（免费）。
- **Jboss**：是一个遵从 JavaEE 规范的、开放源代码的、纯 Java 的 EJB 服务器，它支持所有的 JavaEE 规范（免费）。
- **GlassFish**： 由 Oracle 公司开发的一款 JavaWeb 服务器，是一款强健的商业服务器，达到产品级质量（应用很少）。
- **Resin**：是 CAUCHO 公司的产品，是一个非常流行的服务器，对 servlet 和 JSP 提供了良好的支持， 性能也比较优良，resin 自身采用 JAVA 语言开发（收费，应用比较多）。
- **WebLogic**：是 Oracle 公司的产品，是目前应用最广泛的 Web 服务器，支持 JavaEE 规范， 而且不断的完善以适应新的开发要求，适合大型项目（收费，用的不多，适合大公司）。

## 4.Tomcat 服务器和 Servlet 版本的对应关系

当前企业常用的版本 7.*、8.*
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201224110507845.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

Servlet 程序从 2.5 版本是现在世面使用最多的版本（xml 配置） 到了 Servlet3.0 之后。就是注解版本的 Servlet 使用。
以 2.5 版本为主线讲解 Servlet 程序

# TomCat的使用

## 1.安装

找到你需要用的 Tomcat 版本对应的 zip 压缩包，解压到需要安装的目录即可。

## 2.目录介绍

**bin** 专门用来存放 Tomcat 服务器的可执行程序
**conf** 专门用来存放 Tocmat 服务器的配置文件
**lib** 专门用来存放 Tomcat 服务器的 jar 包
**logs** 专门用来存放 Tomcat 服务器运行时输出的日记信息
**temp** 专门用来存放 Tomcdat 运行时产生的临时数据
**webapps** 专门用来存放部署的 Web 工程。
**work** 是 Tomcat 工作时的目录，用来存放 Tomcat 运行时 jsp 翻译为 Servlet 的源码，和 Session 钝化的目录

## 3.如何启动 Tomcat 服务器

找到 Tomcat 目录下的 bin 目录下的 startup.bat 文件，双击，就可以启动 Tomcat 服务器。

**如何测试 Tomcat 服务器启动成功？？？**
打开浏览器，在浏览器地址栏中输入以下地址测试： 

- 1、http://localhost:8080

- 2、http://127.0.0.1:8080

- 3、http://真实 ip:8080
  当出现如下界面，说明 Tomcat 服务器启动成功！！！
  ![在这里插入图片描述](https://i.loli.net/2021/01/30/GvW8wXe5U27RxSc.png)
  
  ## 服务器启动失败原因
  
  **常见的启动失败的情况有**，双击 startup.bat 文件，就会出现一个小黑窗口一闪而来。 这个时候，失败的原因基本上都是因为没有配置好 JAVA_HOME 环境变量
  **配置 JAVA_HOME 环境变量**
  ![在这里插入图片描述](https://i.loli.net/2021/01/30/fcreWbUuYlp5vs8.png)
  **常见的 JAVA_HOME 配置错误有以下几种情况：**
  
- 一：JAVA_HOME 必须全大写。

- 二：JAVA_HOME 中间必须是下划线，不是减号

- 三：JAVA_HOME 配置的路径只需要配置到 jdk 的安装目录即可。不需要带上 bin 目录

- 

**另一种启动 tomcat 服务器的方式**

- 1、打开命令行
- 2、cd 到 你的 Tomcat 的 bin 目录下
- 3、敲入启动命令： catalinarun
  ![在这里插入图片描述](https://i.loli.net/2021/01/30/ma1wVInxT7OokQF.png)

## 4.Tomcat 的停止

- 1、点击 tomcat 服务器窗口的 x 关闭按钮
- 2、把 Tomcat 服务器窗口置为当前窗口，然后按快捷键 Ctrl+C
- 3、找到 Tomcat 的 bin 目录下的 shutdown.bat 双击，就可以停止 Tomcat 服务器

## 5.如何修改 Tomcat 的端口号

**Mysql 默认的端口号是**：3306
**Tomcat 默认的端口号是**：8080
找到 Tomcat 目录下的 conf 目录，找到 server.xml 配置文件
![在这里插入图片描述](https://i.loli.net/2021/01/30/R254cHrBQW6vNfk.png)
平时上百度：http://www.baidu.com:80
**HTTP 协议默认的端口号是：** 80
当端口号为80时，则不会在地址栏上显示80这个端口号

## 6.如何部暑 web 工程到 Tomcat 中

**第一种部署方法：只需要把 web 工程的目录拷贝到 Tomcat 的 webapps 目录下即可**。
**1、在 webapps 目录下创建一个 book 工程**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201224231006880.png)
**2、把项目拷贝到里面**
![在这里插入图片描述](https://i.loli.net/2021/01/30/3yCqEVcfiKSIheA.png)
**3、如何访问 Tomcat 下的 web 工程。**
**只需要在浏览器中输入访问地址格式如下**
![在这里插入图片描述](https://i.loli.net/2021/01/30/o2rGAFIHV4L5Ok8.png)![在这里插入图片描述](https://i.loli.net/2021/01/30/PnZ8N4Q6FMVRifI.png)

**第二种部署方法：这种配置工程可以在任何位置不一定要在webapps 目录下即可。**

找到 Tomcat 下的 conf 目录\Catalina\localhost\ 下,创建如下的配置文件
![在这里插入图片描述](https://i.loli.net/2021/01/30/hyEKfke4xTXM8vu.png)

abc.xml 配置文件内容如下(注意该xml文件的编码集要是utf-8)：（假设现在book工程路径为：D:\book）配置完后要重启TomCat
![在这里插入图片描述](https://i.loli.net/2021/01/30/5EN2UrxwGFuAXpY.png)
访问这个工程的路径如下:http://ip:port/abc/ 就表示访问 D:\book 目录

## 7.手托html页面到浏览器和在浏览器中输入http://ip:端 口号/工程名/访问的区别

**手托 html 页面的原理**
![在这里插入图片描述](https://i.loli.net/2021/01/30/qkJjSfatG9AWbeB.png)

**输入访问地址访问的原因**
![在这里插入图片描述](https://i.loli.net/2021/01/30/gAazY39CLyhNES5.png)

## 8.ROOT 的工程的访问，以及 默认 index.html 页面的访 问

当我们在浏览器地址栏中输入访问地址如下：
http://ip:port/ ====>>>> 没有工程名的时候，**默认访问的是 ROOT** 工程。
当我们在浏览器地址栏中输入的访问地址如下：
http://ip:port/工程名/ ====>>>> 没有资源名，**默认访问 index.html 页面**

# IDEA 中动态 web 工程的操作

## a)IDEA 中如何创建动态 web 工程

1、创建一个新模块：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225026620.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

2、选择你要创建什么类型的模块：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225041304.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
3、输入你的模块名，点击【Finish】完成创建。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225051159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
4、创建成功如下图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225102782.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## b)Web 工程的目录介绍

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225120548.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## c)如何给动态 web 工程添加额外 jar 包

1、可以打开项目结构菜单操作界面，添加一个自己的类库
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225138558.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
2、添加你你类库需要的 jar 包文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225157102.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
3、选择你添加的类库，给哪个模块使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225209781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
4、选择 Artifacts 选项，将类库，添加到打包部署中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225219934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## d)如何在 IDEA 中部署工程到 Tomcat 上运行

1、建议修改 web 工程对应的 Tomcat 运行实例名称：
![在这里插入图片描述](https://i.loli.net/2021/01/30/Lc3jpICd2WuNUeV.png)
**Edit Configrations**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225336201.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
2、确认你的 Tomcat 实例中有你要部署运行的 web 工程模块：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225348734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
3、你还可以修改你的 Tomcat 实例启动后默认的访问地址：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225359758.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)
4、在 IDEA 中如何运行，和停止 Tomcat 实例。

4.1、正常启动 Tomcat 实例：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225410628.png)
4.2、Debug 方式启动 Tomcat 运行实例：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225422835.png)
4.3、停止 Tomcat 运行实例：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225433444.png)
4.4、重启 Tomcat 运行实例：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225443892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## e)修改工程访问路径

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225458399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## f) 修改运行的端口号

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225513533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## g)修改运行使用的浏览器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201225225525219.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)

## h)配置资源热部署

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122522554272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NTU0OTA5,size_16,color_FFFFFF,t_70)