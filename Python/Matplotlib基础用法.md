## Matplotlib基础用法

### 折线图

`plt.plot()`前两个参数接收X轴和Y轴的变量，此外还可以接收多个参数以改变图形主体的外观：

* `color`：指定曲线的颜色，可以用常用颜色的英文，也可以使用RGB值
* `marker`：指定数据点的类型，如`o`代表圆点，`s`代表方块，`x`代表叉号等
* `linewidth`：指定曲线的宽度
* `linestyle`：指定曲线的类型，如`-`代表实线，`--`代表虚线，`-.`代表点划线等
* `alpha`：指定曲线的透明度

### 散点图

用`plt.scatter()`来绘制散点图，除了上述在折线图可用的参数外，散点图还有其它一些可选参数：

* `s`：点的大小，可以设置为与数据数组大小相同的数组来指定每个点的大小。

```python
x = np.random.randn(50)
y = np.random.randn(50)
area = np.random.randint(10, 100, 50)
plt.scatter(x, y, s=area)
```

### 柱状图

`plt.bar()`用于绘制柱状图，它还可以接收如下的参数：

* `height`：用数组指定每个柱子的高度
* `width`：指定柱子的宽度
* `align`：设置对齐方式，默认是`center`

### 箱线图

`plt.boxplot()`可以用于绘制箱线图，以下列出一些其他可能用到的参数：

* `vert`：布尔型，指定图的方向，`True`为纵向，`False`为横向
* `patch_artist`：布尔型，指定四分框内是否填充，`True`为填充

### 饼图

`plt.pie()`用于绘制饼图，它可接收如下参数：

* `explode`：当要把某一部分凸出时，将对应的值设为0.1就够
* `labels`：对应每个部分的标签
* `autopct`：显示百分比的格式
* `shadow`：是否显示阴影
* `startangle`：起始角度，从X轴起逆时针旋转的度数

### 热力图

`plt.imshow()`可以用于生成热力图，分析变量间相关性时常用此图。`imshow()`主要接收如下参数：

* `x`：即数据，可以是二维浮点型（灰度）、三维浮点型或unit8（RGB）或者四维浮点型或unit8（RGBA）数组
* `camp`：用于指定颜色图谱，默认为RGB(A)色彩空间，比如`gray`、`jet`等
* `interpolation`：插值方法，默认为`nearest`，用其他方法可以平滑色块边缘

通常还会定义一个`plt.colorbar()`用于标识颜色。

* `shrink`：设置Bar的长度（比例）

```python
plt.imshow(X, cmap=None, norm=None, aspect=None, interpolation=None, alpha=None, vmin=None, vmax=None, origin=None, extent=None, shape=None, filternorm=1, filterrad=4.0, imlim=None, resample=None, url=None, hold=None, data=None)
```

1. **X**：类数组，比如`shape(n, m)`或者`shape(n, m, 3)`

2. **cmap**：Colormap，可选，例如`cmap='gray'`

3. **aspect**：['auto' | 'euqal' | scalar]，可选

    1. 如果是'auto'，图像长宽比将和坐标系匹配
    2. 如果是'equal'，并且`extent`为None，坐标系长宽比将匹配图像；如果`extent`不为None，坐标系的长宽比将匹配`extent`

4. **interpolation**：string，可选，差值方式

    ‘none’, ‘nearest’, ‘bilinear’, ‘bicubic’, ‘spline16’, ‘spline36’, ‘hanning’, ‘hamming’, ‘hermite’, ‘kaiser’, ‘quadric’, ‘catrom’, ‘gaussian’, ‘bessel’, ‘mitchell’, ‘sinc’, ‘lanczos’之一

5. **norm**：Normalize，可选，颜色映射使用

### 图形的其他元素

#### 坐标轴

坐标轴可以手动设置范围、刻度等。以X轴为例：

* `plt.xlim`：设置坐标轴的范围
* `plt.xlabel`：设置坐标轴的名称
* `plt.xticks`：设置坐标轴的刻度，可以接收一个数组，也可以接收一对数组及其对位的刻度

利用`plt.gca()`可以对当前绘图区域的坐标轴进行更多操作

