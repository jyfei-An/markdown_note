# 设置软件更新源

在terminal输入下面命令，弹出设置框，选择阿里云源

```
software-properties-gtk
```



# vi按上下左右键为字母解决办法

```
sudo apt-get remove vim-common
sudo apt-get install vim
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
   
   
   
   ## 