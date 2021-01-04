

小飞机翻墙（次元链接）：

https://cylink.store/user##

毒药机场测速：

https://www.duyaoss.com/archives/3/



# youtube视频下载

https://www.ganbey.com/youtube-download-3774





## Jupyter Notebook快捷键

Alt-Enter : 运行本单元，在其下插入新单元

```
https://blog.csdn.net/lawme/article/details/51034543
```



# anaconda基础教程

```
https://docs.anaconda.com/anaconda/user-guide/getting-started/
```

2、conda常用的命令。

  1）conda list 查看安装了哪些包。

  2）conda env list 或 conda info -e 查看当前存在哪些虚拟环境

  3）conda update conda 检查更新当前conda

3、创建python虚拟环境。

   使用 conda create -n your_env_name python=X.X（2.7、3.6等)命令创建python版本为X.X、名字为your_env_name的虚拟环境。your_env_name文件可以在Anaconda安装目录envs文件下找到。

4、使用激活(或切换不同python版本)的虚拟环境。

  打开命令行输入python --version可以检查当前python的版本。

  使用如下命令即可 激活你的虚拟环境(即将python的版本改变)。

  Linux: source activate your_env_name(虚拟环境名称)

  Windows: activate your_env_name(虚拟环境名称)

  这是再使用python --version可以检查当前python版本是否为想要的。

5、对虚拟环境中安装额外的包。

  使用命令conda install -n your_env_name [package]即可安装package到your_env_name中

6、关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)。

  使用如下命令即可。

  Linux: source deactivate

  Windows: deactivate

7、删除虚拟环境。

  使用命令conda remove -n your_env_name(虚拟环境名称) --all， 即可删除。

8、删除环境中的某个包。

  使用命令conda remove --name your_env_name package_name 即可。



在创建环境之前在Anaconda Prompt中运行以下代码，切换国内清华源
仅限windows系统

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```

# vmware桥接模式下主机与虚拟机相互ping不通的几种情况

```
https://blog.csdn.net/sj_djw/article/details/98504180?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase
```



# VMware的三种网络模式

```
https://zhuanlan.zhihu.com/p/24758022
```



# 安装ubuntu双系统

```
https://www.cnblogs.com/masbay/p/11627727.html
```

# VS2017 开发linux项目

## dlopen

<img src="E:\mygithub\markdown_note\images\1550546129_560350.png" alt="img" style="zoom:50%;" />

<img src="E:\mygithub\markdown_note\images\1550546129_911639.png" alt="img" style="zoom:50%;" />

# typeora侧边折叠显示

```
https://blog.csdn.net/tian_ci/article/details/85257667
```

# typeora图床功能

```
https://www.zhihu.com/people/jia-yun-fei-16-79
```



# 录屏软件

```
Captura
```

# 打开画图

```
mspaint
```

# 虚拟机相关

## 查看系统安装的虚拟机

f9 打开虚拟机库，里面有你安装过的虚拟机

## 虚拟机全屏显示

1. 点开菜单栏的 虚拟机---------> 安装VMware Tools
2. 将下载文件拷贝到其他目录中，右键extract here
3. 在终端中输入：sudo perl vmware-install.pl，一直点击回车，完成安装



# Notepad++格式化XML文件

Try Plugins -> XML Tools -> Pretty Print (libXML) or (XML only - with line breaks Ctrl + Alt + Shift + B)

You may need to install XML Tools using your plugin manager in order to get this option in your menu.

In my experience, libXML gives nice output but only if the file is 100% correctly formed.

https://stackoverflow.com/questions/3961217/how-do-i-format-xml-in-notepad

# 查看谷歌浏览器保存的密码

1. 打开浏览器,点击右上角
2. 点击设置
3. 点击”自动填充“
4. 点击“密码”
5. 查看密码

# XML转义字符

![image-20200605233225816](E:\mygithub\markdown_note\images\image-20200605233225816.png)