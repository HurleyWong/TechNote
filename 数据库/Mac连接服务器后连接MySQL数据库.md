## Mac连接服务器后连接MySQL数据库

1. 输入mysql -uroot -p，输入密码

2. 赋予任何主机访问数据的权限

    ```sh
    grant all privileges on *.* to 'root'@'%'with grant option
    ```

    如果你想允许某个用户从自己的主机连接到mysql服务器，并使用自己设定的密码作为密码

    ```shell
    GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'192.168.1.3'IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
    ```

3. 输入flush privileges

4. 输入exit退出

