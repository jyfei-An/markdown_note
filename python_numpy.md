Numpy是一个用python实现的科学计算的扩展程序库，包括：

- 1、一个强大的N维数组对象Array；
- 2、比较成熟的（广播）函数库；
- 3、用于整合C/C++和Fortran代码的工具包；
- 4、实用的线性代数、傅里叶变换和随机数生成函数。numpy和稀疏矩阵运算包scipy配合使用更加方便。

NumPy（Numeric Python）提供了许多高级的数值编程工具，如：矩阵数据类型、矢量处理，以及精密的运算库。专为进行严格的数字处理而产生。多为很多大型金融公司使用，以及核心的科学计算组织如：Lawrence Livermore，NASA用其处理一些本来使用C++，Fortran或Matlab等所做的任务。

# CSV文件读取

## 一维CSV文件读取

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155229728-1347880001.png)

![(https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154650447-536657294.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154653905-243523839.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154700976-1918848712.png)

### 保存文件savetxt

```python
import numpy as np

a = np.arange(100).reshape(5,20)
np.savetxt('a.csv',a,fmt='%d',delimiter=',')
```

### 读取文件loadtxt

```
b=np.loadtxt('a.csv',delimiter=',')
b.shape
```



![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154724375-135027373.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154731275-763014628.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154735469-1408733135.png)





## 多维CSV文件读取

### 保存文件tofile

```
import numpy as np

a = np.arange(100).reshape(5,20)
#存储的文件中不包含任何维度信息
a.tofile('D:/b.dat',sep=',',format='%d')
```

```
import numpy as np

a = np.arange(100).reshape(5,20)
#不指定分隔符后，存储的文件为二进制文件，二进制文件会比文本文件占用更小的空间
a.tofile('D:/b.dat',sep='',format='%d')
```

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154740713-16800467.png)



### 读取文件fromfile

```
c=np.fromfile('D:/b.dat',dtype=int).reshape(5,20)
```

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154800143-329679379.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154829900-1423764316.png)

### 便捷文件存取save/load

存储文件

```python
import numpy as np

a = np.arange(100).reshape(5,20)
np.save('a.npy',a)
```



加载文件

```python
import numpy as np

a = np.arange(100).reshape(5,20)
np.save('a.npy',a)

b= np.load('a.npy')
#(5,20)
print(b.shape)
```



![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154840787-2000451776.png)

