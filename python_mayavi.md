# Mayavi 库基本元素

## Mayavi.mlab

![image-20210114232721694](C:/Users/jiayunfei/AppData/Roaming/Typora/typora-user-images/image-20210114232721694.png)

## Mayavi API



![image-20210114233026824](https://i.loli.net/2021/01/14/REpg2ZtAfoPMx4l.png)





# 测试是否安装成功

```
from mayavi import mlab
```

# 绘图实例

```
from mayavi import mlab

x = [[-1, 1, 1, -1, -1], [-1, 1, 1, -1, -1]]
y = [[-1, -1, -1, -1, -1], [1, 1, 1, 1, 1]]
z = [[1, 1, -1, -1, 1], [1, 1, -1, -1, 1]]

s = mlab.mesh(x, y, z)
mlab.show()
```

![image-20210114233257712](https://i.loli.net/2021/01/14/KmfPIdxgAe5Da7h.png)

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