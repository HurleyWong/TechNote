## 使用Counter统计list中各个元素出现的次数

可以利用Python的collection包下的Counter的类来完成。

```python
from collections import Counter
list = ['a', 'b', 'c', 'b', 'c']
result = Counter(list)
print(result)
```

结果为：

```python
{'a': 1, 'b': 2, 'c': 2}
```

那么如何对以上结果做出相应的操作呢？

因为Counter类返回值跟字典很类似，所以字典类的方法对Counter对象也是适用的。

```python
print(result.keys())
print(result.has_key('a'))
print(result.get('a'))
print(result.items())
print(result.values())
print(result.viewitems())
print(result.viewkeys())
```

输出结果分别对应如下：

```python
['a', 'b', 'c']								# keys()
True										# has_key()
1 											# get()
[('a', 1), ('b', 2), ('c', 2)] 				# items()
[1, 2, 2]									# values()
dict_items([('a', 1), ('b', 2), ('c', 2)])	# viewitems()
dict_items(['a', 'b', 'c'])					# viewkeys()
```

