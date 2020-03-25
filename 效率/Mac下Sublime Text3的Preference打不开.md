## Mac下Sublime Text3的Preference打不开

### 原因

原因应该是安装了多语言，导致出现的首选项等同于Preference从而产生了冲突。

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-20_21-45-26.png)

### 解决方法

1. 因为其实可以通过点击首选项进行设置，不必点击Sublime Text3然后再点击Preference，所以其实并不影响使用。
2. 如果需要让Preference发挥作用，则可以打开Finder，搜索ZZZZZZZZ-Localization，将这个文件夹中的Main.sublime-menu文件放入废纸篓即可（想要恢复的话，将该文件还原到该位置即可）。

