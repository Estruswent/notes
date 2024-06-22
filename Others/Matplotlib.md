# 前言

额，应某些课程所需，绘图变得越来越重要，然而很遗憾de是，辅学貌似木有讲解相关芝士（叠个buff，如果有，就是我自己没看到，我的问题），所以本人去查找了一些相关芝士学习，并由此记录下来。
之前本来考虑入门matlab绘图，但是学长告诫本人该软件“太笨重”以及“后面没什么地方用到”，所以接受学长推荐，选择入门`matplotlib`。

# 简介

> "Matplotlib is a comprehensive **library** for creating static, animated, and interactive visualizations in Python. Matplotlib makes easy things easy and hard things possible."
> "NetworkX is a Python **package** for the creation, manipulation, and study of the structure, dynamics, and functions of complex networks."

官方文本介绍，一看就懂......
这个部分应该会不断更新，同时大部分你想画的图都可以参考这个范例官网
>[Matplolib示例](https://www.matplotlib.net/stable/gallery/index.html)

# 准备工作

python环境自然是需要的......你用的是人家的库......

本人使用windows系统，选择将anaconda加入环境变量后下载`matplotlib`库，也可以用`pip`等手段。在终端中输入`conda install matplotlib`和`conda install networkx`。

# 开始绘图

## 一、导入库

好比`#include<stdio.h>`，你需要导入你的库，以下为参考的库。

```python
# 导入matplotlib库，并命名为mpl
import matplotlib as mpl
# 导入pyplot模块，并命名为plt
import matplotlib.pyplot as plt
# 导入numpy库，并命名为np
import numpy as np
# 导入networkx库，并命名为nx
import networkx as nx
```

## 二、绘制图表

### 类型一：由多个已知点绘制单个$x-y$ 折线图

主打一个实用主义，毕竟这个在普物实验里经常出现......

#### 步骤

首先加入你要绘制的点坐标。
```python
# x坐标记录语法为：
x = [a, b, c, d,...]
# y坐标记录语法为：
y = [A, B, C, D,...]
```
然后使用`plot`将点迹穿起来绘图。
```python
# color,marker,linestyle可以不写
plt.plot(x, y, color = '线条颜色', marker = '点的形状', linestyle = '线条形状', label = '你想为这条曲线取的名字')
```
再使用`axis`限制坐标轴范围。
```python
plt.axis([x轴最小值, x轴最大值, y轴最小值, y轴最大值])
```
接下来使用`xlabel`和`ylabel`分别为x轴和y轴取名，用`title`为整个曲线图取标题。
```python
plt.xlabel('x轴的名字')
plt.ylabel('y轴的名字')
# 在官方文档里，这里使用了双引号
plt.title("你的标题")
```
最后使用`show`输出折线图。
```python
plt.show()
```

#### 完整代码
```python
import matplotlib as mpl
import matplotlib.pyplot as plt
import numpy as np
x = [a, b, c, d,...]
y = [A, B, C, D,...]
plt.plot(x, y, color = '线条颜色', marker = '点的形状', linestyle = '线条形状', label = '你想为这条曲线取的名字')
plt.axis([x轴最小值, x轴最大值, y轴最小值, y轴最大值])
plt.xlabel('x轴的名字')
plt.ylabel('y轴的名字')
# 在官方文档里，使用了双引号，不要搞错！
plt.title("你的标题")
plt.show()
```

### 类型二：绘制单个无向图

这个想必不陌生，FDS的报告里整个图出来~~可显得高级不少（bushi）~~。

#### 步骤

首先加入你要绘制的节点(`nodes`)和边(`edges`)。
```python
# nodes的语法很简单，nodes = ['节点1', '节点2', '节点3', ...]
nodes = ['a', 'b', 'c', 'd', ...]
# edges只是看着复杂，实际上edges = [边1, 边2, 边3, ...]
# 而对于边的表示，若为无权重，则('a', 'b')或('b', 'a')；若为有权重，则('a', 'b', weight)
edges = [
    ('a', 'b', weight1),('c', 'd', weight2),...
]
```
然后使用`Graph`创建无向图。
```python
G = nx.Graph() # 若为无向图
```
接着使用`add_nodes_from()`和`add_edges_from()`或`add_weighted_edges_from`将节点和边加入到图中。
```python
G.add_nodes_from(nodes)
# 若图无权重
G.add_edges_from(edges)
# 若图有权重
G.add_weighted_edges_from(edges)
```
接下来使用`spring_layout()`、`draw`以及`draw_networkx_edge_labels`绘图。
```python
# k的含义：代表弹簧力常数。这个值越大，节点之间的斥力越大，节点之间的距离会越大。默认值是None，此时会根据图中节点的数量来计算一个合适的值，一般都直接省略k。
pos = nx.spring_layout(G, k = 布局调整参数)
'''
draw的作用就是画出这幅图
G: NetworkX 图对象，包含了节点和边。
pos: 一个字典，指定了图中每个节点的位置，这个位置由刚才的布局函数nx.spring_layout计算得出。
with_labels: 布尔值，指示是否在节点旁边显示节点的标签（即节点的名字）。默认为False。
node_size: 节点的大小。可以是单个数值，也可以是节点大小的一个列表，与节点一一对应。
node_color: 节点的颜色。可以是单一颜色，也可以是节点颜色的一个列表，与节点一一对应。
edge_color: 边的颜色。可以是单一颜色，也可以是边颜色的一个列表，与边一一对应。
font_size: 节点标签的字体大小。
font_weight: 节点标签的字体粗细。
'''
nx.draw(G, pos, with_labels = True, node_size = 节点大小, node_color='节点颜色', edge_color = '边的颜色', font_size = 节点标签的字体大小, font_weight='节点标签的字体粗细')
# 这个函数主要是针对有权重的图，将刚才的边的权重加入到集合edge_labels中
edge_labels = nx.get_edge_attributes(G, 'weight')
# 绘制边的权重
nx.draw_networkx_edge_labels(G, pos, edge_labels = edge_labels)
```
最后使用`show`输出无向图
```python
# 这个操作是为了不显示坐标轴
plt.axis('off')
# 输出无向图
plt.show()
```

#### 完整代码（以加权图为例）
```python
nodes = ['a', 'b', 'c', 'd', ...]
edges = [
    ('a', 'b', weight1),('c', 'd', weight2),...
]

G = nx.Graph()
G.add_nodes_from(nodes)
G.add_weighted_edges_from(edges) # 此处展示有权重的情况，毕竟这种情况出现更多

pos = nx.spring_layout(G, k = 布局调整参数)

nx.draw(G, pos, with_labels = True, node_size = 节点大小, node_color='节点颜色', edge_color = '边的颜色', font_size = 节点标签的字体大小, font_weight='节点标签的字体粗细')
edge_labels = nx.get_edge_attributes(G, 'weight')
nx.draw_networkx_edge_labels(G, pos, edge_labels)

plt.axis('off')
plt.show()
```

### 类型三：绘制单个有向图

这个和上面那个类似，这里采取分开画的方法，用多个`draw`相关的函数完成，而上述直接用`draw`完成。

#### 步骤

首先还是加入你要绘制的节点(`nodes`)和边(`edges`)。
```python
nodes = ['a', 'b', 'c', 'd', ...]
# 如果是无权图
edges = [
    ('a', 'b'),('c', 'd'),...
]
# 如果是加权图
edges = [
    ('a', 'b', weight1),('c', 'd', weight2),...
]
```
然后`DiGraph()`创建有向图。
```python
G = nx.DiGraph()
```
接下来使用`add_nodes_from`和`add_edges_from`来将边和节点加入图中。
```python
G.add_nodes_from(nodes)
# 图无权重
G.add_edges_from(edges)
#图有权重
G.add_weighted_edges_from(edges)
```
再使用`draw_networkx_nodes`、`draw_networkx_edges`和`draw_network_labels`等绘制图
```python
pos = nx.spring_layout(G, k = 布局调整参数)
# 绘制节点
G.draw_networkx_nodes(G, pos, node_size = 节点大小, node_color = '节点颜色')
# 绘制边
G.draw_networkx_edges(G, pos, width = 宽度值, edge_color = '边的颜色', alpha = 透明度值)
# 给节点绘制标签
G.draw_networkx_labels(G, pos)
# 如果是加权的，还需要以下部分来画上权重
# `edge_labels`是一个字典，其中键是边的元组 `(u, v)`，值是该边上 `'weight'` 属性的值。这确保了只有权重值被用作边标签。`G.edges(data=True)` 返回一个包含边的数据和属性的迭代器，我们可以直接从中提取出权重值。
edge_labels = {(u, v): d['weight'] for u, v, d in G.edges(data=True)}
G.draw_networkx_edge_labels(G, pos, edge_labels = edge_labels)
```
最后使用`show`输出有向图
```python
plt.axis('off')
plt.show()
```

#### 完整代码(以加权图为例)
```python
nodes = ['a', 'b', 'c', 'd', ...]
edges = [
    ('a', 'b', weight1),('c', 'd', weight2),...
]

G = nx.DiGraph()

G.add_nodes_from(nodes)
G.add_weighted_edges_from(edges)

pos = nx.spring_layout(G, k = 布局调整参数)
G.draw_networkx_nodes(G, pos, node_size = 节点大小, node_color = '节点颜色')
G.draw_networkx_edges(G, pos, width = 宽度值, edge_color = '边的颜色', alpha = 透明度值)
G.draw_networkx_labels(G, pos)
edge_labels = nx.get_edge_attributes(G, 'weight')
G.draw_networkx_edge_labels(G, pos, edge_labels)

plt.axis('off')
plt.show()
```

### 类型四：由多个已知点生成拟合n阶多项式的单个x-y图

显示散点。
```python
 plt.scatter(x, y)
```

和类型一大部分相同，关键步骤在于拟合。
```python
# 由polyfit函数生成一个n阶多项式模型
model = np.polyfit(x, y, 需要拟合的阶数n)
# 由poly1d函数将该模型转化为一个函数，记为f_model
# f_model相当于就是拟合出的解析式，带入x就得到y了
f_model = np.poly1d(model)
plt.plot(x, f_model(x))
```

# 彩蛋