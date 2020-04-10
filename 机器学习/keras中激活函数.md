## keras中激活函数

激活函数是神经网络中一个很重要的部分，每一层的网络输出都要经过激活函数。

### 使用

可以在`Activation`层中找到。

```python
model.add(Dense(64))
model.add(Activation("relu"))
```

### 常用的激活函数

* softmax：在**多分类**中常用的激活函数，是基于逻辑回归的，用于多分类神经网络输出
* softplus：`softplus(x)=log(1+e^x)`，近似生物神经激活函数，最近出现
* relu：近似生物神经激活函数，最近出现
* tanh：双曲正切激活函数，十分常用
* sigmoid：S型曲线激活函数，**最常用**，用于隐层神经元输出
* hard_sigmoid：基于S型激活函数
* linear：线性激活函数，最简单，用于回归神经网络输出（或二分类问题）

#### Softmax

Softmax用于多分类神经网络输出，函数公式如下：

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-11-29_14-25-21.png)

Softmax是Sigmoid的扩展。当类别数k=2时，Softmax回归退化为Logistic回归。

#### Relu

Relu函数的形状如下：

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/v2-e05dd5aa9a1674395a279da6645c060f_hd.jpg)

它的函数公式是：
$$
f(x) = max(0, x)
$$
它不像sigmoid类函数一样会出现梯度消失的情况。

它对比sigmoid类函数的主要变化有：

* 单侧抑制
* 相对宽阔的兴奋边界
* 稀疏激活性

它存在的问题是：Relu单元比较脆弱并且可能“死掉”，而且是不可逆的，因此导致了数据多样化的丢失。通过合理设置学习率，会降低神经元“死掉”的概率。

#### Sigmoid

非线性函数Sigmoid的数学公式是：
$$
\sigma=\frac{1}{1+e^{-x}}
$$
函数图像如下所示，它输入实数值并将其挤压到0-1范围内，适合输出为概率的情况。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/v2-4b26e9fdd710e3621467de2fa935d63f_hd.jpg)

但是它也存在一些问题：

* Sigmoid函数饱和时会使梯度消失。当神经元的激活在接近0或者1处时会饱和，在这些区域梯度几乎都是0，这样会导致梯度消失，几乎就有没有信号通过神经传回上一层。
* Sigmoid函数的输出不是零中心的。因为如果输入神经元的数据总是正数，那么关于![[公式]](https://www.zhihu.com/equation?tex=w)的梯度在反向传播的过程中，将会要么全部是正数，要么全部是负数，这将会导致梯度下降权重更新时出现z字型的下降。

#### Tanh

非线性函数的数学公式是：
$$
tanh(x) = 2\sigma(2x)-1
$$
Tanh非线性函数图像如下图所示，它将实数值压缩到[-1, 1]之间。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/v2-c14a20c9ccd9c724e603aafdc11dfdb8_hd.jpg)

Tanh解决了Sigmoid的输出无零中心的问题，但仍然存在饱和问题。

为了解决饱和问题，会在激活函数前进行batch normalization，尽可能保证每一层网络的输入具有均值较小的、零中心的分布。

