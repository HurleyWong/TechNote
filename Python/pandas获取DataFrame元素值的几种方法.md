## pandas获取DataFrame元素值的几种方法

### pandas.DataFrame.at

根据**行索引**和**列名**，获取一个元素的值：

```python
>>> df = pd.DataFrame([[0, 2, 3], [0, 4, 1], [10, 20, 30]],
...                   columns=['A', 'B', 'C'])
>>> df
    A   B   C
0   0   2   3
1   0   4   1
2  10  20  30
```

那么：

```python
>>> df.at[4, 'B']
2
```

或者：

```python
>>> df.iloc[5].at['B']
4
```

这里4和5都已经超过了行数的范围，但是会重新循环。即这里总共有3行，那么4就代表$4-3=1$行，再搭配`'B'`，所以是2；同理，$5-3=2$行，配合`'B'`，就是4。

### pandas.DataFrame.iat

根据行索引和列索引获取元素值

```python
>>> df = pd.DataFrame([[0, 2, 3], [0, 4, 1], [10, 20, 30]],
...                   columns=['A', 'B', 'C'])
>>> df
    A   B   C
0   0   2   3
1   0   4   1
2  10  20  30
```

那么：

```python
>>> df.iat[1, 2]
1
```

或者：

```python
>>> df.iloc[0].iat[1]
2
```

### pandas.DataFrame.loc

选取元素，或者选取行和列：

```python
>>> df = pd.DataFrame([[1, 2], [4, 5], [7, 8]],
...      index=['cobra', 'viper', 'sidewinder'],
...      columns=['max_speed', 'shield'])
>>> df
            max_speed  shield
cobra               1       2
viper               4       5
sidewinder          7       8
```













