## MySQL连接报"Communications link failure"的错误

### 方法一

在jdbcURL后加上了`?autoReconnect=true&failOverReadOnly=false`

据说这个方法在MySQL4.x的版本可以用，但是如果是MySQL5版本及以上就不行了

### 方法二

在MySQL的my.ini里面加上这两个参数

```ini
wait_timeout=2147483
interactive_timeout=2147483
```

如果在配置不改变的情况下，如果连续8小时内都没有访问数据库的操作，再次访问MySQL数据库的时候，MySQL数据库就会拒绝访问

### 方法三

把jdbcURL的ip地址链接改成localhost

因为项目是部署在云服务器上的，所以用localhost也可以访问云服务器上的数据库

