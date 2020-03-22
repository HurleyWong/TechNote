## 隐藏Mac终端窗口的"ttys000"

每次打开终端窗口都会显示如下界面的“ttys000”，这究竟是什么原因？

![https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/image-20191015161230255.png](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/image-20191015161230255.png)

### **含义**

ttys000就是TTY名称，而TTY的百度百科解释结果是：

![https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/image-20191015161755748.png](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/image-20191015161755748.png)

如果一直新建终端窗口，那么ttys会从001开始递增计数，似乎是126是上限（没有亲测）。

### **解决方法**

在命令行中输入以下命令即可隐藏显示：

```powershell
touch ~/.hushlogin
```

如果想取消隐藏就删除上面的文件：

```powershell
rm ~/.hushlogin
```

