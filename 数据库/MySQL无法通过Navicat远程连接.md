## MySQL无法通过Navicat远程连接

1. 考虑root账号是否具有远程访问权限，进入数据库输入

    ```mysql
    use mysql;
    select host,user from user;
    ```

    ![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-04-20_09-08-44.png)

    如果root账号没有远程访问权限，则需要给root账号赋予远程访问权限

2. 输入以下命令

    ```mysql
    GRANT ALL PRIVILEGES ON *.* TO root@"%" IDENTIFIED BY "用户密码"; 
      
    // 格式：grant 权限 on 数据库名.表名 to 用户@登录主机 identified by "用户密码";
    // @ 后面是访问MySQL的客户端IP地址（或是 主机名） % 代表任意的客户端，如果填写 localhost 为本地访问（那此用户就不能远程访问该mysql数据库了）。
    ```

3. 再次通过navicat进行远程连接即可

