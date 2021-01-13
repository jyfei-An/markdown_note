# 1 导入

```python
import  matplotlib.pyplot as plt
```

# 2 plot 函数

pIt. plot（x, y, format string,kwargs）

x:X轴数据，列表或数组，可选。

y:Y轴数据，列表或数组。

format string:控制曲线的格式字符串，可选，由颜色字符、风格字符和标记字符组成

```python
#‘r’:绘制一条红色线条，当第二个参数和第三个参数同时省略时，默认绘制直线
#'go-':绿色+实心圈标记+实线
#'rx'：红色+X标记+无线条，当第三个参数省略时，默认绘制散点图
#'b-'：蓝色+实线
```

**kwargs：第二组或更多（x,y, format string）

color：控制颜色， color='g' 

linestyle：线条风格， linestyle= ':' 

marker：标记风格， marker=‘o’ 

markerfacecolor：标记颜色， markerfacecolor=‘blue’

markersize：标记尺寸， markersize=20



注：当绘制多条曲线时，各条曲线的x不能省略。



# 3 绘制曲线

## 绘制一条曲线

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制一条曲线，可以省略x，x默认是数组的下标
plt.plot(a)
plt.show()
```

## 绘制多条曲线

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
plt.plot(a,a*2,a,a*4,a,a*6)
plt.show()
```

# 改变线条颜色

##  通过format_string改变

| 颜色字符  | 说明         |
| --------- | ------------ |
| ‘b’       | 蓝色         |
| 'g'       | 绿色         |
| 'r'       | 红色         |
| 'c'       | 青绿色       |
| '#008000' | RGB某颜色    |
| 'm'       | 洋红色       |
| 'y'       | 黄色         |
| 'k'       | 黑色         |
| 'w'       | 白色         |
| ‘0.8’     | 灰度值字符串 |



```
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制一条红色曲线
plt.plot(a,a*2,'r')
plt.show()
```



## 通过kwargs改变

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制一条绿色曲线
plt.plot(a,a*2,color='green')
plt.show()
```



# 改变曲线风格

## 通过format_string改变

![](https://i.loli.net/2021/01/13/tDkJBHusbGhU6R5.png)

```
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制一条红色虚线
plt.plot(a,a*2,'r:')
plt.show()
```

## 通过kwargs改变

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制一条虚线
plt.plot(a,a*2,linestyle=':')
plt.show()
```

# 改变曲线标记字符

## 通过format_string改变

