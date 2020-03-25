## Mac和Linux下的Tomcat

## Mac

#### 下载

从Tomcat官网下载Tomcat9的版本，注意Mac请选择Core下的zip版本下载。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-18_23-35-33.png)

#### 解压拷贝

下载后进行解压，然后可以拷贝到自己选择的路径。

#### 执行脚本权限

在命令行下输入执行脚本权限：

```
chmod +x startup.sh
chmod +x shutdown.sh
chmod +x catalina.sh
chmod +x setclasspath.sh
chmod +x bootstrap.jar
chmod +x tomcat-jni.jar
```

最后一行命令有可能出现```No such file or directory```的情况。

#### 启动

命令行进入解压路径的bin路径中，输入```sudo ./startup.sh```，即可启动。如果想要停止，可以输入```sudo ./shutdown.sh```。

## Linux

#### 检测是否有安装了Tomcat

```shell
rpm -qa|grep tomcat
```

如果出现Tomcat的版本，则说明已经安装了Tomcat

#### 查看Tomcat的进程ID

```shell
pa -ef|grep tomcat
```

#### 查看Tomcat目录

```shell
find / -name tomcat
```

#### 关闭Tomcat

1. 首先，进入Tomcat下的bin目录

    ```shell
    cd /usr/local/tomcat/bin
    ```

2. 使用Tomcat关闭命令

    ```shell
    ./shutdown.sh
    ```

3. 查看Tomcat是否已关闭

    ```shell
    pa -ef|grep java
    ```

如果想直接关闭Tomcat，可以使用kill命令，直接杀死Tomcat进程

```shell
kill -9 7010
```

#### 启动Tomcat

```shell
./startup.sh
```



