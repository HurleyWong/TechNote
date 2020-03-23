## Error while Installing APKs

今天开发时，因为gradle加上代码重构等原因，我先是拷贝了一份代码，然后对改动后的代码运行过之后，再运行拷贝的代码，就发现了问题。

在运行时，就提示warning:uninstall will remove the application data!

然后点击确认卸载后，发现仍然无法装上应用，提示如下

```
Unknown failure (at android.os.Binder.execTransact)
Error while Installing APKs
```

即使自己手动卸载后也仍然无法正常安装上应用。

后来就只好在网上查找，终于找到了有用的方法（不一定是最好的方法）

打开设置（mac打开preferences），搜索出Instant Run，把Enable Instant Run to选项去掉勾选再重新运行一遍，就可以正常安装了。

但是有一次即使这样做了，也无法正常安装。后来发现，重启Android手机即可安装了。

