## Linux服务器上部署带有jar包的Java项目

先在Idea中打包好jar包，然后通过FTP协议把jar放置在Linux服务器上。

然后用命令行输入一下命令

```
java -jar jar包的路径
```

运行成功

当断开与服务器的连接后，工程会停止，所以需要使用一下命令

```
nohup java -jar jar包的路径
```

通过指令`ps -ef | grep java` 可以查看进程

