## Linux下使用yum安装jdk

1. 查看系统版本命令

    ```
    cat /etc/issue
    ```

2. 查看yum包含的jdk版本

    ```
    yum search java 或者 yum list java*
    ```

3. 选择版本安装jdk

    ```
    yum install java-1.8.0-openjdk-devel.x86_64
    ```

4. 配置全局变量

    ```
    vi /etc/profile
    ```

    复制以下三行到文件中，按esc退出编辑模式，输入:wq保存退出（这里的JAVA_HOME以自己实际的目录为准）

    ```
    export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.171-8.b10.el6_9.x86_64
    export CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
     export PATH=$PATH:$JAVA_HOME/bin
    ```

    全局变量立即生效

    ```
    source /etc/profile
    ```

5. 查看安装jdk是否成功

    ```
    java -version
    ```

