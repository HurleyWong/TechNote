## Android通过友盟多渠道打包apk

### 1. 在AndroidManifest.xml配置友盟key的相关信息

```xml
<meta-data
  android:name="UMENG_APPKEY"
  android:value="xxx"/>
<meta-data
  android:name="UMENG_CHANNEL"
  android:value="${UMENG_CHANNEL_VALUE}"/>
```

其中的${UMENG_CHANNEL_VALUE}能够通过动态的根据渠道改变

### 2. 在build.gradle文件里配置具体的渠道号

```
productFlavors {
  xiaomi {}
  offical {}
  baidu {}
  googleplay {}
  qihu360 {}
  huawei {}
  sougou {}
  wangyi {}
  uc {}
  meizu {}
  ali {}
  wandoujia {}
  anzhishichang {}
  lianxiang {}
  yingyongbao {}
  oppo {}
  sametest {}  
}

productFlavors.all {
  flavor -> flavor.manifestPlaceholders = [UMENG_CHANNEL_VALUE: name]
}
```

完成以上步骤就已经可以根据不同的渠道进行打包了。但是为了便于区分，我们要对打包好的apk根据不同的渠道来进行命名。所以接下来第三步。

### 3. 根据不同的渠道对apk进行命名

```
buildTypes {
  release {
    // 批量修改apk名字
    applicationVariants.all { variant ->
      variant.outputs.all { output ->
        def outputFile = output.outputFile
        if (outputFile != null && outputFile.name.endsWith("apk")) {
          // 获取签名的名字
          variant.signingConfig.name
          // 要被替换的源字符串
          def sourceFile = "-${variant.flavorName}-${variant.buildType.name}"
          // 替换的字符串
          def replaceFile = "-v${variant.versionName}-${variant.flavorName}_${variant.buildType.name}"
          outputFileName = output.outputFile.name.replace(sourceFile, replaceFile)
        }
      }
    }
  }
}
```

### 4. 打包

打包的方式有几种，可以直接通过AndroidStudio的Generate Signed APK进行打包。将打包后生成的apk文件直接拖进AndroidStudio，查看其AndroidManifest.xml里的${UMENG_CHANNEL_VALUE}是否已经被替换成了该渠道名。如果替换，则说明打包成功。