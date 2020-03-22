## Google Colab安装2.x版本的Tensorflow

Google Colab目前的默认Tensorflow的版本是1.x版本，但实际上现在很多的代码都是基于2.x版本的Tensorflow了。

试过了网上很多的方法都没有效果，后来发现可以直接通过输入以下命令：

```python
pip install tensorflow-gpu
```

等待下载安装完成之后可以进行测试

```python
import tensorflow as tf
tf.__version__
```

得到的结果就是2.x版本的Tensorflow。

