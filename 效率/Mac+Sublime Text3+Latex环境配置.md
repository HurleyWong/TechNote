## Mac+Sublime Text3+Latex环境配置

### 安装步骤

1. 下载安装MacTex，文件较大，有3个多G。但是安装是直接安装，不需要任何配置。

2. 安装Sublime Text3，然后安装插件LatexTool。具体步骤如下：

    1. 安装Package Control

    2. 安装LatexTool插件

        按下`shift + ⌘ + P`，输入`Install Package`，然后再输入`LatexTools`，出现LatexTools插件，双击安装即可。

3. 配合Preview使用

    1. 很多网络上的教程描述要用skim搭配Sublime Text3使用，通过skim查看编译后生成的PDF。但是skim这个软件很久没有更新，现在已经不支持macOS 10.15 Catalina版本。好在其实macOS自带的Preview也可以预览PDF。

    2. 只需要在Sublime的Preference中点击settings，然后在右侧的user栏中的代码中按照下图加上`"viewer": "preview"`即可。

        ![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-21_15-22-10.png)

    3. 输入完毕后，按`cmd + B`即可编辑，build completed后即可出现Preview预览生成的PDF文件。

### 配置中文

因为pdfLatex对于Unicode十分不友好，编译中文很麻烦。但是在代码的开头加上以下代码，然后再添加一个package即可编译中文。

如下图所以，在文件的顶部添加`%!TEX program = xelatex`，然后在package中添加`\usepackage[UTF8]{ctex}`，即可编译中文。

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Snipaste_2019-10-21_15-54-11.png)