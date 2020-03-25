## Hexo怎么避免README文件以及CNAME文件的覆盖

### 避免README.md文件的覆盖

因为Github的版本库一般都会附上README.md的说明，但是Hexo默认会把所有的md文件解析成html文件，所以即使编写了README.md文件，也会在下一次部署博客时被删去。

解决方法：

在博客文件夹的根目录下的配置文件_config.yml中配置一下`skip_render`选项，如下所以：

```
skip_render: README.md
```

这样就可以确保README.md文件不被渲染了。

### 避免CNAME文件被删除的四种方法

* 每次`hexo d`之后，都重新去Github仓库目录下新建CNAME文件

* 在 `hexo g` 之后， `hexo d` 之前，把CNAME文件复制到 “\public\” 目录下面，里面写入你要绑定的域名。

* 将需要上传至github的内容放在source文件夹，例如CNAME、favicon.ico、images等，这样在`hexo d`之后就不会被删除了。

* 通过安装插件实现永久保留

    `npm install hexo-generator-cname --save`

    之后在_config.yml中添加

    ```
    Plugins:
    - hexo-generator-cname
    ```

    需要注意的是：如果是在github上建立的CNAME文件，需要先clone到本地，然后安装插件，在deploy上去即可。CNAME只允许一个域名地址。