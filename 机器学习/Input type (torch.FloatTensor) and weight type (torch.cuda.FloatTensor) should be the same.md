## Input type (torch.FloatTensor) and weight type (torch.cuda.FloatTensor) should be the same

在使用PyTorch中出现这个错误。

通过观察错误，提示我们`torch.FloatTensor`和`torch.cuda.FloatTensor`要一致，从而很容易判断出可能是数据和模型不再同一处。例如，模型在GPU上，数据却在CPU上。

首先，观察是否正确地使用了CUDA，我采用的是下面的方式

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
inputs.to(device)
```

通过以上代码找出了原因，因为`torch.to()`这个方法的功能是产生一个新的tensor，而不会改变原数据。所以如果直接`inputs.to(device)`是没有用的。

要采用以下方式：

```python
inputs = inputs.to(device)
```

这样就把`inputs`放在了该放置的CPU或者GPU上了。