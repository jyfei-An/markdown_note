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



![image-20210111223555957](https://i.loli.net/2021/01/11/Ti98hkxg4cMF7XS.png)

查看conda版本

```
conda --version
```



# Jupyter Notebook快捷键

Alt-Enter : 运行本单元，在其下插入新单元

```
https://blog.csdn.net/lawme/article/details/51034543
```



## 安装自动补全功能

1 打开anaconda，选择环境，选择open Terminal,输入下面命令进行安装（不要使用网络代理，否则会安装失败）
 1) pip install jupyter_contrib_nbextensions
 2) pip install jupyter_nbextensions_configurator
 3) jupyter contrib nbextension install --user 
 4) jupyter nbextensions_configurator enable --user

2 打开jupyter notebook

1)click on nbextensions tab

2)unckeck disable configuration for nbextensions without explicit compatibility

3)put a check on Hinterland

3 打开新文件，使用自动补全功能



# Jupyter

音标:/ˈdʒuːpɪtə(r)/

朱批特儿

## 1 显示左边markdown目录

### （1）安装Jupyter Notebook extensions

打开anaconda，选择base环境，右键open terminal，执行下面命令

（当存在多个python环境时，安装Jupyter-plugins选择base即可，其他环境的jupyter也会进行同步）

```text
conda install -c conda-forge jupyter_contrib_nbextensions
```

### （2）打开jupyter，选择Nbextensions

![image-20210619110041930](https://i.loli.net/2021/06/19/vqeJHgRzCrWSFab.png)

### (3)选择table_of_counts插件

![image-20210619110125258](https://i.loli.net/2021/06/19/u5d2h4NFGoylVQR.png)

### （4）勾选后退出当前界面，重新打开想要显示目录的文件

### （5）点击下图中的按钮，显示markdown目录

![image-20210619110257518](https://i.loli.net/2021/06/19/gA26O7uaNQcIR4V.png)