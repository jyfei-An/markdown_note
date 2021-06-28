# Ubuntu开机报错“Started User Manager for UID 121“解决办法

https://blog.csdn.net/weixin_38765304/article/details/108462032

选择修复模式进行修复

# How to fix “Failed to start MokManager” / “import_mok_state() failed” after failed Ubuntu Installation

出现场景：

在secureboot开启的情况下，安装navida显卡驱动，需要设置密钥，重启之后没有加载密钥，出现上述问题，之后将secureboot关闭，问题依旧，猜测是因为硬件会加载受信任的驱动程序，插入优盘后，不能进入安装操作系统选项，依然提示这个bug，是因为优盘里面的文件不是受信任的文件，驱动程序不会直接加载，所以可将shim里面的文件进行拷贝，该文件存储了mok信息，然后优盘即可被识别，驱动程序即可被正常加载，或者选择第二种方法，手动选择加载的驱动程序

第一种方法：

1 到`(usb stick)/pool/main/s/shim`目录下找到里面的`shim`安装包，解压出其中的`data.tar.gz`中的`./usr/lib/shim/mmx64.efi.signed`，然后移动到`(usb stick)/EFI/BOOT`，并重命名为`mmx64.efi`。

2 选择相应的boot option，reset mok manager

3 安装操作系统

3 安装完成后使用之前不能使用的优盘进行重新安装操作系统

第二种方法：

The way I got this fixed was eventually pretty easy, but it took me some time to find out:

1. Enter your BIOS (I used holding F2 while booting)
2. Go to the “Boot” tab
3. Use “Add New Boot Option”
4. Press enter on “Add boot option”
5. Enter your boot title, I just named it “ubuntuinstall”
6. Press enter on “Path for boot option”
7. Select your USB
8. Select UEFI
9. Select BOOT
10. Select grubx64.efi
11. Press Create
12. Reboot, and enter BIOS again
13. Go to “Save & Exit” tab
14. Use Boot Override to launch your just created “ubuntuinstall” option
15. Ubuntu will now properly boot the installation again and you can now install it properly

# 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系

使用sudo apt-get install <packgename>时出现提示无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。

可以换个命令sudo aptitude  install <packgename>，因为aptitude会自动把所有依赖的库都帮你顺着找到，并下载好。而apt-get下载某个包中它的所有依赖项都必须存在，这就是为什么我们每次执行apt-get的时候都需要先apt-get update的更新软件包的原因。

如果提示找不到aptitude，可以先使用sudo apt-get install aptitude进行下载


# apt-get update 与 upgrade区别

apt-get是某些linux发行版使用的一个“包管理器”（还有别的发行版使用yum等，以及brew等其他平台上的包管理器，工作原理类似）。
包管理器的作用是从源（Source）服务器那里下载最新的软件包列表，然后在你需要安装某个软件包（apt-get install）的时候从列表里面查询这个软件包的版本信息、系统要求、翻译、依赖项（该软件正常运行必须安装的其它软件）并且添加到同时安装的列表里面，再查询所有安装列表里面的软件包的.deb文件下载地址，最后批量下载，自动分析安装顺序然后安装完成。
但是这个软件包列表是不会被自动下载的，需要用户使用apt-get update更新。这样，apt-get才能知道每个软件包的最新信息，从而正确地下载最新版本的软件。
至于apt-get upgrade，则是对已经安装的软件包本身进行更新的过程。由于确定要更新的软件包需要对本地安装的版本和列表的版本进行比较，所以要在update以后运行这一条。
要求在install操作之前执行update和upgrade，实际上是确保本地软件列表信息和已安装软件均为最新的过程。这样做可以最大限度地确保新安装的软件包正常工作。

# 下载搜狗输入法

## 下载链接

https://pinyin.sogou.com/linux/

## 使用文档

https://pinyin.sogou.com/linux/help.php

# 下载 Google Chrome

1 打开终端，下载安装文件

```text
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```

2 安装deb文件

```text
sudo apt install ./google-chrome-stable_current_amd64.deb
```

3 运行google chrome

命令行输入`google-chrome`启动 Chrome。或者

在活动搜索栏输入"Google Chrome”，并且点击图标，启动这个应用

4 将应用固定到左侧菜单栏中

点击图标，右键，选择添加到收藏夹

# 安装Nvidia Driver

https://www.linuxbabe.com/ubuntu/install-nvidia-driver-ubuntu-18-04

https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-18-04-bionic-beaver-linux

# 运行 apt-get 时报错（锁住）

```text
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
```

解决方案:

```text
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/lib/dpkg/lock
sudo rm /var/cache/apt/archives/lock
```

都运行一遍，具体也不知道哪条起了作用。



# How To Fix System Program Problem Detected In Ubuntu

```
sudo gedit /etc/default/apport

Change the enabled=1 to enabled=0. Save and close the file. You won’t see any pop up for crash reports after doing this. Obvious to point out that if you want to enable the crash reports again, you just need to change the same file and put enabled as 1 again.

```



# 切换root用户

 ubuntu有以下方式切换到root身份：

