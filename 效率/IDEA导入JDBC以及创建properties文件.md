## IDEA导入JDBC以及创建properties文件

### IDEA导入JDBC

1. 在官网 https://dev.mysql.com/downloads/connector/j/ 下载JDBC驱动程序，在Operating System栏中可以选择Platform independent
2. 解压压缩包
3. 打开IDEA，打开Project Structure，Modules然后选中Dependencies，点击底部+号，选第一个jars or directories，选中解压的jar包文件，例如mysql-connector-java-8.0.18.jar，然后确定
4. 查看External libraries，发现多了上面这个jar包文件

### IDEA创建properties文件

new一个Resource Bundle文件，然后输入文件名，确定即可