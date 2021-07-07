文字版本：https://cloud.tencent.com/developer/news/619121

https://blog.csdn.net/DTRblank/article/details/106586653

# 一：Pandas库的介绍

## 导入

```python
import pandas as pd
```

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711154905373-1891857829.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711155159834-1577416892.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711155608607-1661279375.png)

# 二：Pandas库的Series类型

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711155739215-1705628390.png)

## 索引

### 自动索引

```python
import pandas as pd
#自动增加索引，（0，1，2，3，4）
s = pd.Series([1,3,5,7,9])
print(s)
```



### 自定义索引

 import pandas as pd
#自定义索引索，['a','b','c','d','e']，索引数量必须和值列表数量相同
s = pd.Series([1,3,5,7,9],index=['a','b','c','d','e'])
print(s)

## Series类型创建

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711160241966-948469211.png)

### 列表创建

```python
import pandas as pd
#自动增加索引，（0，1，2，3，4）
s = pd.Series([1,3,5,7,9])
print(s)
```



### 标量值创建

```python
import pandas as pd
#使用标量创建，['a','b','c','d','e']，不能省略index，否则将创建一个
s = pd.Series(25,index=['a','b','c','d','e'])
#s = pd.Series(25)
print(s)
```



### 字典类型创建

```python
import pandas as pd
#使用字典创建，默认将字典键作为索引
#s = pd.Series({'a':9,'b':7})
#使用字典创建，若index存在，存在对应关系
s = pd.Series({'a':9,'b':7,'t':12},index=['a','b','c','d','e'])
print(s)

out:
a    9.0
b    7.0
c    NaN
d    NaN
e    NaN
dtype: float64
```



###  从ndarray类型创建

```python
import pandas as pd
import numpy as np
#s = pd.Series(np.arange(5))
s = pd.Series(np.arange(5),index=np.arange(9,4,-1))
print(s)
```



![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711161703928-420845804.png)

## 基本操作

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711161759363-833832375.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711162120994-497854448.png)

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165138799-1971064582.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165215470-1385553494.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165312078-1175176309.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165448969-995273809.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165555707-1891707212.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165655410-37849249.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165736172-1271637131.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711165805244-1411921444.png)

# 三：Pandas库的DataFrame类型

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711182750049-117176372.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711182848473-973144950.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711182901246-502150376.png)

## （一）DataFrame创建

### （1）ndarray创建

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711183051146-953135844.png)

### （2）字典创建（值为Series类型）

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711185420990-3785616.png)

### （3）字典创建（值为列表类型）字典键都是列索引，行索引是自带或者我们使用index创建的

![img](https://i.loli.net/2021/01/17/3OtkbqJhc4mgLpN.png)

### 删除行/删除满足条件的行

https://www.geeksforgeeks.org/drop-rows-from-the-dataframe-based-on-certain-condition-applied-on-a-column/

当元素是list或者是其他复杂元素时，可使用map函数，具体可参考

https://zhuanlan.zhihu.com/p/100064394

### 当元素是list时，删除满足元素的list

def listtoint_map(x):
    return x[0]

#将列表转为int（列表中只有一个值），否则没办法直接和0比较
test_data["key"] = human_test_data["key"].map(listtoint_map)

test_data1 = test_data()
test_data2 = test_data()

==============================


data1 = test_data1.drop(test_data1[test_data1['key']<0].index)

Data2 = test_data2.drop(test_data2[test_data2['key']>=0].index)

==================================

#将int转为list，和原始特征值的格式相同
def inttolist_map(x):
    data = []
    data.append(x)
    return data

data1["key"] = data1["key"].map(inttolist_map)
data2["key"] = data2["key"].map(inttolist_map)

=================================

data1.to_pickle("./data1.pkl")
data2.to_pickle("./data2.pkl")



## （二）案例使用

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711190539780-1229352807.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711192041942-87658980.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711192253869-1219273255.png)

