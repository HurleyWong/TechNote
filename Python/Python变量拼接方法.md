## Python变量拼接方法

1. 字符串的话可以通过`+`来进行拼接，把字符串和变量拼接在一起：

    ```python
    name = 'hurley'
    meet = 'nice to meet you'
    print('你好，' + hurley + '，' + meet)
    ```

2. 通过`{}`表示变量，然后通过`format`函数传入要填入的变量，**多个的话就要用逗号隔开**：

    ```python
    first_name = 'A'
    last_name = 'B'
    print('你好，{} {}'.format(first_name,last_name))
    ```

3. 可以在字符串前加`f`，然后在字符串中用（变量名）自动拼接内容：

    ```python
    name1 = 'A'
    name2 = 'B'
    print(f'你好，{name1}，我是{name2}')
    ```

4. 使用`%s`，然后再接上`%(变量名)`的方式获取，多个的话用逗号隔开：

    ```python
    name1 = 'A'
    name2 = 'B'
    print('你好，%s，我是%s' % (name1,name2))
    ```

    