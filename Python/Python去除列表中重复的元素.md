## Python去除列表中重复的元素

### 排序改变

1. 使用内置的`set`

    ```python
    l1 =['b', 'c', 'd', 'b', 'c', 'a', 'a']
    l2 = list(set(l1))
    print l2
    ```

2. 使用`fromkeys().keys()`的方法：

    ```python
    l1 =['b', 'c', 'd', 'b', 'c', 'a', 'a']
    l2 = {}.fromkeys(l1).keys()
    print l2
    ```

这样上述两种方法的缺点是去除重复元素后，列表中的元素的位置即排序发生了改变，变成了`['a', 'c', 'b', 'd']`

### 排序未变

如果想要排序保持不变，则可以使用使用下面几种方法：

1. 用list的`sort`方法：

    ```python
    l1 = ['b','c','d','b','c','a','a']
    l2 = list(set(l1))
    l2.sort(key=l1.index)
    # 或者
    l2 = sorted(set(l1), key=l1.index)
    print l2
    ```

2. 用遍历的方式：

    ```python
    l1 = ['b','c','d','b','c','a','a']
    l2 = []
    for i in l1:
        if not i in l2:
            l2.append(i)
    print l2
    
    # 或者简写
    l1 = ['b','c','d','b','c','a','a']
    l2 = []
    [l2.append(i) for i in l1 if not i in l2]
    print l2
    ```

用这两种方法就可以在排序后保持原有顺序不变了，`['b', 'c', 'd', 'a']`