![image-20210113075115977](https://i.loli.net/2021/01/13/ewpZLGzQHIUVFMc.png)

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#'go-':绿色+实心圈标记+实线
plt.plot(a,a*2,'go-')
plt.show()
```

## 通过kwargs改变

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')
plt.show()
```



# 设置坐标轴名称(xlabel)

## 英文名称

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

#设置横坐标轴名称
plt.xlabel('x value')
#设置纵坐标轴名称
plt.ylabel('y value')
plt.show()
```

## 中文名称

###  设置全局字体

pyplot井不默认支持中文显示，需要 rcParams修改字体实现。

![image-20210113085929850](https://i.loli.net/2021/01/13/2ndIZJREiLSFB9v.png)

![image-20210113085950915](https://i.loli.net/2021/01/13/Sh26CFNAxI3pEqb.png)



```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
import matplotlib

#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

matplotlib.rcParams['font.family'] = 'STSong'
matplotlib.rcParams['font.size'] = 20

#设置横坐标轴名称
plt.xlabel('横坐标轴')
#设置纵坐标轴名称
plt.ylabel('纵坐标轴')
plt.show()
```



### 设置坐标轴字体

在有中文输出的地方，增加一个属性：fontproperties

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

##设置坐标轴含义， 注：英文直接写，中文需要后面加上fontproperties属性
#设置横坐标轴名称
plt.xlabel(u'横坐标轴',fontproperties='SimHei',fontsize=50)
#设置纵坐标轴名称
plt.ylabel(u'纵坐标轴',fontproperties='SimHei',fontsize=20)
plt.show()
```



# 设置曲线标题名称(title)

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

##设置坐标轴含义， 注：英文直接写，中文需要后面加上fontproperties属性
#设置横坐标轴名称
plt.xlabel(u'横坐标轴',fontproperties='SimHei',fontsize=50)
#设置纵坐标轴名称
plt.ylabel(u'纵坐标轴',fontproperties='SimHei',fontsize=20)
#plt.title('title')
plt.title('标题',fontproperties='SimHei',fontsize=50)
plt.show()
```

# 在任意位置增加文本（text）

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

##设置坐标轴含义， 注：英文直接写，中文需要后面加上fontproperties属性
#设置横坐标轴名称
plt.xlabel(u'横坐标轴',fontproperties='SimHei',fontsize=50)
#设置纵坐标轴名称
plt.ylabel(u'纵坐标轴',fontproperties='SimHei',fontsize=20)
plt.title('标题',fontproperties='SimHei',fontsize=50)
#在坐标（2，1）位置绘制文本内容
plt.text(2,1,'test text',fontsize=15)
plt.show()
```

# 在图形中增加带箭头的注释（annotate）

plt.annotate（s, xy=arrow_crd, xytext=text_crd, arrowprops=dict）

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

##设置坐标轴含义， 注：英文直接写，中文需要后面加上fontproperties属性
#设置横坐标轴名称
plt.xlabel(u'横坐标轴',fontproperties='SimHei',fontsize=50)
#设置纵坐标轴名称
plt.ylabel(u'纵坐标轴',fontproperties='SimHei',fontsize=20)
plt.title('标题',fontproperties='SimHei',fontsize=50)
#在坐标（2，1）位置绘制文本内容
plt.text(2,1,'test text',fontsize=15)

#xy箭头位置坐标，xytext文本位置坐标，
plt.annotate('test annotate', xy=(3,1),
                xytext=(5,6),
                arrowprops=dict(facecolor='black', headwidth=4, 
                                width=2, headlength=4,shrink=0.1))
plt.show()
```



# 设置坐标轴范围（axis）

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

##设置坐标轴含义， 注：英文直接写，中文需要后面加上fontproperties属性
#设置横坐标轴名称
plt.xlabel(u'横坐标轴',fontproperties='SimHei',fontsize=50)
#设置纵坐标轴名称
plt.ylabel(u'纵坐标轴',fontproperties='SimHei',fontsize=20)
plt.title('标题',fontproperties='SimHei',fontsize=50)
#在坐标（2，1）位置绘制文本内容
plt.text(2,1,'test text',fontsize=15)

#xy箭头位置坐标，xytext文本位置坐标，
plt.annotate('test annotate', xy=(3,1),
                xytext=(5,6),
                arrowprops=dict(facecolor='black', headwidth=4, 
                                width=2, headlength=4,shrink=0.1))

#参数为一个数组，依次为x的左边界，x的右边界，y的下边界，y的上边界
plt.axis([-10,10,0,15])

plt.show()
```



# 设置坐标轴网格显示（grid）

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
#绘制多条曲线，每条曲线必须有x,y
#绿色+虚线+实心圆标记
plt.plot(a,a*2, color='g', linestyle= ':',marker='o')

##设置坐标轴含义， 注：英文直接写，中文需要后面加上fontproperties属性
#设置横坐标轴名称
plt.xlabel(u'横坐标轴',fontproperties='SimHei',fontsize=50)
#设置纵坐标轴名称
plt.ylabel(u'纵坐标轴',fontproperties='SimHei',fontsize=20)
plt.title('标题',fontproperties='SimHei',fontsize=50)
#在坐标（2，1）位置绘制文本内容
plt.text(2,1,'test text',fontsize=15)

#xy箭头位置坐标，xytext文本位置坐标，
plt.annotate('test annotate', xy=(3,1),
                xytext=(5,6),
                arrowprops=dict(facecolor='black', headwidth=4, 
                                width=2, headlength=4,shrink=0.1))

#参数为一个数组，依次为x的左边界，x的右边界，y的下边界，y的上边界
plt.axis([-10,10,0,15])

#设置坐标轴网格显示
plt.grid(True)

plt.show()
```

