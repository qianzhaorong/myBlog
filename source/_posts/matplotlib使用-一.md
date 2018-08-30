---
title: matplotlib使用(一)
date: 2018-07-08 22:45:45
tags: 
	- Python
categories:
	- 学习笔记
---

### 简介

- matplotlib是Python的绘图工具，语法与matlab相似。<!--more-->

### 安装
```
pip install matplotlib
```

### 基本用法

```
import matplotlib.pyplot as plt
import numpy as np

# 在-1到1这个区间生成50个点
x = np.linspace(-1, 1, 50)
y = x * 2 + 1
# 绘制图形
plt.plot(x, y)
# 显示图形
plt.show()
```
- 生成的图形如下

![image](https://note.youdao.com/yws/api/personal/file/8A5994C8CFB24FEEBB6894ED10C45963?method=download&shareKey=961d9054b9ea9a05fc004b1e718812c5)

### Figure使用

```
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-3, 3, 50)
y1 = x**2
y2 = x * 2 + 1

# 画出figure1
plt.figure()
plt.plot(x, y1)

# 通过指定参数画出figure3，figsize参数指定了长和宽
plt.figure(num=3, figsize=(8, 5))
plt.plot(x, y2)
# 将两张图画在一个figure中，通过参数来设置样式
plt.plot(x, y1, color='red', linewidth=1.0, linestyle='--')

plt.show()
```

- 生成的图形如下

![image](https://note.youdao.com/yws/api/personal/file/387A82B4229F430FAF6EB1C7FAD6F8A7?method=download&shareKey=b64f441797e0b1d919306cc9f5ad1c62)

![image](https://note.youdao.com/yws/api/personal/file/38176754EB7244DFB6D962202287909B?method=download&shareKey=1d066369839e83fee851a2a85bf509ed)

### 坐标轴

- 修改坐标轴
```
# 设置坐标轴的取值范围
plt.xlim((-1, 2))
plt.ylim((3, 5))    

# 修改坐标轴名称
plt.xlabel('I am x')
plt.ylabel('I am y')

# 修改坐标轴区间
new_ticks = np.linspace(-1, 2, 5)
plt.xticks(new_ticks)
# 修改坐标轴描述为文字，使用$修改字体
plt.yticks([-2, -1.8, -1, 1.22, 3], [r'$really\ bad$', r'$bad\ \alpha$', r'$normal$', r'$good$', r'$very\ good$'])
```

- 修改坐标轴位置
```
# gca = 'get current axis'
ax = plt.gca()
# 隐藏上和右坐标轴
ax.spines['right'].set_color('none')
ax.spines['top'].set_color('none')

# 将底部作为x坐标轴，左边作为y坐标轴
ax.xaxis.set_ticks_position('bottom')
ax.yaxis.set_ticks_position('left')

# 设置x坐标轴的起点为y坐标轴的0位置
ax.spines['bottom'].set_position(('data', 0))

# 设置y坐标轴的起点为x坐标轴的0位置
ax.spines['left'].set_position(('data', 0))
```
- 结果如图

![image](https://note.youdao.com/yws/api/personal/file/8A58406C6A0C4EA8BA511BF5253EB02E?method=download&shareKey=2bf28d49bd39010bc5736d542d7ce321)

### Legend

- Legend图例

```
# 使用默认参数的legend
plt.plot(x, y2, label='up')
plt.plot(x, y1, label='down')
plt.legend()
```

- 效果如图

![image](https://note.youdao.com/yws/api/personal/file/C4760AF257A64A6CA0E41E120BF558C1?method=download&shareKey=da81299780851a68d65f41c678d431e0)

```
# 不使用默认的label
line1, = plt.plot(x, y2, label='up')
line2, = plt.plot(x, y1, label='down')
plt.legend(handles=[line1, line2], labels=['aaa', 'bbb'], loc='best')
```

### 标注

- Annotation标注

```
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(-3, 3, 50)
y = 2 * x + 1

plt.plot(x, y)
plt.xlim(-1, 2)
plt.ylim(-3, 5)

ax = plt.gca()
ax.spines['right'].set_color('None')
ax.spines['top'].set_color('None')
ax.xaxis.set_ticks_position('bottom')
ax.yaxis.set_ticks_position('left')
ax.spines['bottom'].set_position(('data', 0))
ax.spines['left'].set_position(('data', 0))

x0 = 1
y0 = 2*x0 + 1

# 在图上画出x0, y0这个点
plt.scatter(x0, y0, color='b')

# 画出这个点到x轴的虚线，k--代表黑色的虚线
plt.plot([x0, x0],[y0, 0], 'k--', lw=2.5)

# 画箭头标注
plt.annotate(r'$2x+1=%s$'%y0, xy=(x0, y0), xycoords='data', xytext=(+30, -30), textcoords='offset points', fontsize=16, arrowprops=dict(arrowstyle='->', connectionstyle='arc3, rad=.2'))

# 添加文字标注
plt.text(-1, 3, r'$\mu=100,\ \sigma_t=15$')

plt.show()
```

- 结果如图

![image](https://note.youdao.com/yws/api/personal/file/7EC6DE36937E4202ACBBD83196A945D4?method=download&shareKey=e7d0c85f0995e0b5a6247c66f1f2acd3)

### 能见度

- 先来看一张图片

![image](https://note.youdao.com/yws/api/personal/file/D0EDED2EA048470AB8314953DAA98CB4?method=download&shareKey=19c31f4b440d35093135e7e4f8bdfedd)

- 使线条不挡住后面的坐标

```
for label in ax.get_xticklabels() + ax.get_yticklabels():
	label.set_fontsize(12)
	label.set_bbox(dict(facecolor='white', edgecolor='None', alpha=0.7))
```

- 效果如图

![image](https://note.youdao.com/yws/api/personal/file/1626CA4B43E344B9B53DE44819537BAD?method=download&shareKey=4103f417e606abf73c9ba7280b65b5a9)
