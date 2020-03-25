## AndroidStudio的目录结构

### Project视图

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Android%20Studio%20Project%E8%A7%86%E5%9B%BE.jpeg)

| 文件（夹）名      | 用途                                                         |
| :---------------- | ------------------------------------------------------------ |
| .gradle           | Gradle编译系统，版本由wrapper指定                            |
| .idea             | Android Studio IDE所需要的文件                               |
| build             | 代码编译后生成的文件存放的位置                               |
| gradle            | wrapper的jar和配置文件所在的位置                             |
| .gitignore        | git使用的ignore文件                                          |
| build.gradle      | gradle编译的相关配置文件，这里区分是Project的和Moudle的      |
| gradle.properties | gradle相关的全局属性设置                                     |
| gradlew           | *nix下的gradle wrapper可执行文件                             |
| graldew.bat       | windows下的gradle wrapper可执行文件                          |
| local.properties  | **本地属性设置（key设置，android sdk位置等属性），这个文件不推荐上传到VCS中** |
| settings.gradle   | 和设置相关的gradle脚本                                       |

### Android视图

![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/Android%20Studio%20Android%E8%A7%86%E5%9B%BE.png)

| 文件（夹）名                 | 用途                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| build                        | 编译后的文件存在的位置（包括最终生成的apk也在这里面）        |
| libs                         | 依赖的库所在的位置（jar和aar)                                |
| src                          | 源代码所在的目录                                             |
| src/main                     | 主要代码所在位置                                             |
| src/main/assets              | android中附带的一些文件                                      |
| src/main/java                | java代码所在的位置                                           |
| src/main/jniLibs             | jni的一些动态库所在的默认位置(.so文件)                       |
| src/androidTest              | 测试代码所在位置                                             |
| src/main/res                 | android资源文件所在位置                                      |
| src/main/AndroidManifest.xml | 清单文件                                                     |
| build.gradle                 | 和这个项目有关的gradle配置，相当于这个项目的Makefile，一些项目的依赖就写在这里面 |
| proguard.pro                 | 代码混淆配置文件                                             |

### 本地依赖

`jar` 包和 `aar` 包生成的路径，只要构建后就会生成：

* .jar：库/build/intermediates/bundles/debug(release)/classes.jar
* .aar：库/build/outputs/aar/libraryname.aar

### jar包和so的使用

so 文件：src/main/jniLibs，或者使用 sourceSet 修改路径

```groovy
dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
}
```

### aar本地加载

`aar`文件是含有`res`资源的`jar`包，这是为了便于安卓开发引用，不用再去拷贝那么多资源文件

第一步：在文件系统操作，将aar拷贝到libs目录下；

第二步：`build.gradle` 配置文件( Module中的)中更改为

```groovy
repositories {
    flatDir {
        dirs 'libs'
    }
} 
dependencies {
    compile(name:'library', ext:'aar')
}
```

这里分别添加了`repositories`与更改了`dependencies`，然后重新编译一次项目就可以正常使用了；

如果是库项目引用 `aar` 文件需要拷贝一份到主项目里面，就相当于原来 ADT 的库项目里包含 `assert` 文件；