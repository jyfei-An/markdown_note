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



# 3 绘制折线图

## 绘制一条折线

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

## 绘制多条折线

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



# 绘制散点图

## 通过plot函数

```python
import numpy as np
import matplotlib.pyplot as plt

ax = plt.subplot()
#曲线格式为实心圆标记+无线条
ax.plot(10*np.random.randn(100),10*np.random.randn(100),'o-')
ax.set_title("Simple Scatter")

plt.show()
```

## 通过scatter函数

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np
#创建连续数组（0-0）
a = np.arange(10)
b = np.arange(10)
#s参数表示绘制图形时使用的点的尺寸
plt.scatter(a,b,s=500)
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



# 设置坐标轴范围

## 1 axis函数

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

## 2 xlim函数

```
plt.xlim((-1,2))#设置x轴范围
plt.ylim((-2,3))#设置轴y范围
```

```
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
#plt.axis([-10,10,0,15])

plt.xlim((-1,10))#设置x轴范围
plt.ylim((-2,10))#设置轴y范围

#设置坐标轴网格显示
plt.grid(True)

plt.show()
```



# 设置坐标轴显示刻度

## xticks  yticks 函数

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
#plt.axis([-10,10,0,15])

plt.xlim((-1,10))#设置x轴范围
plt.ylim((-2,10))#设置轴y范围

# 设置x轴刻度

# -1到2区间，5个点，4个区间，平均分：[-1.,-0.25,0.5,1.25,2.]

new_ticks=np.linspace(-1,20,5)
print(new_ticks)


#设置x轴，Y轴刻度,刻度可现实字符串
plt.xticks(new_ticks)
#plt.yticks([-2,-1.8,-1,1.22,3.], ['非常糟糕','糟糕',r'$good\ \alpha$',r'$really\ good$','超级好'],fontproperties='SimHei')
plt.yticks([-2,-1.8,-1,1.22,20.])


#设置坐标轴网格显示
plt.grid(True)

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



# 设置图例

## plot函数label设置图例

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np


fig = plt.figure();
ax = fig.add_subplot(1, 1, 1)
#创建连续数组（0-0）
a = np.arange(10)

#绘制多条曲线，每条曲线必须有x,y，label代表图例属性
plt.plot(a,a*2,'go-',label='three')
plt.plot(a,a*4,'rx',label='One')

#自动创建图例,loc告诉matplotlib把图例放在哪里。如果不挑剔的话，直接设定'best'就可以了，
#它会自动选择一个合适的位置。如果想要从图例中排除一个或更多的元素，那就不要传入label，或设置label='_nolegen_'。
#在show之前设置，否则不生效
ax.legend(loc='best')

plt.show()
```

## Legend设置图例

```python
#导入包
import  matplotlib.pyplot as plt
import numpy as np


fig = plt.figure();
ax = fig.add_subplot(1, 1, 1)
#创建连续数组（0-0）
a = np.arange(10)

#返回值必须加逗号，加逗号得到的是 line2D 对象，不加逗号得到的是只有一个 line2D 对象的列表
p1, = plt.plot(a,a*2,'go-')
p2, =plt.plot(a,a*4,'rx')

'''
prop={'family':'SimHei','size':15}显示中文
legend(hadles=[,,],labels=[,,],loc='best/upper right/upper left/.../lower right')
handles就是你给他添加legend的线,如果要用handles，则前面的plt.plot，必须用l1,形式(不要忘记逗号)
此处labels会覆盖上述的plt.plot()的label
loc默认是best,给你放在一个合适的位置上，如果你拉伸弹框，位置会跟着变，自动放置合适位置
'''
plt.legend(handles=[p1,p2],prop={'family':'SimHei','size':15},loc='lower right',labels=['直线','曲线'])

plt.show()
```

# 保存图片(savefig)

```python
import matplotlib.pyplot as plt

plt.plot([3,1,4,5,2])
plt.ylabel("grade")
#默认为png文件，dpi修改输出质量
plt.savefig("qqq",dip=600)
plt.show()
```

# 区域划分subplot

## 简单绘图区域(subplot)

![img](https://i.loli.net/2021/01/16/6dEAFxgZOJyYcj7.png)

**注意：划分区域可以不使用','**

```python
import matplotlib.pyplot as plt
import numpy as np

def f(t):
    #衰减曲线
    return np.exp(-t)*np.cos(2*np.pi*t)

a = np.arange(0.0,5.0,0.02)

#划分为两行一列，选取第一个区域
plt.subplot(211)
#绘制衰减曲线
plt.plot(a,f(a))

#在将绘图区域换到整个绘图区域的第二个,自动切换
#如果注释掉下面代码，两条曲线会绘制到一张图上
plt.subplot(2,1,2)
#绘制余弦曲线
plt.plot(a,np.cos(2*np.pi*a),'r--')

plt.show()
```

## 复杂绘图区域(subplot2grid)

![img](https://i.loli.net/2021/01/16/YPawHLGn3ptIjhC.png)

![img](https://i.loli.net/2021/01/16/gx8CblmJvc9VaX4.png)

![img](https://i.loli.net/2021/01/16/tumG7Xza3KCUpyN.png)

![img](https://i.loli.net/2021/01/16/ePRn2AJBoxGgD83.png)

# 基本绘图函数

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711112843173-1716331814.png)



![img](https://i.loli.net/2021/01/16/4VwzEsygR3SUqAp.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180711112941509-1035106964.png)



## 饼图plt.pie的绘制

```python
import matplotlib
import matplotlib.pyplot as plt

labels = 'Frogs','Hogs','Dogs','Logs'
#这是各个区域所占的大小，不一定是100，会自动换算为百分比
sizes = [15,30,45,10]
#0.1是表示这个区域突出的程度
explode = (0,0.1,0,0)

#explode是突出比例，startangle起始角度
plt.pie(sizes,explode=explode,labels=labels,autopct="%1.1f%%",shadow=False,startangle=90)
#将饼图变水平
plt.axis("equal")
plt.show()
```

![image-20210116131006811](https://i.loli.net/2021/01/16/iPdS1bMLal4rtuY.png)



## 直方图plt.hist的绘制

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(0)
#均值和标准差
mu,sigma = 100,20 
#正态分布，size=100，表示一维数组，长度100
a = np.random.normal(mu,sigma,size=100)
plt.hist(a,20,histtype="stepfilled",facecolor="b",alpha=0.75)

plt.title("Histogram")

plt.show()
```

```
def hist(x, bins=10, range=None, normed=False, weights=None, cumulative=False,
         bottom=None, histtype='bar', align='mid', orientation='vertical',
         rwidth=None, log=False, color=None, label=None, stacked=False,
         hold=None, data=None, **kwargs):
```

修改第二个参数bins:代表直方图的个数，均分为多段，取其中的每段均值

```
plt.hist(a,10,normed=1,histtype="stepfilled",facecolor="b",alpha=0.75)
```

```
plt.hist(a,20,normed=1,histtype="stepfilled",facecolor="b",alpha=0.75)
```

```
plt.hist(a,40,normed=1,histtype="stepfilled",facecolor="b",alpha=0.75)
```

 normed为1代表我们要使用归一化数据（所占比例）在y轴，为0表示每个期间所占个数

```
plt.hist(a,20,normed=1,histtype="stepfilled",facecolor="b",alpha=0.75)
```

```
plt.hist(a,20,normed=0,histtype="stepfilled",facecolor="b",alpha=0.75)
```



# 参考资料

https://www.cnblogs.com/ssyfj/p/9293844.html