## keras基础模型调参指南

### 1. 初始化一个NN模型

随机初始化一个NN模型

```python
model = Sequential()
model.add(Dense(input_dim=28*28,units=633,activation='sigmoid'))
model.add(Dense(units=633,activation='sigmoid'))
model.add(Dense(units=633,activation='sigmoid'))
model.add(Dense(units=10,activation='softmax'))

model.compile(loss='mse',optimizer=SGD(lr=0.1),metrics=['accuracy'])

model.fit(x_train,y_train,batch_size=100,epochs=20)

train_result = model.evaluate(x_train,y_train,batch_size=10000)
test_result = model.evaluate(x_test,y_test)
```

### 2. 调整Loss Function

从损失函数入手，修改损失函数。原模型选用的损失函数是MSE。MSE是均方误差，往往用于线性回归的损失函数。这里是多分类问题，如果就换成`categorical_crossentropy`。

```python
model.compile(loss='categorical_crossentropy')
```

### 3. 调整batch_size

batch_size在深度学习模型中十分重要，叫做梯度下降。可以参考以下步骤：

1. 随机初始化神经网络的参数
2. 随机选择第一个batch，计算其loss，计算偏微分，根据L`更新参数
3. 继续随机选择一个batch，计算其loss，计算偏微分，根据L``更新参数
4. 重复上述2-3步，直到所有的batch都被更新了一次，一个epoch才算结束

```python
# 增大batch_size
model.fit(x_train, y_train, batch_size=1000, epochs=20)
# 减小batch_size
model.fit(x_train, y_train, batch_size=10, epochs=20)
```

如果设置太大的batch_size，训练效率是快了很多，但是效果较差。如果按照batch_size的原理，减小batch_size的值，效率会慢很多，但效果不错。

### 4. 调整layer

通过增加隐藏层，看看效果。

```python
model.add(Dense(input_dim=28*28, units=633, activation='sigmoid'))
for _ in range(10)
	model.add(Dense(units=633, activation='sigmoid'))
model.add(Dense(units=10, activation='softmax'))
```

结果是**效率很差**。所以并不能盲目地通过增加隐含层数量来提升效果。

### 5. 调整activation function

通过比较不同激活函数在的差异，在不同的场景下选择合适的激活函数。例如这里把Sigmoid都换成relu。

```python
model.add(Dense(input_dim=28*28, units=633, activation='relu'))
for _ in range(2):
  model.add(Dense(units=633, activation='relu'))
model.add(Dense(units=10, activation='softmax'))
```

从结果可以看出，在该场景下选择**relu**比Sigmoid好很多。

### 6. 调整optimizer

优化器除了有初始模型中的SGD，还有Adam、RMSprop、Adagrad、Adamax、Nadam等。可以通过换用不同的优化器来检查效果。

```python
model.compile(loss='categorical_crossentropy', optimizer='Adam', metrics=['accuracy'])
```

可以发现采用Adam的效果更好。

### 7. 调整Dropout

Dropout的作用就是减少过拟合情况，是最简单的神经网络正则化方法，可以用于输入层和隐含层，取值在0-1之间，一般会在**0.2-0.7**之间比较好。

```python
model = Sequential()
model.add(Dense(input_dim=28*28, units=633, activation='relu'))
model.add(Dropout(0.7))

for _ in range(2):
  model.add(Dense(units=633, activation='relu'))
  model.add(Dropout(0.7))

model.add(Dense(units=10, activation='softmax'))

model.compile(loss='categorical_crossentropy', 
             optimizer='Adam', metrics=['accuracy'])
model.fit(x_train, y_train, batch_size=100, epochs=20)
```

通过增加0.7的Dropout，效果有所下降，但能让Train和Test之间的差距缩小，降低过拟合的情况。