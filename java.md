https://blog.csdn.net/qq_45554909/article/details/111611282

https://blog.csdn.net/qq_45554909/article/details/111658223



[IDEA 整合 Tomcat 服务器_少年西西的博客-CSDN博客](https://blog.csdn.net/qq_45554909/article/details/111712970)



# Maven

https://www.jetbrains.com/help/idea/maven-support.html#javaee_maven

# Tomcat 

## startup.bat后控制台乱码

解决：

1. 打开tomcat文件夹到conf目录下找到logging.properties文件；

![img](https://i.loli.net/2021/01/19/I9AcdRgSmOfWzGt.jpg)

2. 找到 java.util.logging.ConsoleHandler.encoding = utf-8 这行；

![img](https://i.loli.net/2021/01/19/7u5pa8k1Y6zTNnR.jpg)

3. 更改为 java.util.logging.ConsoleHandler.encoding = **GBK**，就可以了！



# Idea第一个HelloWorld程序

## 1 新建project

![image-20210114210026812](https://i.loli.net/2021/01/14/tnEo2gLlDzYwUMd.png)



## 2 选择java程序

![image-20210114210111396](https://i.loli.net/2021/01/14/Ee1PvhQokOY53zr.png)

3 填写项目名字和路径

![image-20210114210154464](https://i.loli.net/2021/01/14/DJ7Or5sxQtGCBZY.png)



## 3 创建package

点击src，右键，选择new,选择Package,创建包（包名不能以数字开头），包名为java01.helloworld

java项目以Package的形式管理源文件，单个java文件直接创建文件亦可

Idea会根据包名自动创建相应的文件夹，当前包名会自动创建java01文件夹和helloworld文件夹

![image-20210114210310723](https://i.loli.net/2021/01/14/sk6elCIic5RPTtv.png)



## 4 创建class

点击包名，右键选择new，选择Java Class,填写Class名称为HelloWorld，Idea会自动创建HelloWorld.java文件

![image-20210114211444828](https://i.loli.net/2021/01/14/wKWP6b4Uexv7QfJ.png)



## 5 编写源文件

```java
package java01.helloworld;
//public的类必须与文件名称相同，私有类可以不同
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```



## 6 运行程序

在源文件空白处右键，选择Run‘HelloWorld.main()’运行程序

![image-20210114211727047](https://i.loli.net/2021/01/14/QmokPpAU2zyciIh.png)

# Idea2020创建第一个应用程序并打包

https://www.jetbrains.com/help/idea/creating-and-running-your-first-java-application.html





# 环境变量设置

```
export JAVA_HOME=/usr/lib/jvm/default-java
export PATH=$JAVA_HOME/bin:$PATH 
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