* `ax.set_title`：设置图表标题
* `ax.set_xlabel`：设置坐标轴的名称
* `ax.set_xticks`：设置坐标轴的刻度
* `ax.set_xticklabels`：设置上面所设置刻度对应的标签
* `ax.spines['left']`：一幅图共有四个坐标轴，分别于用`left`、`right`、`top`、`bottom`来表示
* `ax.spines['left'].set_color`：设置该轴颜色，将颜色设置为`none`可以隐藏该轴

#### 标题、图例、网络

* 标题：可以通过`plt.title()`设置，同时可以传入参数设置标题的颜色、字体等
* 图例：可以通过`plt.legend()`方法显示，前提是创建图形时传入了`label`参数，还可以接收`loc`参数来指定图例的位置，一般指定为`best`即可，图例会被自动放在最合适的位置
* 网格：可以通过`plt.grid()`来显示。通过传入`axis`参数可以指定显示`'x'`、`'y'`或者`'both'`方向上的网格线。网格线也可以使用`color`等参数

```python
# 设置标题
plt.title('Title', fontsize=20)
# 显示图例
plt.legend(loc='best')
# 显示网络
plt.grid(axis='y', color='grey', linestyle=':')
```

#### 标注

当需要特别标注出图上一个点时，先需要标出该点，过该点向坐标轴引一条垂线，再用箭头将其标注出来。可以使用`annotate()`的方法来让我实现这一功能。

`annotate()`第一个参数接收一组字符串作为显示的标注文字，其余部分参数如下：

* `xy`：被标注的点坐标
* `xytext`：标注文字的坐标
* `arrowprops`：字典类型的参数，定义箭头的属性
* `arrowstyle`：`arrowprops`的一个键，用于设置箭头的形状。

#### 设置中文

当不改变参数时，Matplotlib的图上的中文会变成方框，因此需要手动修改字体。

```python
plt.rcParams['font.sans-serif'] = ['SimHei']
# 解决负号变成方框的问题
plt.rcParams['axes.unicode_minus'] = False
```

#### plt.ion()和plt.ioff()

Python可视化库Matplotlib的默认显示模式是**阻塞（block）**模式。在阻塞模式下，执行`plt.show()`之后，程序会暂停在那不会继续执行，除非关闭已显示的图片。如果需要展示动态图或多个窗口，则需要使用到`plt.ion()`方法，使Matplotlib的显示模式默认转化为**交互（interactive）**模式。这样即使在脚本中遇到`plt.show()`，代码也还是会继续执行。

```python
# 打开交互模式
plt.ion()
# 显示前关掉交互模式
plt.ioff()
plt.show()
```

在`plt.show()`之前需要添加`plt.ioff()`，如果不加，界面会一闪而过，不会停留。

##### 区别

在交互模式下：

`plt.plot(x)`或者`plt.imshow(x)`是直接出图像，不需要`plt.show()`

在阻塞模式下：

`plt.plot(x)`或者`plt.imshow(x)`是直接出图像，需要`plt.show()`后才能显示图像

#### Matplotlib的cla() clf() close()的用途

```python
# clear axis即清除当前图形中的活动轴（坐标轴），其它轴不受影响
plt.cla()
# clear figure即清除所有轴（当前figure对象），但是窗口打开
# plt.clf()是plt.clear()的同义词
plt.clf()
# close 关闭当前或者指定的figure window或图片等
plt.close(fig=None)[source]
```

`plt.close()`的fig参数可以为：

* None: the current figure
* Figure: the given Figure instance
* int: a figure number
* str: a figure name
* 'all': all figures

#### Matplotlib中的tight_layout密致布局

`tight_layout`会自动调整子图参数，使之填充整个图像区域。它仅仅检查坐标轴标签、刻度标签以及标题的部分。

当拥有多个子图时，会经常看到不同轴的标签堆叠在一起。`tight_layout()`会调整子图之间的间隔来减少堆叠。

`tight_layout()`可以接受关键字参数`pad`、`w_pad`或者`h_pad`，这些参数图像边界和子图之间的额外边距。边距以字体大小单位规定。

```python
plt.tigh_layout(pad=0.4, w_pad=0.5, h_pad=1.0)
```

