![img](https://i.loli.net/2021/01/17/wYr3ACP6mlbhWSj.png)

# 四：Pandas库的数据类型操作

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711192446944-459596870.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711192530126-606359647.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711192807341-18228709.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711193009216-896929990.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711202250306-1550542609.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711203919590-1690156305.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711204100317-598592942.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711204310278-427765683.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711202352426-509065677.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711203339547-1721345131.png)

#  五：Pandas库的数据类型运算

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711204557510-949141554.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711204910308-11425717.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711204956314-1368012572.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711205130648-1025766802.png)

## 不同维度的运算Series和DataFrame（为广播运算）

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711210116826-1850153128.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711210218337-784138153.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711210303503-168718208.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711210731832-1508778635.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711211110983-85148797.png)

# 总结

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711211239098-698518657.png)

 

> [说明：0轴axis=0和1轴axis=1](https://www.cnblogs.com/ssyfj/p/9297263.html#说明：0轴axis=0和1轴axis=1)
> [简介](https://www.cnblogs.com/ssyfj/p/9297263.html#简介)
> [一：数据的排序](https://www.cnblogs.com/ssyfj/p/9297263.html#一：数据的排序)
> [二：数据的基本统计分析](https://www.cnblogs.com/ssyfj/p/9297263.html#二：数据的基本统计分析)
> [三：数据的累积统计分析](https://www.cnblogs.com/ssyfj/p/9297263.html#三：数据的累积统计分析)
> [四：数据的相关分析](https://www.cnblogs.com/ssyfj/p/9297263.html#四：数据的相关分析)
> [ ](https://www.cnblogs.com/ssyfj/p/9297263.html# )
> [一：数据的排序](https://www.cnblogs.com/ssyfj/p/9297263.html#一：数据的排序)
> [二：数据的基本统计分析](https://www.cnblogs.com/ssyfj/p/9297263.html#二：数据的基本统计分析)
> [三：数据的累积统计分析](https://www.cnblogs.com/ssyfj/p/9297263.html#三：数据的累积统计分析)
> [四：数据的相关分析](https://www.cnblogs.com/ssyfj/p/9297263.html#四：数据的相关分析)
> [总结](https://www.cnblogs.com/ssyfj/p/9297263.html#总结)

# 说明：0轴axis=0和1轴axis=1

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711212206238-1055636702.png)

# 简介

# 一：数据的排序

# 二：数据的基本统计分析

# 三：数据的累积统计分析

# 四：数据的相关分析

------

#  

# 一：数据的排序

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711211721468-65537024.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711211815209-1862653983.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711211943659-902704375.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711212302628-112439428.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711212356187-495722637.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711212501937-1839072729.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711213301536-345948215.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711224416096-1845620204.png)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
    0   1   2   3   4
a   0   1   2   3   4
b   5   6   7   8   9
c  10  11  12  13  14
d  15  16  17  18  19
```

------

```
    4   3   2   1   0
a   4   3   2   1   0
b   9   8   7   6   5
c  14  13  12  11  10
d  19  18  17  16  15
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711224531706-241375313.png)

# 二：数据的基本统计分析

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711224708421-1967676523.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711224732840-1797780443.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711224811918-1961873125.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711224934465-893882144.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711225249513-684645473.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711225026256-757693270.png)

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711225419811-956148830.png)

# 三：数据的累积统计分析

```
累积统计分析：是能够对数据中的前1-n个数，进行累积运算，在一些大量数据分析中，可以减少for循环的使用，使得数据的运算更加灵活
```

 ![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711225652303-166605176.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711225906335-1679006806.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711230001473-660402123.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711231134635-89670042.png)

# 四：数据的相关分析

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711231330185-1480781812.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711231403980-629056507.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711231523359-242592335.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711231543196-1357717853.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711231955919-448157702.png)

# 总结

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711232048149-523432938.png)

 



# 参考资料

https://www.cnblogs.com/ssyfj/p/9297263.html