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



# python list 使用方法

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