![img](https://i.loli.net/2021/01/16/adfLpG8X7kJtQ1D.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154829900-1423764316.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154834749-394575513.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154840787-2000451776.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154845426-1504447695.png)



## 注意

```
若是作为中间数据缓存，save和load是一种十分便捷的方法
若是与其他程序进行交互对接，CSV是一种不错的方法
```

## 参考资料

https://www.cnblogs.com/ssyfj/p/9291265.html#%E4%B8%80%EF%BC%9A%E6%95%B0%E6%8D%AE%E7%9A%84csv%E6%96%87%E4%BB%B6%E5%AD%98%E5%8F%96%E4%B8%80%E7%BB%B4%E6%88%96%E4%BA%8C%E7%BB%B4

# numpy随机数函数

![img](https://i.loli.net/2021/01/16/ov1GSZPzEXQwjBD.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154909887-1028229803.png)

## 均与分布（0，1）

![img](https://i.loli.net/2021/01/16/jv2lDMfhGLzVJZk.png)





## 标准正太分布

![img](https://i.loli.net/2021/01/16/s7SwVgBi4ejvyq9.png)

## 随机整数

![img](https://i.loli.net/2021/01/16/c3pwE4vUMu9aKnD.png)

![img](https://i.loli.net/2021/01/16/5S83qXDveM7grWP.png)

## 乱序数组

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112154949462-1021028478.png)
![img](https://i.loli.net/2021/01/16/9z2LkmbtRYZrI7O.png)

![img](https://i.loli.net/2021/01/16/qODys15CrQKhEJH.png)



![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180710192657652-1772400634.png)

注意：上面的概率是谁的数值越大，谁被抽取的概率越大



![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155011748-1884537475.png)

## 均匀分布数组（设置上下限）

![img](https://i.loli.net/2021/01/16/2JdhcWCOSbZm8pf.png)

## 正太分布数组（设置均值标准差）

![img](https://i.loli.net/2021/01/16/HfGX7P8bTZwMIYD.png)



## 参考资料

https://www.cnblogs.com/ssyfj/p/9291265.html#%E4%B8%80%EF%BC%9A%E6%95%B0%E6%8D%AE%E7%9A%84csv%E6%96%87%E4%BB%B6%E5%AD%98%E5%8F%96%E4%B8%80%E7%BB%B4%E6%88%96%E4%BA%8C%E7%BB%B4

# numpy中random的统计函数

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155253572-778561272.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155248450-85772522.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155243086-38666497.png)


![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155110100-505827727.png)

## 数组求和

![img](https://i.loli.net/2021/01/16/x9yY2UQeLsHmnib.png)

## 加权平均

![img](https://i.loli.net/2021/01/16/8o5lPVFDrQL9Yqk.png)


![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155131969-2025717557.png)

## 获取数组元素最大值

![img](https://i.loli.net/2021/01/16/2yDbWEiJ6nXwGtZ.png)

## 获取元素最大值下标

![](https://i.loli.net/2021/01/16/IsP4hprYQOHWdEM.png)

## 梯度函数

```
梯度：反应了元素的变化率，梯度有助于我们发现图像。声音的边缘，在那些不是很平滑的地方，我们能够很快的发现
```

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155213403-1722184397.png)

![img](https://i.loli.net/2021/01/16/13dQfWObgXGxym4.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180710201423991-42965212.png)

## 参考资料

https://www.cnblogs.com/ssyfj/p/9291265.html#%E4%B8%80%EF%BC%9A%E6%95%B0%E6%8D%AE%E7%9A%84csv%E6%96%87%E4%BB%B6%E5%AD%98%E5%8F%96%E4%B8%80%E7%BB%B4%E6%88%96%E4%BA%8C%E7%BB%B4



# 1.Numpy基本操作

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155604518-1979432601.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155640588-302628499.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155644572-750836774.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155653250-1415060589.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155657735-272093820.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155704686-1407975550.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155710089-1548297428.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155713375-1229729247.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112155716650-344416812.png)

## 1.1 列表转为矩阵

```python
import numpy as np
#np.array生成一个ndarray数组，ndarray再程序中的别名为array
#np.array()输出形式为[],元素之间由空格分隔
array = np.array([
    [1,3,5],
    [4,6,9]
])

print(array)
[[1 3 5]
 [4 6 9]]
```

## 1.2 维度

```python
print('number of dim:', array.ndim)
number of dim: 2
```

## 1.3 行数和列数()

```python
print('shape:',array.shape)
shape: (2, 3)
```

## 1.4 元素个数

```python
print('size:',array.size)
size: 6
```

## 1.5 ndarray对象的属性

| 属性      | 说明                                      |
| --------- | ----------------------------------------- |
| .ndim     | 秩，即轴的数量或者维度的数量              |
| .shape    | ndarray对象的尺度，对于矩阵，n行m列       |
| .size     | ndarray对象的个数，相当于.shape中n*m的值  |
| .dtype    | ndarray对象的元素类型                     |
| .itemsize | ndarray对象中每个元素的大小，以字节为单位 |

## 1.6 ndarray对象的元素类型

| 数据类型   | 说明                                                 |
| ---------- | ---------------------------------------------------- |
| bool       | 布尔类型，True或者False                              |
| intc       | 与C语言中int类型一致，一般是int32或者int64           |
| intp       | 用于于索引的整数，与C语言中 size_t一致，int32或int64 |
| int8       | 字节长度的整数，取值：[-128,127]                     |
| int16      | 16位长度的整数，取值：[-32768,32767]                 |
| int32      | 32位长度的整数，取值：[-2^31,2^31-1]                 |
| int64      | 64位长度的整数，取值：[-2^63,2^63-1]                 |
| uint8      | 8位无符号整数，取值：[0,255]                         |
| uint16     | 16位无符号整数，取值：[0,65535]                      |
| uint32     | 32位无符号整数，取值：[0,2^32-1]                     |
| uint64     | 64位无符号整数，取值：[0,2^64-1]                     |
| float16    | 16位半精度浮点数：1位符号位，5位指数，10位尾数       |
| float32    | 32位半精度浮点数：1位符号位，8位指数，23位尾数       |
| float64    | 64位半精度浮点数：1位符号位，11位指数，52位尾数      |
| complex64  | 复数类型，实部和虚部都是32位浮点数                   |
| complex128 | 复数类型，实部和虛部都是64位浮点数                   |



# 2.Numpy创建array

## 从列表类型创建数组

```
a = np.array([2,23,4]) 
```

## 从元组类型创建数组

```
a = np.array((2,23,4)) 
```

## 从列表和元组混合类型创建数组

```
a = np.array([2,23,4],[1,2,3],(4,5,6)) 
```

## 使用numpy中函数创建数组

| 函数                  | 说明                                            |
| --------------------- | ----------------------------------------------- |
| np. arange（n）       | 类似 range0函数，返回 ndarray类型，元素从0到n-1 |
| np.ones（ shape）     | 根据 shape生成一个全1数组， shape是元组类型     |
| np, zeros（ shape）   | 根据 shape生成一个全0数组， shape是元组类型     |
| np. full（shape,vaD） | 根据 shape生成一个数组，每个元素值都是val       |
| np. eye（n）          | 创建一个正方的n*n单位矩阵，对角线为1，其余为0   |
| np. ones_like（a）    | 根据数组a的形状生成一个全1数组                  |
| np.zeros_like（a）    | 根据数组a的形状生成一个全0数组                  |
| np. full_like（a,va） | 根据数组a的形状生成一个数组，每个元素值都是val  |
| np. linspaceO         | 根据起止数据等间距地填充数据，形成数组          |
| np. concatenate()     | 将两个或多个数组合井成一个新的数组              |

## ndarray数组的维度变换

| 说明                 | 方法                                                 |
| -------------------- | ---------------------------------------------------- |
| reshape（shape）     | 不改变数组元素，返回一个 shape形状的数组，原数组不变 |
| resize（shape）      | 与 reshape功能一致，但修改原数组                     |
| swapaxes（ax1，ax2） | 将数组n个维度中两个维度进行调换                      |
| flatten()            | 对数组进行降维，返回折叠后的一维数组，原数组不变     |

## ndarray数组的类型变换

```python
#astype方法一定会创建新的数组（原始数据的一个拷贝），即使两个类型一致。
new a=a. astype（new type）
```

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112152239342-418492174.png)

## ndarray数组向列表的转换
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112152306026-1683541509.png)


## 2.1 一维array创建

```python
import numpy as np
# 一维array
a = np.array([2,23,4], dtype=np.int32) # np.int默认为int32
print(a)
print(a.dtype)
===========================
[ 2 23  4]
int32
```

## 2.2 多维array创建

```python
# 多维array
a = np.array([[2,3,4],
              [3,4,5]])
print(a) # 生成2行3列的矩阵
==========================================
[[2 3 4]
 [3 4 5]]
```

## 2.3 创建全零数组(zeros)

```
a = np.zeros((3,4))
print(a) # 生成3行4列的全零矩阵
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
```

## 2.4 创建全1数据(ones)

In [8]:

```
# 创建全一数据，同时指定数据类型
a = np.ones((3,4),dtype=np.int)
print(a)
[[1 1 1 1]
 [1 1 1 1]
 [1 1 1 1]]
```

## 2.5 创建全空数组(empty)

In [9]:

```
# 创建全空数组，其实每个值都是接近于零的数
a = np.empty((3,4))
print(a)
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
```

## 2.6 创建连续数组(arange)

In [10]:

```
# 创建连续数组
a = np.arange(10,21,2) # 10-20的数据，步长为2
print(a)
[10 12 14 16 18 20]
```

## 2.7 reshape操作

In [11]:

```
# 使用reshape改变上述数据的形状
b = a.reshape((2,3))
print(b)
[[10 12 14]
 [16 18 20]]
```

## 2.8 创建连续型数据(linspcace)

```python
# 创建线段型数据
a = np.linspace(1,10,20) # 开始端1，结束端10，且分割成20个数据，生成线段
print(a)
[ 1.          1.47368421  1.94736842  2.42105263  2.89473684  3.36842105
  3.84210526  4.31578947  4.78947368  5.26315789  5.73684211  6.21052632
  6.68421053  7.15789474  7.63157895  8.10526316  8.57894737  9.05263158
  9.52631579 10.        ]
  
  #endpoint为false时，生成的数组不含结束端
  b= np linspace（l, 10， 4， endpoint=False）
  print(b)
  [1.,3.25,5.5,7.75]
```

## 2.9 linspace的reshape操作

In [13]:

```
# 同时也可以reshape
b = a.reshape((5,4))
print(b)
[[ 1.          1.47368421  1.94736842  2.42105263]
 [ 2.89473684  3.36842105  3.84210526  4.31578947]
 [ 4.78947368  5.26315789  5.73684211  6.21052632]
 [ 6.68421053  7.15789474  7.63157895  8.10526316]
 [ 8.57894737  9.05263158  9.52631579 10.        ]]
```

## 2.10 根据一个整数生成数组

np. full（shape,vaD）

根据 shape生成一个数组，每个元素值都是val

# 3.Numpy基本运算


## 数组与标量之间的运算
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153303390-1066869342.png)

## numpy一元函数
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153400904-2139331733.png)

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153408282-1047921320.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153413198-686279075.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153417663-1589651173.png)

## numpy二元函数
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153434882-95002202.png)
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153438876-2048729231.png)


## 3.1 一维矩阵运算

In [14]:

```
import numpy as np
# 一维矩阵运算
a = np.array([10,20,30,40])
b = np.arange(4)
print(a,b)
[10 20 30 40] [0 1 2 3]
```

In [15]:

```
c = a - b
print(c)
[10 19 28 37]
```

In [16]:

```
print(a*b) # 若用a.dot(b),则为各维之和
[  0  20  60 120]
```

In [17]:

```
# 在Numpy中，想要求出矩阵中各个元素的乘方需要依赖双星符号 **，以二次方举例，即：
c = b**2
print(c)
[0 1 4 9]
```

In [18]:

```
# Numpy中具有很多的数学函数工具
c = np.sin(a)
print(c)
[-0.54402111  0.91294525 -0.98803162  0.74511316]
```

In [19]:

```
print(b<2)
[ True  True False False]
```

In [20]:

```
a = np.array([1,1,4,3])
b = np.arange(4)
print(a==b)
[False  True False  True]
```

## 3.2 多维矩阵运算

In [21]:

```
a = np.array([[1,1],[0,1]])
b = np.arange(4).reshape((2,2))
print(a)
[[1 1]
 [0 1]]
```

In [22]:

```
print(b)
[[0 1]
 [2 3]]
```

In [23]:

```
# 多维度矩阵乘法
# 第一种乘法方式:
c = a.dot(b)
print(c)
[[2 4]
 [2 3]]
```

In [24]:

```
# 第二种乘法:
c = np.dot(a,b)
print(c)
[[2 4]
 [2 3]]
```

In [25]:

```
# 多维矩阵乘法不能直接使用'*'号

a = np.random.random((2,4))

print(np.sum(a))
3.825517216750851
```

In [26]:

```
print(np.min(a))
0.09623355767721398
```

In [27]:

```
print(np.max(a))
0.7420428188342583
```

In [28]:

```
print("a=",a)
a= [[0.48634962 0.74204282 0.09623356 0.69074812]
 [0.60218881 0.52734181 0.41434585 0.26626662]]
```

如果你需要对行或者列进行查找运算，

就需要在上述代码中为 axis 进行赋值。

当axis的值为0的时候，将会以列作为查找单元，

当axis的值为1的时候，将会以行作为查找单元。

In [29]:

```
print("sum=",np.sum(a,axis=1))
sum= [2.01537412 1.8101431 ]
```

In [30]:

```
print("min=",np.min(a,axis=0))
min= [0.48634962 0.52734181 0.09623356 0.26626662]
```

In [31]:

```
print("max=",np.max(a,axis=1))
max= [0.74204282 0.60218881]
```

## 3.3 基本计算

In [32]:

```
import numpy as np

A = np.arange(2,14).reshape((3,4))
print(A)
[[ 2  3  4  5]
 [ 6  7  8  9]
 [10 11 12 13]]
```

In [33]:

```
# 最小元素索引
print(np.argmin(A)) # 0
0
```

In [34]:

```
# 最大元素索引
print(np.argmax(A)) # 11
11
```

In [35]:

```
# 求整个矩阵的均值
print(np.mean(A)) # 7.5
7.5
```

In [36]:

```
print(np.average(A)) # 7.5
7.5
```

In [37]:

```
print(A.mean()) # 7.5
7.5
```

In [38]:

```
# 中位数
print(np.median(A)) # 7.5
7.5
```

In [39]:

```
# 累加
print(np.cumsum(A))
[ 2  5  9 14 20 27 35 44 54 65 77 90]
```

In [40]:

```
# 累差运算
B = np.array([[3,5,9],
              [4,8,10]])
print(np.diff(B))
[[2 4]
 [4 2]]
```

In [41]:

```
C = np.array([[0,5,9],
              [4,0,10]])
print(np.nonzero(B))
print(np.nonzero(C))
(array([0, 0, 0, 1, 1, 1], dtype=int64), array([0, 1, 2, 0, 1, 2], dtype=int64))
(array([0, 0, 1, 1], dtype=int64), array([1, 2, 0, 2], dtype=int64))
```

In [42]:

```
# 仿照列表排序
A = np.arange(14,2,-1).reshape((3,4)) # -1表示反向递减一个步长
print(A)
[[14 13 12 11]
 [10  9  8  7]
 [ 6  5  4  3]]
```

In [43]:

```
print(np.sort(A))
[[11 12 13 14]
 [ 7  8  9 10]
 [ 3  4  5  6]]
```

In [44]:

```
# 矩阵转置
print(np.transpose(A))
[[14 10  6]
 [13  9  5]
 [12  8  4]
 [11  7  3]]
```

In [45]:

```
print(A.T)
[[14 10  6]
 [13  9  5]
 [12  8  4]
 [11  7  3]]
```

In [46]:

```
print(A)
[[14 13 12 11]
 [10  9  8  7]
 [ 6  5  4  3]]
```

In [47]:

```
print(np.clip(A,5,9))
[[9 9 9 9]
 [9 9 8 7]
 [6 5 5 5]]
```

clip(Array,Array_min,Array_max)

将Array_min<X<Array_max X表示矩阵A中的数，如果满足上述关系，则原数不变。

否则，如果X<Array_min，则将矩阵中X变为Array_min;

如果X>Array_max，则将矩阵中X变为Array_max.



# 4.Numpy索引与切片
![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153138019-1378933608.png)

## 一维数组的索引

```python
x1 = np.arange(10)
#[0 1 2 3 4 5 6 7 8 9]
print(x1)
#0
print(x1[0])
#5
print(x1[5])
#9
print(x1[-1])
```



## 多维数组的索引

每个维度一个索引值，逗号分隔

```python
x2 = np.arange(20).reshape(2,10)
#[[ 0  1  2  3  4  5  6  7  8  9] [10 11 12 13 14 15 16 17 18 19]]
print(x2)
#11
print(x2[1, 1])
#11
print(x2[1][1])
```

![](https://i.loli.net/2021/01/16/dqHrZtjEPUIkh7s.png)

## 一维数组的切片

![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153113041-639532905.png)

```python
x1 = np.arange(10)
#[0 1 2 3 4 5 6 7 8 9]
print(x1)
#起始编号默认为0，步长默认为1
#[0 1 2]
print(x1[:3])
#终止编号默认为最后一个，步长默认为1
#[3 4 5 6 7 8 9]
print(x1[3:])
#步长为-1，倒序输出
#[9 8 7 6 5 4 3 2 1 0]
print(x1[::-1])
```



## 多维数组的切片



![](https://img2020.cnblogs.com/blog/1317399/202101/1317399-20210112153159196-936523627.png)

```python
x2 = np.arange(20).reshape(2,10)
#[[ 0  1  2  3  4  5  6  7  8  9] [10 11 12 13 14 15 16 17 18 19]]
print(x2)
#第一个维度选取第一行和第二行，第二个维度选取0，1，2列
#[[ 0  1  2] [10 11 12]]
print(x2[:2, :3])
#第一个维度选取第一行和第二行，第二个维度选取0，2列
#[[ 0  2] [10 12]]
print(x2[:2, 0:3:2]) 
#选取全部，行列倒序输出
print(x2[::-1, ::-1])

#获取第一行元素[10 11 12 13 14 15 16 17 18 19]
print(x2[1, :])

#获取第二列元素[ 2 12]
print(x2[:,2])
```

## 打印每一行元素

```
for row in B:
    print(row)
[3 4 5 6]
[ 7  8  9 10]
[11 12 13 14]
```

## 打印每一列元素

```
# 如果要打印列，则进行转置即可
for column in B.T:
    print(column)
[ 3  7 11]
[ 4  8 12]
[ 5  9 13]
[ 6 10 14]
```

## 打印每一个元素

```
for item in A.flat:
    print(item)
3
4
5
6
7
8
9
10
11
12
13
14
```



## 多维转一维

### ravel函数

```python
A = np.arange(3,15).reshape((3,4))
print(A)
#ravel不会产生源数据的副本，对B的修改同时影响原数组
B=A.ravel()
print(B)
B[0]=100
print(B)
print(A)
```



### flatten函数

```python
A = np.arange(3,15).reshape((3,4))
print(A)
#flatten返回源数据的副本,对副本的修改不会影响原数组
B=A.flatten()
print(B)
B[0]=100
print(B)
print(A)
```

### reshape(-1)函数

```python
A = np.arange(3,15).reshape((3,4))
print(A)
#reshape不会产生源数据的副本，对B的修改同时影响原数组
B=A.reshape(-1)
print(B)
B[0]=100
print(B)
print(A)
```



#  5.Numpy array合并

## 5.1 数组合并

### 上下合并vstack

```python
import numpy as np
A = np.array([[1,1,1],[2,3,4]])
B = np.array([2,2,2])
#要求两个数组有相同的列
print(np.vstack((A,B)))
# vertical stack 上下合并,对括号的两个整体操作。
[[1 1 1]
 [2 2 2]]
```

### 水平合并hstack

```python
import numpy as np
A = np.array([[1,1,1],[2,3,4]])
B = np.array([[2,2,2],[3,3,3]])
#要求两个数字有相同的行
print(np.hstack((A,B)))
```

### 上下合并r_

```python
import numpy as np
A = np.array([[1,1,1],[2,3,4]])
B = np.array([2,2,2]).reshape(1,3)
#要求两个数组有相同的列
print(np.r_[A,B])
```

### 水平合并c_

```python
import numpy as np
A = np.array([[1,1,1],[2,3,4]])
B = np.array([[2,2],[3,3]])
#要求两个数字有相同的行
print(np.c_[A,B])
```



### 维度降维squeeze

```python
import numpy as np

a  = np.arange(10).reshape(1,10)
#(1, 10)
print(a.shape)
#将shape中为1的维度去掉
b = np.squeeze(a)
#(1, 10)
print(b.shape)

a  = np.arange(10).reshape(5,2,1)
#(1, 10)
print(a.shape)
#将shape中为1的维度去掉
b = np.squeeze(a)
#(1, 10)
print(b.shape)
```



## 5.2 数组转置为矩阵

In [64]:

```
print(A[np.newaxis,:]) # [1 1 1]变为[[1 1 1]]
[[1 1 1]]
```

In [65]:

```
print(A[np.newaxis,:].shape) # (3,)变为(1, 3)
(1, 3)
```

In [66]:

```
print(A[:,np.newaxis])
[[1]
 [1]
 [1]]
```

## 5.3 多个矩阵合并

In [67]:

```
# concatenate的第一个例子
print("------------")
print(A[:,np.newaxis].shape) # (3,1)
------------
(3, 1)
```

In [68]:

```
A = A[:,np.newaxis] # 数组转为矩阵
B = B[:,np.newaxis] # 数组转为矩阵
```

In [69]:

```
print(A)
[[1]
 [1]
 [1]]
```

In [70]:

```
print(B)
[[2]
 [2]
 [2]]
```

In [71]:

```
# axis=0纵向合并
C = np.concatenate((A,B,B,A),axis=0)
print(C)
[[1]
 [1]
 [1]
 [2]
 [2]
 [2]
 [2]
 [2]
 [2]
 [1]
 [1]
 [1]]
```

In [72]:

```
# axis=1横向合并
C = np.concatenate((A,B),axis=1)
print(C)
[[1 2]
 [1 2]
 [1 2]]
```

## 5.4 合并例子2

In [73]:

```
# concatenate的第二个例子
print("-------------")
a = np.arange(8).reshape(2,4)
b = np.arange(8).reshape(2,4)
print(a)
print(b)
print("-------------")
-------------
[[0 1 2 3]
 [4 5 6 7]]
[[0 1 2 3]
 [4 5 6 7]]
-------------
```

In [74]:

```
# axis=0多个矩阵纵向合并
c = np.concatenate((a,b),axis=0)
print(c)
[[0 1 2 3]
 [4 5 6 7]
 [0 1 2 3]
 [4 5 6 7]]
```

In [75]:

```
# axis=1多个矩阵横向合并
c = np.concatenate((a,b),axis=1)
print(c)
[[0 1 2 3 0 1 2 3]
 [4 5 6 7 4 5 6 7]]
```

# 6.Numpy array分割

## 6.1 构造3行4列矩阵

In [76]:

```
import numpy as np
A = np.arange(12).reshape((3,4))
print(A)
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

6.2 等量分割

In [77]:

```
# 等量分割
# 纵向分割同横向合并的axis
print(np.split(A, 2, axis=1))
[array([[0, 1],
       [4, 5],
       [8, 9]]), array([[ 2,  3],
       [ 6,  7],
       [10, 11]])]
```

In [78]:

```
# 横向分割同纵向合并的axis
print(np.split(A,3,axis=0))
[array([[0, 1, 2, 3]]), array([[4, 5, 6, 7]]), array([[ 8,  9, 10, 11]])]
```

## 6.3 不等量分割

In [79]:

```
print(np.array_split(A,3,axis=1))
[array([[0, 1],
       [4, 5],
       [8, 9]]), array([[ 2],
       [ 6],
       [10]]), array([[ 3],
       [ 7],
       [11]])]
```

## 6.4 其他的分割方式

In [80]:

```
# 横向分割
print(np.vsplit(A,3)) # 等价于print(np.split(A,3,axis=0))
[array([[0, 1, 2, 3]]), array([[4, 5, 6, 7]]), array([[ 8,  9, 10, 11]])]
```

In [81]:

```
# 纵向分割
print(np.hsplit(A,2)) # 等价于print(np.split(A,2,axis=1))
[array([[0, 1],
       [4, 5],
       [8, 9]]), array([[ 2,  3],
       [ 6,  7],
       [10, 11]])]
```

# 7.Numpy copy与 =

## 7.1 =赋值方式会带有关联性

In [82]:

```
import numpy as np
# `=`赋值方式会带有关联性
a = np.arange(4)
print(a) # [0 1 2 3]
[0 1 2 3]
```

In [83]:

```
b = a
c = a
d = b
a[0] = 11
print(a) # [11  1  2  3]
[11  1  2  3]
```

In [84]:

```
print(b) # [11  1  2  3]
[11  1  2  3]
```

In [85]:

```
print(c) # [11  1  2  3]
[11  1  2  3]
```

In [86]:

```
print(d) # [11  1  2  3]
[11  1  2  3]
```

In [87]:

```
print(b is a) # True
True
```

In [88]:

```
print(c is a) # True
True
```

In [89]:

```
print(d is a) # True
True
```

In [90]:

```
d[1:3] = [22,33]
print(a) # [11 22 33  3]
[11 22 33  3]
```

In [91]:

```
print(b) # [11 22 33  3]
[11 22 33  3]
```

In [92]:

```
print(c) # [11 22 33  3]
[11 22 33  3]
```

## 7.2 copy()赋值方式没有关联性

In [93]:

```
a = np.arange(4)
print(a) # [0 1 2 3]
[0 1 2 3]
```

In [94]:

```
b =a.copy() # deep copy
print(b) # [0 1 2 3]
[0 1 2 3]
```

In [95]:

```
a[3] = 44
print(a) # [ 0  1  2 44]
print(b) # [0 1 2 3]

# 此时a与b已经没有关联
[ 0  1  2 44]
[0 1 2 3]
```

# 8.广播机制

numpy数组间的基础运算是一对一，也就是`a.shape==b.shape`，但是当两者不一样的时候，就会自动触发广播机制，如下例子：

In [96]:

```
from numpy import array
a = array([[ 0, 0, 0],
           [10,10,10],
           [20,20,20],
           [30,30,30]])
b = array([0,1,2])
print(a+b)
[[ 0  1  2]
 [10 11 12]
 [20 21 22]
 [30 31 32]]
```

为什么是这个样子？

这里以tile模拟上述操作，来回到`a.shape==b.shape`情况！

In [97]:

```
# 对[0,1,2]行重复3次，列重复1次
b = np.tile([0,1,2],(4,1))
print(a+b)
[[ 0  1  2]
 [10 11 12]
 [20 21 22]
 [30 31 32]]
```

到这里，我们来给出一张图

![img](https://github.com/fengdu78/Data-Science-Notes/raw/931f533bcc16ac3ce5db24f956bacb61b8a827f5/2.numpy/images/3.png)

也可以看这张图：![img](https://github.com/fengdu78/Data-Science-Notes/raw/931f533bcc16ac3ce5db24f956bacb61b8a827f5/2.numpy/images/4.png)

是不是任何情况都可以呢？

当然不是，只有当两个数组的`trailing dimensions  compatible`时才会触发广播，否则报错`ValueError: frames are not aligned exception`。

上面表达意思是尾部维度必须兼容！



# .常用函数

## 9.1 np.bincount()

In [98]:

```
x = np.array([1, 2, 3, 3, 0, 1, 4])
np.bincount(x)
```

Out[98]:

```
array([1, 2, 1, 2, 1], dtype=int64)
```

统计索引出现次数：索引0出现1次，1出现2次，2出现1次，3出现2次，4出现1次

因此通过bincount计算出索引出现次数如下：

上面怎么得到的？

对于bincount计算吗，bin的数量比x中最大数多1，例如x最大为4，那么bin数量为5(index从0到4)，也就会bincount输出的一维数组为5个数，bincount中的数又代表什么？代表的是它的索引值在x中出现的次数！

还是以上述x为例子，当我们设置weights参数时候，结果又是什么？

这里假定：

In [99]:

```
w = np.array([0.3,0.5,0.7,0.6,0.1,-0.9,1])
```

那么设置这个w权重后，结果为多少？

In [100]:

```
np.bincount(x,weights=w)
```

Out[100]:

```
array([ 0.1, -0.6,  0.5,  1.3,  1. ])
```

怎么计算的？

先对x与w抽取出来：

```
x --->  [1, 2, 3, 3, 0, 1, 4]
```

`w --->  [0.3,0.5,0.7,0.6,0.1,-0.9,1]` 索引 0 出现在x中index=4位置，那么在w中访问index=4的位置即可，w[4]=0.1

索引 1 出现在x中index=0与index=5位置，那么在w中访问`index=0`与`index=5`的位置即可，然后将两这个加和，计算得：`w[0]+w[5]=-0.6` 其余的按照上面的方法即可！

bincount的另外一个参数为minlength，这个参数简单，可以这么理解，当所给的bin数量多于实际从x中得到的bin数量后，后面没有访问到的设置为0即可。

还是上述x为例：

这里我们直接设置minlength=7参数，并输出！

In [101]:

```
np.bincount(x,weights=w,minlength=7)
```

Out[101]:

```
array([ 0.1, -0.6,  0.5,  1.3,  1. ,  0. ,  0. ])
```

与上面相比多了两个0，这两个怎么会多？

上面知道，这个bin数量为5，index从0到4，那么当minlength为7的时候，也就是总长为7，index从0到6，多了后面两位，直接补位为0即可！

## 9.2 np.argmax()

函数原型为：`numpy.argmax(a, axis=None, out=None)`.

函数表示返回沿轴axis最大值的索引。

In [102]:

```
x = [[1,3,3],
     [7,5,2]]
print(np.argmax(x))
3
```

对于这个例子我们知道，7最大，索引位置为3(这个索引按照递增顺序)！

axis属性

axis=0表示按列操作，也就是对比当前列，找出最大值的索引！

In [103]:

```
x = [[1,3,3],
     [7,5,2]]
print(np.argmax(x,axis=0))
[1 1 0]
```

axis=1表示按行操作，也就是对比当前行，找出最大值的索引！

In [104]:

```
x = [[1,3,3],
     [7,5,2]]
print(np.argmax(x,axis=0))
[1 1 0]
```

那如果碰到重复最大元素？

返回第一个最大值索引即可！

例如：

In [105]:

```
x = np.array([1, 3, 2, 3, 0, 1, 0])
print(x.argmax())
1
```

## 9.3 上述合并实例

这里来融合上述两个函数，举个例子：

In [106]:

```
x = np.array([1, 2, 3, 3, 0, 1, 4])
print(np.argmax(np.bincount(x)))
1
```

最终结果为1，为什么？

首先通过`np.bincount(x)`得到的结果是：`[1 2 1 2 1]`，再根据最后的遇到重复最大值项，则返回第一个最大值的index即可！2的index为1，所以返回1。

## 9.4 求取精度

In [107]:

```
np.around([-0.6,1.2798,2.357,9.67,13], decimals=0)#取指定位置的精度
```

Out[107]:

```
array([-1.,  1.,  2., 10., 13.])
```

看到没，负数进位取绝对值大的！

In [108]:

```
np.around([1.2798,2.357,9.67,13], decimals=1)
```

Out[108]:

```
array([ 1.3,  2.4,  9.7, 13. ])
```

In [109]:

```
np.around([1.2798,2.357,9.67,13], decimals=2)
```

Out[109]:

```
array([ 1.28,  2.36,  9.67, 13.  ])
```

从上面可以看出，decimals表示指定保留有效数的位数，当超过5就会进位(此时包含5)！

但是，如果这个参数设置为负数，又表示什么？

In [110]:

```
np.around([1,2,5,6,56], decimals=-1)
```

Out[110]:

```
array([ 0,  0,  0, 10, 60])
```

发现没，当超过5时候(不包含5)，才会进位！-1表示看一位数进位即可，那么如果改为-2呢，那就得看两位！

In [111]:

```
np.around([1,2,5,50,56,190], decimals=-2)
```

Out[111]:

```
array([  0,   0,   0,   0, 100, 200])
```

看到没，必须看两位，超过50才会进位，190的话，就看后面两位，后两位90超过50，进位，那么为200！

计算沿指定轴第N维的离散差值

In [112]:

```
x = np.arange(1 , 16).reshape((3 , 5))
print(x)
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]]
```

In [113]:

```
np.diff(x,axis=1) #默认axis=1
```

Out[113]:

```
array([[1, 1, 1, 1],
       [1, 1, 1, 1],
       [1, 1, 1, 1]])
```

In [114]:

```
np.diff(x,axis=0)
```

Out[114]:

```
array([[5, 5, 5, 5, 5],
       [5, 5, 5, 5, 5]])
```

## 取整

In [115]:

```
np.floor([-0.6,-1.4,-0.1,-1.8,0,1.4,1.7])
```

Out[115]:

```
array([-1., -2., -1., -2.,  0.,  1.,  1.])
```

看到没，负数取整，跟上述的around一样，是向左！

## 取上限

In [116]:

```
np.ceil([1.2,1.5,1.8,2.1,2.0,-0.5,-0.6,-0.3])
```

Out[116]:

```
array([ 2.,  2.,  2.,  3.,  2., -0., -0., -0.])
```

取上限！找这个小数的最大整数即可！

## 查找

利用np.where实现小于0的值用0填充吗，大于0的数不变！

In [117]:

```
x = np.array([[1, 0],
       [2, -2],
     [-2, 1]])
print(x)
[[ 1  0]
 [ 2 -2]
 [-2  1]]
```

In [118]:

```
np.where(x>0,x,0)
```

Out[118]:
array([[1, 0],
       [2, 0],
       [0, 1]])  





# 网格点坐标矩阵meshgrid

## 二维坐标矩阵

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.array([[0, 1, 2], [0, 1, 2]])
y = np.array([[0, 0, 0], [1, 1, 1]])

#给matplotlib的坐标信息是矩阵也是可以的，只要横纵坐标的尺寸一样。都会按照对应关系生成点。
plt.plot(x, y,
         color='red',  # 全部点设置为红色
         marker='.',  # 点的形状为圆点
         linestyle='')  # 线型为空，也即点与点之间不用线连接
plt.grid(True)
plt.show()
```

![这里写图片描述](https://i.loli.net/2021/01/17/OLyGlzE9d6kaFRS.png)

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0,1000,20)
y = np.linspace(0,500,18)

#X矩阵的每一行都相同，共有18行
#Y矩阵的每一列都相同，共有20列
X,Y = np.meshgrid(x, y)
"""
>>> X, Y = np.meshgrid([1,2,3], [4,5,6,7])
>>> X
array([[1, 2, 3],
       [1, 2, 3],
       [1, 2, 3],
       [1, 2, 3]])
>>> Y
array([[4, 4, 4],
       [5, 5, 5],
       [6, 6, 6],
       [7, 7, 7]])
"""

#(18, 20)
print(X.shape)
#(18, 20)
print(Y.shape)

plt.plot(X, Y,
         color='limegreen',  # 设置颜色为limegreen
         marker='.',  # 设置点类型为圆点
         linestyle='')  # 设置线型为空，也即没有线连接点
plt.grid(True)
plt.show()
```

![image-20210117215630031](https://i.loli.net/2021/01/17/n8qCAKxX1YWJT3F.png)

参考资料：https://blog.csdn.net/lllxxq141592654/article/details/81532855

## 三维坐标矩阵

```python
import numpy as np

x_ = np.linspace(0., 1., 10)
y_ = np.linspace(1., 2., 20)
z_ = np.linspace(3., 4., 30)

x, y, z = np.meshgrid(x_, y_, z_, indexing='ij')

assert np.all(x[:,0,0] == x_)
assert np.all(y[0,:,0] == y_)
assert np.all(z[0,0,:] == z_)
#(10, 20, 30)
print(x.shape)
```