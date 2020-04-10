## R语言开发之零碎问题

这篇文章主要收集在使用R语言开发过程中碰到的零碎问题。

### RStudio出现中文乱码

* 可以在`preference`或者`setting`中将`code`栏中的`Saving`tab下的**Default text encoding**设置为**UTF-8**之外
* 在菜单栏设置`file->reopen with encoding->utf8`

### 查看数据类型

使用命令`class(xxx)`即可查看该数据类型

### 读取数据只取某几列或者某几行

`data[, 2]`表示data中的第2列

`data[1, ]`表示data中的第1行

`data[, 2:4]`表示data中第2到4列

`data[2:4, ]`表示data中第2到4行

如果要取不是连续的行，比如读取第1、4、5行，则可用以下命令`data[c(1, 4, 5), ]`















