## AndroidStudio自动删除无用包

### 方式1：

先打开要整理的java文件，点击Code→Optimize Imports，即可自动自动删除该java文件中没有用的包（使用快捷键Ctrl+Alt+O可实现同样的效果）

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/20161207110138950.png)

### 方式2：

点击File→Setting，Setting→Editor→General→Auto Import,勾选Optimize imports on the fly，点击apply→OK，然后在编辑java文件时即可自动删除没有用到的包（勾选Add unambiguous imports on the fly可自动导包）

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/20161207110152550.png)