## 各平台重启MySQL的命令

### **Linux平台重启MySQL的方法**

1. 通过rpm包安装的MySQL

    ```
     service mysqld restart
    ```

2. 以上方法都无效的时候，可以通过强行命令：“killall mysql”来关闭MySQL，但是不建议用这样的方式，因为这种野蛮的方法会强行终止MySQL数据库服务，有可能导致表损坏

3. 从源码包安装的MySQL

    ```
     # linux关闭MySQL的命令 
     $mysql_dir/bin/mysqladmin -uroot -p shutdown 
     # linux启动MySQL的命令 
     $mysql_dir/bin/mysqld_safe &
    ```

    其中的mysql_dir为MySQL的安装目录，mysqladmin和mysqld_safe位于MySQL安装目录的bin目录下

具体的步骤或方法：

- RedHat Linux (Fedora Core/Cent OS)

    1. 启动

        ```
         /etc/init.d/mysqld start
        ```

    2. 停止

        ```
         /etc/init.d/mysqld stop
        ```

    3. 重启

        ```
         /etc/init.d/mysqld restart
        ```

- Debian / Ubuntu Linux

    1. 启动

        ```
         /etc/init.d/mysql start
        ```

    2. 停止

        ```
         /etc/init.d/mysql stop
        ```

    3. 重启

        ```
         /etc/init.d/mysql restart
        ```

### **Windows平台重启MySQL的方法**

在命令行输入`net start mysql`启动，输入`net stop mysql`停止服务

### 总结MySQL启动、停止、重启的方法

#### **1. 启动方式**

1. 使用service启动：`service mysqld start`
2. 使用mysqld脚本启动：`/etc/inint.d/mysqld start`
3. 使用safe_mysqld启动：`safe_mysqld&`

#### 2. 停止

1. 使用service停止：`service mysqld stop`
2. 使用mysqld脚本停止：`/etc/inint.d/mysqld stop`
3. `mysqladmin shutdown`

#### 3. 重启

1. 使用service重启：`service mysqld restart`
2. 使用mysqld脚本启动：`/etc/inint.d/mysqld restart`