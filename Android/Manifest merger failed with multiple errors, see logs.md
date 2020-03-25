## Manifest merger failed with multiple errors, see logs

在Android运行时，有时build会报以下错误，然后就没有其它的提示信息了。

```Error:Executionfailedfortask':test:processDebugManifest'.>Manifest merger failed with multiple errors, see logs```

### 解决方法

进入AndroidStudio内部的命令行(一般在底部栏)，输入命令：

* Windows下输入命令：`gradlew processDebugManifest —stacktrace`

* Mac下输入命令：`./gradlew processDebugManifest —stacktract`

    注意：Mac系统下直接输入该命令，会提示```-bash: ./gradlew: Permission denied```，即没有足够的权限

    因此要先输入```chmod +x gradlew```，然后再输入Mac下的命令即可，这时候稍等一会，命令行就会打印出相应的log信息，根据提示操作即可。