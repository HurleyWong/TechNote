## AndroidStudio3.0新功能

### distributionUrl

Plugin 3.0.0+需要配置Gradle的最小版本是4.1，我们可以通过File -> Project Structure -> Project的方式设置Android Plugin的版本，或者修改gradle.properties文件的内容，添加distributionUrl属性：

```
distributionUrl=https\\://services.gradle.org/distributions/gradle-4.1-all.zip
```

### Google’s Maven repository

新版Android Studio工具默认使用Google’s Maven Repository用于下载依赖Android Support Library，替代了Android SDK Manager的本地依赖方式。所以，需要在工程根目录下的build.gradle文件中添加google()一行代码：

```
allprojects {
  repositories {
    google()
  }
}
```

### buildToolsVersion

```
android {
  compileSdkVersion 26
  //remote buildToolsVersion
  buildToolsVersion "25.0.2"
}
```

### each()和outputFile()

Plugin 3.0.0版本移除了一些用于编译配置的API，其中比较常见的就是each()和outputFile()，两个常用于修改输出**Apk文件名**和**路径**的方法。

自定义输出APK文件名（3.0版本之前）可以这样完成：

```
android {
  android.applicationVariants.all { variant ->
  	variant.output.each { output ->
      output.outputFile = new File(output.outputFile.parent, rootProject.getName()
      + "-" + buildType.name
      + "-" + releaseTime()
      + "-v" + defaultConfig.versionName
      + "-" + defaultConfig.versionCode
      + ".apk");
  	}
  }
}
```

但是使用Plugin 3.0.0时就会出现编译错误，我们需要修改each()和outputFile()方法为all()和outputFileName，比如：

```
android {
  android.applicationVariantsl.all { variant ->
    variant.outputs.all {
      outputFileName = rootProject.getName()
      + "-" + buildType.name
      + "-" + releaseTime()
      + "-v" + defaultConfig.versionName
      + "-" + defaultConfig.versionCode
      + ".apk";
    }
  }
}
```