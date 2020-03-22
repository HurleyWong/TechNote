## Springboot访问MySQL8的坑

1. 使用的数据库版本与MySQL驱动的版本要一致，例如使用的是MySQL8，那么与之匹配的Maven依赖为

    ```xml
    <dependency>
     	<groupId>mysql</groupId>
     	<artifactId>mysql-connector-java</artifactId>
     	<version>8.0.11</version>
     </dependency>
    ```

2. SpringBoot JPA配置中的Hibernate的dialect的配置，配置为

    ```xml
    spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
     spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
    ```

3. 数据库的时区错误，在spring.datasource.url后添加

    ```xml
    serverTimezone=UTC
    ```

4. MySQL8的jdbc的driver-class是com.mysql.cj.jdbc.Driver，而不是之前的版本对应的com.mysql.jdbc.Driver

