	## SpringBoot打包web项目成war包部署到Tomcat服务器中

### 将项目打包成war包

首先，修改pom.xml文件，指定打包方式为`<packaging>war</packaging>`，然后修改pom.xml修改SpringBoot内置的Tomcat依赖，指定scope为`provided`

<!-- more -->

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
  <scope>provided</scope>
</dependency>
```

接着，创建一个初始化文件对项目进行初始化，可以命令为`XXXServletInitializer.java`，核心代码如下：

```java
public class XXXServletInitializer extends SpringBootServletInitializer {
  @Override
  protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
    return builder.sources(XXXApplication.class);
  }
}
```

 在控制台中执行命令`mvn clean install -Dmaven.test.skip=true`将项目打包成war包，执行后可以在target目录下找到war包。

### 将war包部署到Tomcat

将war包复制到Tomcat的webapps文件下，然后进入`Tomcat\bin`目录下执行`./startup.sh`即可。

当然，也可以使用jar包的运行方式启动war包。

* 前台运行

    ```shell
    java -jar XXX.war
    ```

    后面的是war包所在的路径，可以通过关闭终端或者`ctrl+C`来停止运行

* 后台运行

    ```shell
    nohup java -jar XXX.war >temp.txt &
    // nohup是不挂断运行命令，当用户退出或者关闭终端时，程序仍然运行
    // 这种方法会把日志文件写入到指定的temp.txt文件中
    // 在哪个目录下运行的该日志文件就会在哪个目录下，没有指定具体文件则会自动创建(nohup.out)
    // &表示后台运行
    ```

### 修改生成的war包名称

可以通过手动重命名进行修改，也可以在pom.xml中使用finalName指定实现

```xml
<build>
	<finalName>XXX</finalName>
  <plugins>
  	<plugin>
    	<groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>
  </plugins>
</build>
```

### 相关Linux命令

* jobs和fg

    ```shell
    $ jobs
    // 显示出所有后台执行的作业，并且每个作业前面都有个编号
    [1]+  Running    nohup java -jar hello-0.0.1-SNAPSHOT.jar > temp.txt 2>&1 &
    // 如果想把某个作业调回前台控制，可以通过 fg + 编号
    $ fg 1
    ```

* 查看某端口占用的线程的pid

    ```shell
    netstat -nlp |grep :8080
    ```

* kill

    ```shell
    kill pid
    ```

    