1. sudo+命令，输入当前用户密码后以[root权限](https://www.baidu.com/s?wd=root权限&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1d-mHf3mHn4nW7hryDdujfv0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EnH0drjc4PjmY)执行命令，有时间限制且仅限当前命令。

2. sudo -i，输入当前用户密码后以[root权限](https://www.baidu.com/s?wd=root权限&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1d-mHf3mHn4nW7hryDdujfv0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EnH0drjc4PjmY)登录shell，无时间限制。使用exit或logout退出。

3. su，输入root账户的密码后切换到root身份，无时间限制。su 用户名切换回其它用户。

4. sudo su，效果同su，只是不需要root的密码，而需要当前用户的密码。



# 更改ubuntu语言设置

1.  如设置中文utf-8格式，添加第一个脚本文件，设置英文utf-8格式。添加第二个脚本文件

language_chinese.sh

```
export LANG="zh_CN.UTF-8"
export LANGUAGE="zh_CN.UTF-8"
export LC_CTYPE="zh_CN.UTF-8"
export LC_NUMERIC="zh_CN.UTF-8"
export LC_TIME="zh_CN.UTF-8"
export LC_COLLATE="zh_CN.UTF-8"
export LC_MONETARY="zh_CN.UTF-8"
export LC_MESSAGES="zh_CN.UTF-8"
export LC_PAPER="zh_CN.UTF-8"
export LC_NAME="zh_CN.UTF-8"
export LC_ADDRESS="zh_CN.UTF-8"
export LC_TELEPHONE="zh_CN.UTF-8"
export LC_MEASUREMENT="zh_CN.UTF-8"
export LC_IDENTIFICATION="zh_CN.UTF-8"
export LC_ALL=zh_CN.UTF-8
```

language_english.sh

```
export LANG="en_US.UTF-8"
export LANGUAGE="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
export LC_NUMERIC="en_US.UTF-8"
export LC_TIME="en_US.UTF-8"
export LC_COLLATE="en_US.UTF-8"
export LC_MONETARY="en_US.UTF-8"
export LC_MESSAGES="en_US.UTF-8"
export LC_PAPER="en_US.UTF-8"
export LC_NAME="en_US.UTF-8"
export LC_ADDRESS="en_US.UTF-8"
export LC_TELEPHONE="en_US.UTF-8"
export LC_MEASUREMENT="en_US.UTF-8"
export LC_IDENTIFICATION="en_US.UTF-8"
export LC_ALL=en_US.UTF-8
```



2. 将脚本移动到/etc/profile.d/目录下
3. 重新启动电脑

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

## 查看安装文件目录

```
dpkg -L packagename
```

dpkg -L +软件包的名字，可以知道这个软件包包含了哪些文件， 这个方法可以列出所有安装后留在系统里的文件

# linux常用命令

## 根据某一列去重

https://blog.csdn.net/github_36669230/article/details/64503589

sort -t $'\t' -k 3 -u filename

sort 排序命令
-t 指定分隔符为‘\t’
-k 指定第三列
-u 去重

sort的其他一些选项：
-r 降序排列
-o 把排序结果输出到源文件

sort默认是把结果输出到标准输出，所以需要用重定向才能将结果写入文件，形如
sort filename>newfile
如果将结果输出到原文件，用重定向相当于清空

-n 看为数字来比较

你有没有遇到过10比2小的情况。我反正遇到过。出现这种情况是由于排序程序将这些数字按字符来排序了，排序程序会先比较1和2，显然1小，所以就将10放在2前面喽。这也是sort的一贯作风。
我们如果想改变这种现状，就要使用-n选项，来告诉sort，“要以数值来排序”！

-f 会将小写字母都转换为大写字母来进行比较，亦即忽略大小写

-c 会检查文件是否已排好序，如果乱序，则输出第一个乱序的行的相关信息，最后返回1

-C 会检查文件是否已排好序，如果乱序，不输出内容，仅返回1

-M 会以月份来排序，比如JAN小于FEB等等

-b 会忽略每一行前面的所有空白部分，从第一个可见字符开始比较。

## 统计文件行数

https://www.cnblogs.com/fullhouse/archive/2011/07/17/2108786.html

wc [选项] 文件…

说明：该命令统计给定文件中的字节数、字数、行数。如果没有给出文件名，则从标准输入读取。wc同时也给出所有指定文件的总统计数。字是由空格字符区分开的最大字符串。

该命令各选项含义如下：

　　- c 统计字节数。

　　- l 统计行数。

　　- w 统计字数。

这些选项可以组合使用。

输出列的顺序和数目不受选项的顺序和数目的影响。

总是按下述顺序显示并且每项最多一列。

行数、字数、字节数、文件名

如果命令行中没有文件名，则输出中不出现文件名。

例如：

wc - lcw file1 file2

4 33 file1

7 52 file2

11 11 85 total

## 合并文件内容

https://blog.csdn.net/Alvin_Lam/article/details/79123882

将多个文件内容合并到一个文件

cat b1.sql b2.sql b3.sql > b_all.sql

或者

cat *.sql > merge.sql



## 清空回收站

```
sudo rm -rf ~/.local/share/Trash/*
```

## 查看动态库依赖性

```
ldd 动态库名字
```

## 把ldd查询到的所有需要的库导出

这里提供一个脚本将ldd打印出来的依赖库复制到指定路径：

```
#!/bin/sh

exe="test" #发布的程序名称
des="/home/hejianglin/QtProject/build-test-Desktop-Release/ReleaseTest" #你的路径

deplist=$(ldd $exe | awk  '{if (match($3,"/")){ printf("%s "),$3 } }')
cp $deplist $des
```

说明：exe ：要发布的程序名称 des：指定复制的路径 


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

ctrl+s进入假死状态

ctrl+q解除假死状态
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
   
   
   