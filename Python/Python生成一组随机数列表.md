## Python生成一组随机数列表

1. `np.random.rand`用于生成$[0.0, 1.0)$之间的随机浮点数。例如`np.random.rand(10)`可以随机生成10个浮点数。

2. `np.random.randn(10)`同样是生成10个数，但生成的数具有标准正态分布。

3. `np.random.randint(low, high=None, size=None, dtype=T)`是返回随机的整数，大小位于半开区间$[low, high)$，例如：

    ```python
    np.random.randint(5, size=10)
    # output: array([1, 3, 0, 3, 4, 3, 3, 4 ,4, 2])
    np.random.randint(low=5, high=7, size=10)
    # output: array([5, 5, 6, 6, 5, 5, 5, 6, 6, 6])
    ```

4. `np.random.random_integers(low, high=None, size=None)`也是返回随机的整数，但是大小都是位于闭区间$[low, high]$的。

5. `np.random.shuffle(x)`的意思是洗牌即打乱顺序；而`np.random.permutation(x)`则是返回一个随机排列。

    ```python
    arr = np.arange(10)
    np.random.shuffle(arr)
    # output: [1 7 5 2 9 4 3 6 0 8]
    
    np.random.permutation(10)
    # output: ([1, 7, 4, 3, 0, 9, 2, 5, 6, 8])
    ```

    

