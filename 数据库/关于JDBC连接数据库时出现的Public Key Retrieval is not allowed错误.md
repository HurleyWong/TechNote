## 关于JDBC连接数据库时出现的Public Key Retrieval is not allowed错误

当使用MyBatis框架时，添加Mapper，在Mapper接口中通过注解配置了SQL语句，一步步的构建完成，前面都顺利执行没有抛出异常，当通过SqlSession拿到Mapper执行SQL语句的时候，抛出了Public Key Retrieval is not allowed异常。

### 三种解决办法

1. MySQL5以及之前的版本使用的是旧版的驱动"com.mysql.jdbc.Driver"，MySQL6以及之后的版本需要更新到新版的驱动，对应的Driver是"com.mysql.cj.jdbc.Driver"，这个其实会有提示信息提示前者已经deprecated。
2. 在连接数据库的url中，加上allowPublicKeyRetrieval=true参数
3. 修改default_authentication_plugin设置，在my.ini中增加[mysqld]default_authentication_plugin=mysql_native_password，然后在mysql命令行执行ALTER USER 'username'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';最后在url中添加时区参数serverTimezone=Asia/Shanghai。