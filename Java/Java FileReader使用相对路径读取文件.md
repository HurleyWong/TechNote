## Java FileReader使用相对路径读取文件

### 原因

编程时对文件进行操作时，如果使用**绝对路径**则需要经常更改，因此使用**相对路径**是一个不错的选择。但是有时在使`./`或者`../`的时候会出现未能找到文件的错误。

### 解决方案

1. 使用`System.getProperty("user.dir")`获取当前程序运行的工作根目录
2. 使用`File.separator`表示目录的分隔符，此操作需要就`import java.io.File`

``````Java
String root = System.getProperty("user.dir");
String fileName = "xxx.txt";
String filePath = root + File.separator+"experiment"+File.separator+fileName;
FileReader fileReader = new FileReader(filePath);
``````

这样就可以避免出现未找到文件的错误。