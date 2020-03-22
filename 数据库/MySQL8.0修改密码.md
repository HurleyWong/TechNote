## MySQL8.0修改密码

因为修改密码过于简单，会不符合MySQL密码的规范，会触发一个提示信息

```
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements
```

对于MySQL5.7的版本，可以使用已下两个命令，即可解决问题

```mysql
mysql> set global validate_password_policy=0;
mysql> set global validate_password_length=1;
```

而MySQL8.0的代码则不一样

```mysql
mysql> set global validate_password.policy=0;
mysql> set global validate_password.length=1;
```

然后再重新设置密码

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY '你的密码';
```