## list合并连接字符串

这是一个列表`list = ['huang', 'peng', 'yuan']`，如果要把列表的元素合并成一个字符串，那么可以用如下方式：

```python
str = "".join(list)
print(str)

# 结果
huangpengyuan
```

当然，如果中间想要添加间隔，比如空格或者逗号，就可以：

```python
str = " ".join(list)
# 或者
str = ",".join(list)
```

