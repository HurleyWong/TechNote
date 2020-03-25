## Hexo更新代码高亮以及Github Page Build Warning

## 更新代码高亮

我的博客使用的主题是[hexo-theme-melody](https://molunerfinn.com/hexo-theme-melody-doc/zh-Hans/#特性)，这是一款非常清新简约但是基本功能都具备的基于Hexo的博客主题，但是其可供选择的代码高亮主题十分有限。我一直比较青睐的代码主题就是Sublime  Text3的**Monokai Sublime**。

好在可以通过自定义修改`highlight.styl`的方式去自己仿造一个Monokai的代码高亮主题。

### 方法

首先进入博客的根目录，进入`themes/melody/source/css/_highlight`文件夹中（不同主题的路径是不一样的，但是都是需要找到定义theme和highlight的配置文件），这里主要有三个文件。其中`highlight.styl`和`theme.styl`是我们需要打开的文件。

#### `theme.styl`文件

可以仿照文件中原有的代码，添加一个新的`highlight_theme`。

```
 if $highlight_theme == "monokai"
   $highlight-background = #23241F
   $highlight-current-line = #3E3D32
   $highlight-selection = #49483E
   $highlight-foreground = #F8F8F2
   $highlight-comment = #75715E
   $highlight-red = #F92672
   $highlight-orange = #FD971F
   $highlight-yellow = #E6DB74
   $highlight-green = #A6E22E
   $highlight-aqua = #A1EFE4
   $highlight-blue = #66D9EF
   $highlight-purple = #AE81FF
   $highlight-gutter = {
     color: #37474F,
     bg-color: $highlight-background
   }
 dig hurley.fun
 dig hurleyjames.github.io
```

因为我的域名是在**namecheap.com**上购买的，所以在该网站中登录自己的账号后，进入Domain List，选择Advanced DNS，然后将A Record添加或者修改成与`HurleyJames.github.io`一样的地址即可。

分别执行以上两行命令，可以看到得到的结果的`ANSWER SECTION`中返回IP地址是不同的。所以要把`hurley.fun`中的地址改成和`HurleyJames.github.io`的地址一样。

因为我的博客原地址是`HurleyJames.github.io`，然后指向`hurley.fun`，所以对这两个网址执行`dig`命令。

所以可以在终端中使用`dig`命令查看具体指向的IP地址。

其中最重要的一句就是**The custome domain for your Github Pages site is pointed at an outdated IP address**。即我的Github Pages所指向的IP地址过期了。

最近发现每个部署一次博客，邮箱都会收到一封邮件如下截图所示： ![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/IMG_6B687C9967AF-1.jpeg)

## Page build warning

最后在博客根目录的`_config.yml`文件中，将`highlight_theme: default`修改成自己刚刚自定义的高亮主题名称`highlight_theme: monokai`即可。

`highlight.styl`文件中的代码较多，其实可以根据搜索颜色代码找到对应的代码部分所对应的颜色，然后自行修改。

#### `highlight.styl`文件

上述的RGB颜色值可以从已有的Sublime Text3配置文件中找到，也可以在[highlightjs.org]()网站中找到**Monokai Sublime**，然后使用取色软件（例如Mac端的Drop）对代码高亮的部分进行取色，得到每一项的RBG值。