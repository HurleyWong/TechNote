## MySQL max_allowed_packet过小引起的问题

报错如下

```
com.mysql.jdbc.PacketTooBigException: Packet for query is too large (5366885 > 4194304)
```

通过如下命令增大max_allowed_packet的值，解决值过小导致的问题

```mysql
set global max_allowed_packet = 10*1024*1024;
```

注意事项：

- max_allowed_packet的值最大为1G，设置的值必须为1024的倍数

- 设置完后，需要退出mysql，重新进入才能看到设置后的值

    mysql> show variables like 'max_allowed_packet'; mysql> set global max_allowed_packet = 10*1024*1024;

设置为10M，退出mysql，然后重新进入，调用

```mysql
show variables like 'max_allowed_packet';
```

查看是否修改成功

```mysql
mysql> show variables like 'max_allowed_packet';
```

### Linux系统

如果是Linux系统，进入到mysql安装目录/usr/local/mysql下，找到my.cnf，用vim打开，增加一行

```mysql
max_allowed_packet = 20M
```

然后通过service mysql restart重启即可

