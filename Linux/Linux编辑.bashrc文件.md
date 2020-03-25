##   Linux编辑.bashrc文件

因为要在学校的服务器上配置数据库的一些信息，所以需要在Linux命令行中进行一些配置环境的操作。但是因为对Linux命令并不十分熟悉，所以记录一下操作的过程。

1. 使用如下命令修改.bashrc文件

    <!-- more -->

    ```
    gedit ~/.bashrc
    ```

    然后在该文件的底部添加以下一行：

    ```
    export CLASSPTH=/usr/share/java/mysql-connector-java.jar:$CLASSPATH
    ```

    ![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-15_21-04-26.png)

2. 使用以下命令更改使其生效

    ```
    source ~/.bashrc
    ```

    ![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-15_21-25-59.png)

