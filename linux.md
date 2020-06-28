# How To Fix System Program Problem Detected In Ubuntu

```
sudo gedit /etc/default/apport

Change the enabled=1 to enabled=0. Save and close the file. You won’t see any pop up for crash reports after doing this. Obvious to point out that if you want to enable the crash reports again, you just need to change the same file and put enabled as 1 again.

```

# GDB调试

```
https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/gdb.html
```

# 安装中文输入法

```
https://www.pinyinjoe.com/linux/ubuntu-18-gnome-chinese-setup.htm
```

# linux 常用工具

```
https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/crontab.html
```

## 打开多个终端窗口

```
Ctrl+Shift+T
```

## 打开多个文件窗口

```
ctrl+t
```

## fsearch搜索工具

```
https://www.addictivetips.com/ubuntu-linux-tips/fsearch-find-files-on-linux/
```

## gparted 磁盘管理工具

```
GParted
```



# Deb文件操作

## 安装deb文件

```
 sudo  dpkg  -i  package.deb
```

## 查看deb文件内容

```
dpkg  -c package.deb 
```

## 解压deb文件

```
dpkg -x package.deb 
```



# linux常用命令

## 查看动态库依赖性

```
ldd 动态库名字
```

## 查看ubuntu系统版本

```
sudo lsb_release -a
```

## 复制文件cp

```
cp  源文件(source) 目标文件(destination)
```

## 复制文件夹cp -r

```
cp  -r 源文件夹(source) 目标文件夹(destination)
```

## 文件移动mv

```
mv  source destination
```

## 文件删除rm

```
rm  文件或目录
rm命令加上-r选项就可以用来删除一个目录
```

## 压缩文件夹zip

```
zip -r foo.zip foo //压缩文件夹
```

## 清空终端窗口信息clear

```
clear
```

## 查看目录内容ls

```
ls 目录路径
如果省略目录路径就可以察看当前目录里的内容
使用-a选项可以察看目录里的所有内容
使用-l选项可以察看内容的详细信息
可以把这两个选项合并成-al
```

## 创建文件夹mkdir

```
mkdir path
mkdir命令可以用来创建目录
要求目录本身还不存在但是父目录必须存在
在命令中使用-p选项可以把路径中所有不存在
    的目录都创建出来
```



## find查找

https://vitux.com/how-to-find-files-on-the-ubuntu-command-line/

```
find /path/to/file/ -iname filename
example：
find / -iname test.txt //从根目录查找text.txt文件
```

## whereis  查找

```
whereis 命令/文件名
```

## vi模式

```
正常模式下可以执行简单命令
插入模式下可以修改文字内容
命令模式下可以执行复杂命令

每次启动vi以后一定处于正常模式下

不同工作模式之间可以互相转换
在正常模式下输入i可以进入插入模式
在正常模式下输入:可以进入命令模式
在任何时候输入esc可以进入正常模式

可以采用如下命令启动vi
vi 文件路径

可以采用两种方法退出vi
1.在命令模式下输入q!(丢失所有没保存的修改)
2.在命令模式下输入wq或x(先保存所有修改然后
		   再退出)
```



# 切换安装gcc,g++版本

```
https://linuxize.com/post/how-to-install-gcc-compiler-on-ubuntu-18-04/
```



# 虚拟机共享文件夹的位置

```
/mnt/hgfs/
```



# 安装Qtcreator

## Install Qt Creator

```bash
sudo apt install build-essential
sudo apt install qtcreator
```

If you want Qt 5 to be the default Qt version to be used when using development binaries like qmake, install the following package:

```bash
sudo apt install qt5-default
```

##  Install documentation and examples

If Qt Creator is installed thanks to the Ubuntu Sofware Center or thanks to the synaptic package manager, documentation for Qt Creator is not installed. Hitting the F1 key will show you the following message : **“No documentation available”**. This can easily be solved by installing the Qt documentation:

```bash
sudo apt install qt5-doc
```

And eventually:

```bash
sudo apt install qt5-doc-html qtbase5-doc-html
```

If examples are still missing:

```bash
sudo apt install qtbase5-examples
```

Restart Qt Creator to make the documentation available.

# 设置软件更新源

在terminal输入下面命令，弹出设置框，选择阿里云源

```
software-properties-gtk
```

# 更新全部软件

```
sudo apt-get update
sudo apt-get upgrade
```

# 卸载软件

```
//或者sudo apt-get purge <package-name>
sudo apt-get remove <application_name>
```



# vi按上下左右键为字母解决办法

```
sudo apt-get remove vim-common
sudo apt-get install vim
```



# vi卡死解决办法

```
Ctrl+S在Linux里是锁定屏幕的快捷键，如果要解锁，按下Ctrl+Q就可以了。
```



# 设置vi行号

## 临时设置

```
1. Press ESC key
2. At the : prompt type the following command to run on line numbers: set number
3. To turn off line numbering, type the following command at the :  set nonumber
```



## 永久设置

```
vi ~/.vimrc
//Append the following line:
set number
```



# 环境变量

## 设置临时环境变量

```
//export NAME=VALUE
export JAVA_HOME=/opt/openjdk11

//append PATH
exprot PATH=$PATH:YourPath
```

## 取消环境变量设置

```
//unset VARIABLE_NAME
unset JAVA_HOME
```

## 查看环境变量

```
echo $JAVA_HOME
```

## 查看所有的环境变量

```
set
```

## 设置永久环境变量

1. Create a new file under /etc/profile.d to store the global environment variable(s). The name of the should be contextual so others may understand its purpose.
   `sudo touch /etc/profile.d/http_proxy.sh`
   
2. Open the default profile into a text editor.
   `sudo vi /etc/profile.d/http_proxy.sh`
   
3. Add new lines to export the environment variables
   `export HTTP_PROXY=http://my.proxy:8080`
   `export HTTPS_PROXY=https://my.proxy:8080`
   `export NO_PROXY=localhost,::1,.example.com`
   
4. Save your changes and exit the text editor

5. restart your machine

   

   example:
   
   ```
   https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-environment-variables-in-linux/
   ```
   
   
   