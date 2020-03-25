## Androidx和Android Support库共存问题

最近在gradle里更新一些第三方框架的版本。之后运行的时候就无法build成功，日志提示需要添加```tool:replace="android:appComponentFactory"```，之后按照网上查找的继续添加```android:appComponentFactory="任意字符"```(这里的任意字符可以为任意字符串)。

运行后仍然无法build成功，提示让我移除```'META-INF/androidx.localbroadcastmannager_localbroadcastmanager.version'```，之后运行后，仍然不停地让我提示移除各种androidx的东西。

后来我认为Androidx和Android Support库无法共存，所以要么全部转换为Androidx，要么就移除Androidx。

### 全部转换成Androidx

1. 统一build tools、gradle和依赖的Android Support库的版本
2. 选择工程，然后右键->Refactor->Migrate to Androidx，然后Do Refactor，工程就会全部转换成Androidx工程

### 全部转换成Android Support

1. 查看到底是哪些第三方库依赖了Android，Windows下执行```gradlew :app:dependencies```，Mac下执行```./gradlew :app:dependencies```(注意，Mac下直接执行该命令会提示```-bash: ./gradlew: Permission denied```，这时候需要先输入```chmod +x gradlew```就可以了)，然后稍微等待，就可以看到树形目录(比较多)，就可以看到到底是哪些库依赖了Androidx。
2. 去查看这些第三方库的Github或者官方文档，查看版本，到底是在哪个版本开始依赖了Androidx，然后将版本回退即可。
3. 然后重新build一下，并且在External Libraries里输入androidx进行查找，如果没有匹配的项，则说明该工程已经全部移除Androidx。