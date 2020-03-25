## Linux下安装与卸载MySQL8.x

## 安装MySQL

### 1. 查询是否已安装MySQL

```
rpm -qa|grep mysql
```

如果已安装MySQL，则按照卸载MySQL的方式完全卸载干净

### 2. 去官网复制链接用wget下载MySQL到服务器

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-04-20_22-18-36.png)

例如以下命令：

```
wget https://dev.mysql.com/get/mysql80-community-release-el6-2.noarch.rpm
```

如果提示没有安装wget，则通过以下命令先安装wget

```
yum -y install wget
```

### 3. 安装MySQL数据库

1. 第一步

    ```
    rpm -ivh mysql80-community-release-el6-2.noarch.rpm
    ```

2. 第二步

    ```
    yum install mysql-server
    ```

    执行后会跳出2次选择，输入Y继续安装

3. 最后出现以下指令，则说明安装成功

    ```
    Installed:
    mysql-community-server.i686 0:8.0.13-1.el6                      
    Dependency Installed:
    mysql-community-client.i686 0:8.0.13-1.el6  mysql-community-common.i686 0:8.0.13-1.el6  mysql-community-libs.i686 0:8.0.13-1.el6  numactl.i686 0:2.0.9-2.el6 
    Complete!
    ```

4. 查询是否安装成功

    ```
    mysqladmin -V
    ```

5. 开启MySQL

    ```
    service mysqld start
    ```

    查看MySQL启动状态

    ```
    service mysqld status
    ```

6. 查看系统给root用户默认自动生成的密码

    ```
    cat /var/log/mysqld.log
    ```

    密码显示在A temporary password的后面

7. 通过命令行登录和修改密码

    ```
    mysql -uroot -p
    ```

    注意，在MySQL5.7之后的版本，必须修改密码后才能操作，并且对密码要求必须严格，至少8位以及包含大小写等。所以，如果想要设置成简单的密码，则要以下两条命令：

    ```
    set global validate_password.policy=0;
    set global validate_password.length=1;
    ```

    然后设置密码

    ```
    alter user user() identified by '123456';
    ```

8. 设置权限

    首先注意：需要关闭防火墙或者开放3306端口

    ```
    # 暂时关闭
    service iptables stop
    # 设置成开启不自启
    chkconfig iptables off
    # 开启3306端口
    /sbin/iptables -I INPUT -p tcp --dport 3306 -j ACCEPT
    # 保存配置
    /etc/rc.d/init.d/iptables save
    # 重启服务
    /etc/rc.d/init.d/iptables restart
    ```

    然后进行远程连接，如果遇到如下错误

    1130 - Host '某个IP地址' is not allowed to connect to this MySQL server

    那么首先在命令行登录MySQL，然后发现root的登录主机是localhost，这显然不能登录，所以需要把root用户的localhost设置为%，这样任意主机都可以连接

    ```
    mysql> use mysql;
    mysql> select user,host from user;
    mysql> update user set host = '%' where user = 'root';
    # 然后刷新权限
    mysql> flush privileges;
    ```

9. 用Navicat搭配SSH连接远程数据库

    ![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-04-20_22-21-04.png)

    在常规的选项里，连接名是自己定义的。主机或者ip地址是本地localhost或者填写127.0.0.1，端口是3306，用户名和密码是登录我们之前的创建的数据库的用户名密码。之前我们为root用户赋予了远程访问的权限，所以这里我们也可以用root用户和其密码登录。

    然后还需要通过SSH连接服务器。

    ![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-04-20_22-22-57.png)

    这里的主机就是我们的服务器的IP地址，端口默认22，用户名和密码都是我们连接自己服务器的用户名密码。

    填写完成后，就可以通过测试连接测试是否能够连接成功。

## 卸载环境

### 1. 检查当前是否安装MySQL

```
rpm -qa|grep -i mysql
```

可以出现已经安装了的MySQL组件

### 2. 停止MySQL服务，删除之前已安装的MySQL

删除命令

```
rpm -e –nodeps 包名
```

### 3. 删除遗留的MySQL文件和依赖库

```
find / -name mysql
rm -rf /var/lib/mysql
```

### 4. 手动删除/etc/my.cnf文件

```
rm -rf /etc/my.cnf
```

### 5. 再次查找是否还有MySQL

```
rpm -qa|grep -i mysql
```

