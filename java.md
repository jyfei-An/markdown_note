https://blog.csdn.net/qq_45554909/article/details/111611282

https://blog.csdn.net/qq_45554909/article/details/111658223



[IDEA 整合 Tomcat 服务器_少年西西的博客-CSDN博客](https://blog.csdn.net/qq_45554909/article/details/111712970)

https://blog.csdn.net/qq_45554909/article/details/111713007

https://blog.csdn.net/qq_45554909/article/details/111713007

https://blog.csdn.net/weixin_43732424/article/details/107783879

https://blog.csdn.net/weixin_43732424/article/details/107783840

# Maven

https://www.jetbrains.com/help/idea/maven-support.html#javaee_maven

# Tomcat 

![image-20210124213807930](C:/Users/jiayunfei/AppData/Roaming/Typora/typora-user-images/image-20210124213807930.png)

## startup.bat后控制台乱码

解决：

1. 打开tomcat文件夹到conf目录下找到logging.properties文件；

![img](https://i.loli.net/2021/01/19/I9AcdRgSmOfWzGt.jpg)

2. 找到 java.util.logging.ConsoleHandler.encoding = utf-8 这行；

![img](https://i.loli.net/2021/01/19/7u5pa8k1Y6zTNnR.jpg)

3. 更改为 java.util.logging.ConsoleHandler.encoding = **GBK**，就可以了！





# 将myeclipse的web项目导入Idea

## myeclipse的web项目目录结构

![image-20210124205347543](https://i.loli.net/2021/01/24/zkcibJ7ZfmA6xYt.png)

## idea 打开项目

### 1 File->New->Project from existing Sources



![image-20210124205525459](https://i.loli.net/2021/01/24/DqYymxWwgkEUZhR.png)



### 2 选择jidian文件夹

![image-20210124205727548](https://i.loli.net/2021/01/24/aFnHBRx8fmW9AyU.png)



### 3 选择默认即可

![image-20210124205825960](https://i.loli.net/2021/01/24/5j8PlJCQSnUri4O.png)

### 4 File->Project Structure

将modules的paths的output path设置为webroot/web-inf/classes目录下

dependencies下设置module sdk,并将红色的class给删除掉

![image-20210124210142480](https://i.loli.net/2021/01/24/2fD6SnUlbsP8M9W.png)





### 5 在’Facets’,添加web应用

![这里写图片描述](https://i.loli.net/2021/01/24/knfUIZXC3AaRmPL.png)

### 6 修改web.xml目录

修改web.xml的地方为webroot的web-inf目录下，web resources root为WebRoot， 然后点击create artifact
![image-20210124210142480](https://i.loli.net/2021/01/24/2fD6SnUlbsP8M9W.png)

### 7 apply,ok

## 配置tomcat启动

![这里写图片描述](https://i.loli.net/2021/01/24/nmtzyGcHbUZ23QV.png)
![这里写图片描述](https://i.loli.net/2021/01/24/bo3qKS2rAy4tdmU.png)
![这里写图片描述](https://i.loli.net/2021/01/24/yf7TIQp2GB3tUiP.png)
![这里写图片描述](https://i.loli.net/2021/01/24/JocHgDWbavV5u6y.png)
然后ok，确定，接着即可启动tomcat查看效果
![这里写图片描述](https://i.loli.net/2021/01/24/JNTBARbZvzgYkxE.png)



## 参考链接

https://blog.csdn.net/lxfHaHaHa/article/details/78285102





# IDEA创建第一个Web程序

https://m.yisu.com/zixun/314055.html

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

