# VS设置python编译环境

在VS中添加python组件，注意默认为再次安装anacoda和python，如电脑上已经安装，可以取消组件

# Ubuntu下设置python默认版本为python3

```
update-alternatives --install /usr/bin/python python /usr/bin/python3 10
```



# if...else

```
var = False
if not var:
    print 'learnt stuff'
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

