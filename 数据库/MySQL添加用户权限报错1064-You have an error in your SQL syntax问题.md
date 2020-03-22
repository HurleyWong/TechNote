## MySQL添加用户权限报1064 - You have an error in your SQL syntax问题解决

mysql添加用户及权限报错：

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-04-20_09-20-17.png)

出现这种错误的原因有两个：

- 语法有问题
- mysql版本是否支持 此种写法

后来查找到MySQL8是不支持同时创建用户和授予权限的，只能分开写

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/20181108172917596.png)

