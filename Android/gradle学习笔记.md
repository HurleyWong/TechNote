## gradle学习笔记

Gradle是一种依赖管理工具，基于Groovy语言，面向Java应用为主，它抛弃了基于XML的各种繁琐配置，取而代之的是一种基于Groovy的内部领域特定（DSL）语言。

### Gradle基本概念

1. **app/build.gradle**

    这个文件是app文件夹里的这个Module的gradle配置文件，也可以算是整个项目最主要的gradle配置文件。

    ```
     // 声明是android程序
     apply plugin: 'com.android.application'
     
     android {
       // SDK版本
       compileSdkVersion 25
       // build tools版本
       buildToolsVersion "25.0.2"
     
       defaultConfig {
         // 应用包名
         applicationId "com.standards.gradledemo"
         minSdkVersion 15
         targetSdkVersion 25
         versionName "1.0"
         testInstrumentationRunner "android.support.test.runnner.AndroidJUnitRunner"
       }
     
       buildTypes {
         debug {
           // debug 版本
         }
         release {
           // 是否进行混淆
           minifyEnabled false
           // 混淆文件配置
           progurdFiles getDefaultProguardFile ('proguard-android.txt'), 'proguard-rules.pro'
         }
       }
     
       dependencies {
         // 编译libs目录下的所有jar包
         ...
       }
     
     }
    ```

    - buildToolsVersion需要本地安装该版本才行，如果导入新的第三方库失败的原因之一就是build version版本不对，可以手动更改成本地已有的版本或者打开SDK Manager去下载相应的版本
    - proguardFiles这部分有两段，前一部分代表系统默认的Android程序的混淆文件，该文件已经包含了基本的混淆声明，这个文件的目录在/tools/proguard/proguard-Android.txt；后一部分是项目里的自定义的混淆文件，目录在app/proguard-rules.txt。[如果使用AndroidStudio1.0创建的新项目默认生成的文件名是proguard-rules.pro](http://xn--AndroidStudio1-9v1ww58ipd2cu7wc.xn--0proguard-rules-hm6x840bfqil87cp5mhfrzzau7fbt1l7jhda37zv38u207cb7vb.pro)，这个名字没关系，在这个文件里可以声明一些第三方依赖的一些混淆规则
    - 以上文件里的内容只是基本配置，还有很多自定义部分，如自动打包debug，release，beta等环境、签名、多渠道打包等

2. **devlib/build.gradle**

    每一个Module都需要有一个gradle配置文件，语法都是一样的，唯一不同的开头声明的是apply plugin:’com.android.library’

3. **gradle**

    这个目录下有一个wrapper文件夹，里面可以看到两个文件，主要是gradle-wrapper.properties这个文件的内容：

    ```
     distributionBase=GRADLE_USER_HOME
     distributionPath=wrapper/dists
     zipStoreBase=GRADLE_USER_HOME
     zipStorePath=wrapper/dists
     distributionUrl=https\\://services.gradle.org/distributions/gradle-2.14.1-all.zip
    ```

    这里面声明了gradle的目录与下载路径以及当前项目使用的gradle版本，这些默认的路径一般不会更改，这个文件里指明的gradle版本不对也是很多时候导包不成功的原因之一。

4. **build.gradle**

    这个文件是整个项目的gradle基础配置文件

    ```
     buildscript {
       repositories {
         jcenter()
       }
       dependencies {
         classpath 'com.android.tools.build:gradle:2.2.3'
       }
     }
     
     allprojects {
       repositories {
         jcenter()
       }
     }
     
     task clean(type : Delete) {
       delete rootProject.buildDir
     }
    ```

    内容主要包含了两个方面：一个是声明仓库的源，这里指明的是center()，之前版本是mavenCentral()，jcenter()可以理解成是一个新的中央远程仓库，兼容maven中心仓库，而且性能更优。另一个是声明了android gradle plugin的版本。

5. **settings.gradle**

    这个文件是全局的项目配置文件，里面主要声明了一些需要加入gradle的module，一般是

    ```
     include ':app', ':devlib'
    ```

    文件里的app，devlib都是module，如果还有其他module都需要按照如上格式加进去，也可以通过ctrl+shift+alt+s进入项目配置里面可视化配置。

### Gradle命令详解

- ./gradlew -v：版本号
- ./gradlew clean：清除/app目录下的build文件夹
- ./gradlew build：检查依赖并编译打包 (将debug、release环境都打包)
- ./gradlew assembleDebug：编译并将Debug打包
- ./gradlew assembleRelease：编译并将Release打包