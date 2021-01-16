# 安装

```
VTK　　　　>pip3 install VTK-7.1.1-cp35-cp35m-win_amd64.whl
numpy　　 >pip3 install numpy‑1.14.5+mkl‑cp35‑cp35m‑win_amd64.whl
traits　　>pip3 install traits-4.6.0-cp36-cp36m-win_amd64.whl
mayavi　　>pip3 install mayavi-4.5.0+vtk71-cp35-cp35m-win_amd64.whl
PyQt4　　 >pip3 install PyQt4-4.11.4-cp35-cp35m-win_amd64.whl
```

# 测试是否安装成功

```
from mayavi import mlab
```

# Mayavi库的基本元素

```
1.处理图形可视化和图形操作的mlab模块
2.操作管线对象，窗口对象的api
```



## mlab模块

![img](https://i.loli.net/2021/01/16/3mUFBK26SThJ8nE.png)



## mayavi的api

![img](https://i.loli.net/2021/01/16/ckWe9xGA23t8Hyu.png)

# 快速绘图实例

## mlab.mesh的使用，快速创建绘图

```
from mayavi import mlab

x = [[-1, 1, 1, -1, -1], [-1, 1, 1, -1, -1]]
y = [[-1, -1, -1, -1, -1], [1, 1, 1, 1, 1]]
z = [[1, 1, -1, -1, 1], [1, 1, -1, -1, 1]]

for i in range(2):
    for j in range(5):
        print(x[i][j],y[i][j],z[i][j])

s = mlab.mesh(x, y, z)
mlab.show()
```

![image-20210114233257712](https://i.loli.net/2021/01/14/KmfPIdxgAe5Da7h.png)



![img](https://i.loli.net/2021/01/16/LQSkRE3mu4G6Ohr.png)



## 创建一个较为复杂绘图

```
from mayavi import mlab
from numpy import pi, sin, cos, mgrid

#建立数据
dphi, dtheta = pi/250.0, pi/250.0
[phi, theta] = mgrid[0:pi+dphi*1.5:dphi, 0:2*pi+dtheta*1.5:dtheta]
m0 = 4; m1 = 3; m2 = 2; m3 = 3; m4 = 6; m5 = 2; m6 = 6; m7 = 4;
r = sin(m0*phi)**m1 + cos(m2*phi)**m3 + sin(m4*theta)**m5 + cos(m6*theta)**m7
x = r*sin(phi)*cos(theta)
y = r*cos(phi)
z = r*sin(phi)*sin(theta)

#对该数据进行可视化
s = mlab.mesh(x, y, z)
mlab.show()
```

![image-20210114233804436](https://i.loli.net/2021/01/14/Xtakg2UEKF5VP8f.png)

键盘鼠标对场景进行操作

- 旋转场景：左键拖动或键盘的方向键
- 平移场景：按住Shift键并使用左键拖动，或shift+方向键盘
- 缩放场景：鼠标右键上下拖动或使用“ +” 和“ -”按键
- 滚动相机：按住CTRL键并用左键拖动
- 工具栏：从坐标轴6个方向观察场景、等角投影、切换平行透视和成角透视等

# Mayavi 管线

- Engine：建立和销毁Scenes
- Scenes：多个数据集合Sources
- Filters：对数据进行变换
- Module Manager：控制颜色，Colors and Legends
- Modules：最终数据的表示，如线条、平面等

# Mlab了解

```
Mlab是Mayavi提供的面向脚本的api，他可以实现快速的三维可视化，Mayavi可以通过Mlab的绘图函数对Numpy数组建立可视化。
```

过程为：

```
1.建立数据源

2.使用Filter（可选）对数据进行加工

3.添加可视化模块，我们可以通过修改可视化模块的属性，来修改可视化场景
```

# mgrid和ogrid区别

![img](https://img-blog.csdn.net/20170706135936380?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc2lzczBzaXNz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

# 基于Numpy数组的绘图函数

![img](https://i.loli.net/2021/01/16/5WmYzj94eSLyDwc.png)

## Point3d（点图像0维）

![img](https://i.loli.net/2021/01/16/Px9pQ6U7wMNDYrI.png)

![img](https://i.loli.net/2021/01/16/AXFLxZR28OqpJVr.png)

![img](https://i.loli.net/2021/01/16/onOTHP8XQEaNDud.png)

```
这里我们可以看到Point3D参数的描述，是对vtk对象的整体描述，因为Mayavi是对VTK的整体封装，因此Mayavi建立的对象也就是VTK的对象
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab

#建立数据
t = np.linspace(0,4*np.pi,20)   #linspace根据起止数据等间距填充数据，分为20组，所以下面将产生20个点
x = np.sin(2*t)
y = np.cos(t)
z = np.cos(2*t)
s = 2 + np.sin(t)

#对数据进行可视化
points = mlab.points3d(x,y,z,s,colormap="Reds",scale_factor=.25)
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mlab.points3d(x,y,z,s,colormap="Reds",scale_factor=.25) #x,y,z表示Numpy数组，列表或者其他形式的点三维坐标，s表示在该点处的标量值，scale_factor放缩比例
```

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713075524566-1712253999.png)

```
这里:标量值越大，点的尺寸越大，颜色越红
points = mlab.points3d(x,y,z,s,colormap="Greens",scale_factor=.25)
```

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713080131105-526983225.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713094728204-213722142.png)

```
Mayavi.mlab.show建立了简单的GUI，并开始了事件循环，stop用来定义GUI的事件循环是否结束
```

 

```python
import numpy as np
from mayavi import mlab

x = np.arange(10)
y = np.arange(10)
z = np.arange(10)
#z=[7,8,9]
print(a)

#对数据进行可视化
points = mlab.points3d(x,y,z,colormap="Reds",scale_factor=.25)
mlab.show()
```



## plot3d（线图形一维）

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713094949858-1791019942.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713095003110-751707949.png)

![img](https://i.loli.net/2021/01/16/LoWunFdzMcN9Bhs.png)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab　　#引入mlab库

#建立数据
n_mer,n_long = 6,11
dphi = np.pi / 1000.0
phi = np.arange(0.0,2*np.pi+0.5*dphi,dphi)
mu = phi * n_mer
x = np.cos(mu)*(1+np.cos(n_long*mu/n_mer)*0.5)
y = np.sin(mu)*(1+np.cos(n_long*mu/n_mer)*0.5)
z = np.sin(n_long*mu/n_mer)*0.5

#对数据进行可视化
l = mlab.plot3d(x,y,z,np.sin(mu),tube_radius=0.025,colormap="Spectral")
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://i.loli.net/2021/01/16/WwqGtSNkoP3s5Bp.png)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713095753047-1815906855.png)

## 2D数据（二维）

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713100021770-1042479425.png)

### （1）imshow方法

![img](https://i.loli.net/2021/01/16/EkjUxBP4Yv8dHS5.png)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab

#建立数据
s = np.random.random((10,10))   #二维数据

#对数据进行可视化
img = mlab.imshow(s,colormap="gist_earth")  #gist_earth以地球表面的色彩为颜色的颜色映射关系
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713101103660-1138575193.png)

### （2）surf方法

![img](https://i.loli.net/2021/01/16/Ets6eOQ4gbhKWNI.png)

```
s:二维数组第一列表示x轴位置，第二列表示y轴位置，x,y可以是一维或者二维数组，一般情况下，他们都由numpy的mgrid或ogrid得到
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab

def f(x,y):
    return np.sin(x-y)+np.cos(x+y)

x,y = np.mgrid[-7.:7.05:0.1,-5.:5.05:0.05]
s = mlab.surf(x,y,f)
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
mgrid返回两个二维数组（个数是不固定的，我们放置几个元素，就会生成几个二维数组）
-7.:7.05:0.1---->最小-7，最大7.05，步长为0.1依次生成一个n*n矩阵
```

 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
>>> x,y = np.mgrid[-7.:7.05:0.1,-5.:5.05:0.05]
>>> x
array([[-7. , -7. , -7. , ..., -7. , -7. , -7. ],
       [-6.9, -6.9, -6.9, ..., -6.9, -6.9, -6.9],
       [-6.8, -6.8, -6.8, ..., -6.8, -6.8, -6.8],
       ...,
       [ 6.8,  6.8,  6.8, ...,  6.8,  6.8,  6.8],
       [ 6.9,  6.9,  6.9, ...,  6.9,  6.9,  6.9],
       [ 7. ,  7. ,  7. , ...,  7. ,  7. ,  7. ]])
>>> y
array([[-5.  , -4.95, -4.9 , ...,  4.9 ,  4.95,  5.  ],
       [-5.  , -4.95, -4.9 , ...,  4.9 ,  4.95,  5.  ],
       [-5.  , -4.95, -4.9 , ...,  4.9 ,  4.95,  5.  ],
       ...,
       [-5.  , -4.95, -4.9 , ...,  4.9 ,  4.95,  5.  ],
       [-5.  , -4.95, -4.9 , ...,  4.9 ,  4.95,  5.  ],
       [-5.  , -4.95, -4.9 , ...,  4.9 ,  4.95,  5.  ]])
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

![img](https://i.loli.net/2021/01/16/1Y7utNIFJA4yjMB.png)

### （3）contour_surf() 

contour_surf() 与surf()类似，单求解的是等值线，surf求解的是曲面

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab

def f(x,y):
    return np.sin(x-y)+np.cos(x+y)

x,y = np.mgrid[-7.:7.05:0.1,-5.:5.05:0.05]
s = mlab.contour_surf(x,y,f)
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713102600153-1441643867.png)

## 3D数据（三维）

![img](https://images2018.cnblogs.com/blog/1309518/201807/1309518-20180713102714729-599272114.png)

### （1）contour3d方法

![img](https://i.loli.net/2021/01/16/UhcHRNButIMFbf9.png)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab

x,y,z = np.ogrid[-5:5:64j,-5:5:64j,-5:5:64j]　　#64j表示数组长度为64
scalars = x*x + y*y +z*z
obj = mlab.contour3d(scalars,contours=8,transparent=True)　　#contours八个等值面　　transparent该对象可以透明表示，可以查看内部
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

```
ogrid返回3个三维数组（几个是不固定的，我们设置了几个元素，就生成相对应个三维数组）
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
>>> x,y,z = np.ogrid[-5:5:64j,-5:5:64j,-5:5:64j]
>>> x
array([[[-5.        ]],　　#共64个元素

       [[-4.84126984]],

       [[-4.68253968]],

    　　.......
       [[ 4.68253968]],

       [[ 4.84126984]],

       [[ 5.        ]]])
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://i.loli.net/2021/01/16/jAedU2Lu58bRqWT.png)

### （2）quiver3d()方法

![img](https://i.loli.net/2021/01/16/Hp5SLxA46dXTBmU.png)

（x,y,z表示箭头位置，二维即可，不需要三维表示）

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import numpy as np
from mayavi import mlab

x,y,z = np.mgrid[-2:3,-2:3,-2:3]
r = np.sqrt(x**2 + y**2 + z**4)
u = y*np.sin(r)/(r+0.001)
v = -x*np.sin(r)/(r+0.001)
w = np.zeros_like(z)

obj = mlab.quiver3d(x,y,z,u,v,w,line_width=3,scale_factor=1)
mlab.show()
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://i.loli.net/2021/01/16/wcfOjxCEvQ2y1YS.png)

 



# 参考资料

https://www.cnblogs.com/ssyfj/p/9306602.html