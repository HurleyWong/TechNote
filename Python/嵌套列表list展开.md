## 嵌套列表list展开

### 简单嵌套列表

对于列表形如`list = [[1, 2], [3, 4], [1, 3]]`的形式，可以通过以下几种方式实现：

```python
# 普通方法
list_1 = [[1, 2], [3, 4], [1, 3]]
list_2 = []
for _ in list_1:
    list_2 += _
print(list_2)

# 列表推导
list_1 = [[1, 2], [3, 4], [1, 3]]
list_2 = [i for k in list_1 for i in k]
print(list_2)

# 使用sum
list_1 = [[1, 2], [3, 4], [1, 3]]
list_2 = sum(list_1, [])
print(list_2)
```

### 复杂嵌套列表

对于复杂的嵌套列表例如`list = [1, [2], [3, 4], [5], 6]`这种类似的形式就不能用上述的方法了。这里可以采用递归的方式完成：

```python
def flat(nums):
    res = []
    for i in nums:
        if isinstance(i, list):
            res.extend(flat(i))
        else:
            res.append(i)
     return res
```















