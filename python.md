# Anaconda

![image-20210111223555957](https://i.loli.net/2021/01/11/Ti98hkxg4cMF7XS.png)

## 查看conda版本

```
conda --version
```



# Ipython

## 1 变量+？显示变量信息

![image-20210111223811852](https://i.loli.net/2021/01/11/9ACy3mXrQOhzdaW.png)

## 2 %run运行.py程序

![image-20210111223746780](https://i.loli.net/2021/01/11/qdI7UyFRazS4LMC.png)

## 3 ipython 魔术命令

![image-20210111223735306](https://i.loli.net/2021/01/11/IgwURvbeNpDmPMV.png)



# Python main函数

```python
def func():    
	print('hello, world!') 
if __name__ == "__main__":    
	func()
```

https://blog.csdn.net/weixin_35684521/article/details/81396434

# python 读写文件方法

## 1 python读取txt文件，并转为数字

文件内容如下：

<img src="https://i.loli.net/2020/12/13/BulxUPLAQK4zcsh.png" alt="image-20201213150855657" style="zoom: 50%;" />



代码如下：

```python
import sys

txtresult=[]

with open('testdata.txt','r') as f:
  for line in f:
    #去除文件每行的换行符后转为数字
​    txtresult.append(float(line.strip('\n')))

#打印文件内容
print(txtresult)
#打印列表长度
print(len(txtresult))
```





# python 字符串 使用方法

## 1 移除字符串头尾指定的字符

```python
str = "00000003210Runoob01230000000" 
print str.strip( '0' )  # 去除首尾字符 0  
str2 = "   Runoob      "   # 去除首尾空格 print str2.strip();
```

## 2 字符串切片

split() 通过指定分隔符对字符串进行切片，如果第二个参数 num 有指定值，则分割为 num+1 个子字符串。

### 语法

split() 方法语法：

```
str.split(str="", num=string.count(str))
```

### 参数

- str -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。
- num -- 分割次数。默认为 -1, 即分隔所有。

### 返回值

返回分割后的字符串列表。

### 实例

以下实例展示了 split() 函数的使用方法：

```python
str = "this is string example....wow!!!" 
print (str.split( ))       # 以空格为分隔符 
print (str.split('i',1))   # 以 i 为分隔符 
print (str.split('w'))     # 以 w 为分隔符
####################################输出结果##############################
['this', 'is', 'string', 'example....wow!!!']
['th', 's is string example....wow!!!']
['this is string example....', 'o', '!!!']
```



# python list 列表使用方法

## 1 获取列表最大值和最小值

```python
aa = [1,2,3,4,5]
#获取列表最大值
max(aa)
#获取列表最小值
min(aa)
#获取列表最大值的索引
aa.index(max(aa))
#获取列表最小值的索引
aa.index(min(aa))
```

## 2 获取list长度

```python
list1 = [1, 2, 3, 4, 5]
print(len(list1))  #5
```

## 3 列表循环获取下标

```python
#idx为下标，val为列表中的每一项值
for idx, val in enumerate(ints):
    print(idx, val)
```

# python 基础

## 1 条件判断

```python
age = 3
if age >= 18:
    print('your age is', age)
    print('adult')
else:
    print('your age is', age)
    print('teenager')
    
############################################

age = 3
if age >= 18:
    print('adult')
elif age >= 6:
    print('teenager')
else:
    print('kid')
```

# VSCode 开发python

## 1 安装插件

Chinese 汉化插件

Python 编写python插件

alt+shift+F格式化代码插件（autope8） 

2 开发Django项目

https://code.visualstudio.com/docs/python/tutorial-django

3 开发普通python项目

https://code.visualstudio.com/docs/python/python-tutorial



# VS设置python编译环境

在VS中添加python组件，注意默认为再次安装anacoda和python，如电脑上已经安装，可以取消组件

# Ubuntu下设置python默认版本为python3

```
update-alternatives --install /usr/bin/python python /usr/bin/python3 10
```





# 获取当前目录

```
import os
print os.getcwd()
```



# 删除指定文件夹下特定格式文件的方法

```python
import os
def del_files(path):
  for root , dirs, files in os.walk(path):
    for name in files:
      if name.endswith(".jpg"):   #指定要删除的格式，这里是jpg 可以换成其他格式
        os.remove(os.path.join(root, name))
        print ("Delete File: " + os.path.join(root, name))
# test
if __name__ == "__main__":
  path = '指定路径'
  del_files(path)
```

# 编译python源码（指定安装目录）

```
https://www.cnblogs.com/zoro-robin/p/5638774.html
```

1. 下载python源码（github或者官网）
2. 根据github上的步骤进行编译安装

