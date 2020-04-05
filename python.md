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

