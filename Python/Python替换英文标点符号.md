## Python替换英文标点符号

可以调用string包的`string.punctuation`函数就可以得到：

```
!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~
```

那么，替换的方法如下：

```python
import re
import string

line = '要替换的内容'
line = re.sub("[{}]+".format(string.punctuation), "", line)
```

