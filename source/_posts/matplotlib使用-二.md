---
title: matplotlib使用(二)
date: 2018-07-09 13:39:44
tags: Python
categories: 学习笔记
---
# 简介

- 继续matplotlib绘制条形图、等高线图等。<!--more-->

### 散点图

```
import matplotlib.pyplot as plt
import numpy as np

n = 1024

# np.random.normal()产生标准正态分布的数集
x = np.random.normal(0, 1, n)
y = np.random.normal(0, 1, n)
# 产生颜色
t = np.arctan2(y, x)

plt.scatter(x, y, s=75, c=t)


# 隐藏坐标轴的标记
plt.xticks(())
plt.yticks(())

plt.show()
```

- 效果如图

![image](https://note.youdao.com/yws/api/personal/file/D9638C213BFE4F29B0206B1CF5EA9A49?method=download&shareKey=e3f13e7989e102dfc02793080e7696d1)

### 条形图

```
import matplotlib.pyplot as plt
import numpy as np

n = 12
# np.arange()返回一个numpy.ndarray类型的数据，包含0-11，可以通过for来遍历
X = np.arange(n)

# 产生均匀分布的两组数据
Y1 = (1 - X/float(n)) * np.random.uniform(0.5, 1.0, n)

Y2 = (1 - X/float(n)) * np.random.uniform(0.5, 1.0, n)


plt.bar(X, +Y1, facecolor='#9999ff', edgecolor='white')
plt.bar(X, -Y2, facecolor='#ff9999', edgecolor='white')

# 添加文字标注
for x, y in zip(X, Y1):
	# ha:horizontal alignment
	plt.text(x, y+0.05, '%.2f'%y, ha='center', va='bottom')

for x, y in zip(X, Y2):
	# ha:horizontal alignment
	plt.text(x, -(y+0.05), '-%.2f'%y, ha='center', va='top')

plt.xlim(-.5, n)
plt.xticks(())
plt.ylim(-1.25, 1.25)
plt.yticks(())

plt.show()
```

- 效果如图

![image](https://note.youdao.com/yws/api/personal/file/73A95079FD5C4297A4051693ABE59DE9?method=download&shareKey=a5c3c8ea96835cac928fa1b86de5ae30)

### Contours等高线图

```
import matplotlib.pyplot as plt
import numpy as np

def f(x, y):
	# 计算高度
	return (1 - x/2 + x**5 + y**3) * np.exp(-x**2-y**2)

n = 256
x = np.linspace(-3, 3, n)
y = np.linspace(-3, 3, n)
# 生成网格型数据， 接受两个一维数组生成两个二维矩阵
X, Y = np.meshgrid(x, y)

# 使用plt.contourf填充图形，cmap的取值还有plt.cm.cool， plt.cm.bone等
plt.contourf(X, Y, f(X, Y), 8, alpha=0.75, cmap=plt.cm.hot)

# 使用plt.contour添加等高线
C = plt.contour(X, Y, f(X, Y), 8, colors='black', linewidths=.5)

# 添加标注
plt.clabel(C, inline=True, fontsize=10)


plt.xticks(())
plt.yticks(())

plt.show()
```

- 效果如图

![image](https://note.youdao.com/yws/api/personal/file/11F8B2688A6D459FBDDA9326F4E3F1C7?method=download&shareKey=71ce60c4b01601868d4c3c1712a1cd60)

### Image图片

```
import matplotlib.pyplot as plt
import numpy as np

# 将产生的np.array类型的一维数组转化为3*3的二维矩阵
a = np.linspace(0, 1, 9).reshape(3, 3)

plt.imshow(a, interpolation='nearest', cmap='hot', origin='lower')
plt.colorbar()

plt.xticks(())
plt.yticks(())

plt.show()
```

- 效果如图

![image](https://note.youdao.com/yws/api/personal/file/8A05B28820D94D3886CCE7A9E726ECE7?method=download&shareKey=01c19b6c330c5579a72a35ec72d781a8)

### 3D数据

```
import matplotlib.pyplot as plt
import numpy as np
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure()
ax = Axes3D(fig)

# 产生X,Y的值
X = np.arange(-4, 4, 0.25)
Y = np.arange(-4, 4, 0.25)
X, Y = np.meshgrid(X, Y)
R = np.sqrt(X**2 + Y**2)
# 产生高度值
Z = np.sin(R)

# rstride和cstride为线的跨度
ax.plot_surface(X, Y, Z, rstride=1, cstride=1, cmap=plt.get_cmap('rainbow'))
ax.contourf(X, Y, Z, zdir='z', offset=-2, cmap='rainbow')
ax.set_zlim(-2, 2)

plt.show()
```

- 效果图

![imgae](https://note.youdao.com/yws/api/personal/file/A83B584945DB41AFB8B70F59756330A9?method=download&shareKey=4739b7a126164be61ea6988028989067)

### Subplot用法

- 多合一

```
import matplotlib.pyplot as plt

plt.figure()

# 将figure分割为两行两列，在第i个位置画图
plt.subplot(2, 2, 1)
plt.plot([0, 1], [0, 1])

plt.subplot(2, 2, 2)
plt.plot([0, 1], [0, 1])

plt.subplot(2, 2, 3)
plt.plot([0, 1], [0, 1])

plt.subplot(2, 2, 4)
plt.plot([0, 1], [0, 1])

plt.show()
```

- 多合一效果图

![image](https://note.youdao.com/yws/api/personal/file/0CDC0CF79E834FE597C44DD5594BF2FA?method=download&shareKey=14205a06f591aa23eff24bc2ed01629c)

- 分格显示效果图

![image](https://note.youdao.com/yws/api/personal/file/9B633A82BCB847DF9DD2EAA889B477DB?method=download&shareKey=4d85a2f66cc2ff797613eb1e5f5ab8e9)

- 代码

```
import matplotlib.pyplot as plt


plt.figure()

ax1 = plt.subplot2grid((3, 3), (0, 0), colspan=3, rowspan=1)
ax1.plot([1, 2], [1, 2])
ax1.set_title('ax1 title')

ax2 = plt.subplot2grid((3, 3), (1, 0), colspan=2, rowspan=1)
ax2.plot([1, 2], [1, 2])

ax3 = plt.subplot2grid((3, 3), (1, 2), colspan=1, rowspan=2)
ax3.plot([1, 2], [1, 2])

ax4 = plt.subplot2grid((3, 3), (2, 0), colspan=1, rowspan=1)
ax4.plot([1, 2], [1, 2])

ax5 = plt.subplot2grid((3, 3), (2, 1), colspan=1, rowspan=1)
ax5.plot([1, 2], [1, 2])


plt.show()
```




