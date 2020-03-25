## Mac+Hexo+Github Pages搭建博客

### 为什么重新部署博客

以前通过Github上Fork其他大牛的仓库，搭建过一个基于Jekyll的博客，但是个人感觉那个博客过于简陋，且某些方面(例如鼠标滑动方面会与Safari有冲突)，导致在这个清明假期终于狠下心来，决定迁移出博客文章，并且重新部署过一个自己满意的博客。

### Hexo+Github博客

现在主流的基于Github的博客都是根据Jeklly和Hexo两种搭建的方式，因为之前我使用的是基于Jeklly的方式并且不太满意，所以现在决定搭建一个基于Hexo的博客。

选择搭建Github博客的方式是托管方便，并且Github社区活跃，有很多相似的内容。

### 环境搭建

#### 安装Node.js和npm和Git

如何安装Node.js和npm和Git在这里就不综述了，其实在Mac里通过命令行就可以很方便的安装。安装好后可以在命令行中通过以下命令去检测输出的版本。

```
node -v
v11.10.0
npm -v
6.7.0
git --version
git version 2.17.2 (Apple Git-113)
```

#### 安装Hexo

安装时注意权限问题，加上sudo，其中-g表示全局安装。这里会需要输入管理员密码。

```
sudo npm install -g hexo
```

#### 博客初始化

创建一个空的，用于储存博客文章的文件夹，命名随意。然后通过cd进入到该文件夹中。

```
cd HurleyBlog
```

执行下述命令初始化本地博客，下载一系列文件。

```
hexo init
```

执行下述命令安装npm。

```
sudo npm install
```

执行下述命令生成本地网页文件并开启服务器，然后通过localhost:4000查看本地博客。

```
hexo g
hexo s
```

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Mac%2BHexo%2BGitHub%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B%20-%20%E7%9F%A5%E4%B9%8E.jpg)

#### 本地博客关联Github

注册并登陆GitHub账号后，新建仓库，名称必须为`user.github.io`，如`HurleyJames.github.io`。

进入博客文件夹中，用编辑器打开_config.yml，然后在最底部配置deploy。

```yaml
deploy:
	type: git
	repository: https://github.com/HurleyJames/HurleyJames.github.io.git
	branch: master
```

其中将repository中`HurleyJames`改为自己的用户名，注意type、repository、branch后均有空格。通过如下命令在myblog下生成静态文件并上传到服务器。

```
hexo g
hexo d
```

若执行`hexo g`出错则执行`npm install hexo --save`，若执行`hexo d`出错则执行`npm install hexo-deployer-git --save`。错误修正后再次执行`hexo g`和`hexo d`上传到服务器。

`hexo d`执行成功后便可通过HurleyJames.github.io访问博客，看到的内容和localhost:4000相同。

#### 添加SSH Key到Github

这里不再赘述。

#### 更换Hexo主题

可以在Hexo的官网中挑选自己喜欢的主题，我用的是Melody这个主题，因为它的色调我比较喜欢。

```
git clone -b master https://github.com/Molunerfinn/hexo-theme-melody themes/melody
```

然后就是参考[hexo-theme-melody](<https://molunerfinn.com/hexo-theme-melody-doc/zh-Hans/#%E7%89%B9%E6%80%A7>)去根据这个主题的官方文档去配置该主题

#### 注意

因为每次通过命令行`hexo d`重新部署后，都会删除CNAME文件，导致无法通过自己购买的域名去访问博客。解决方法就是通过把CNAME文件放在博客文件夹目录下的source文件夹中，每次重新部署并不会删除source内的文件，这样即可解决问题。