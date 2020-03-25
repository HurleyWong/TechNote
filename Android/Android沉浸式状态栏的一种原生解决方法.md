## Android沉浸式状态栏的一种原生解决方法

### 前提

Android沉浸式状态栏的特性是Android4.4之后的版本才支持，需要最少API19才可以使用。

### 使用方法

```Java
//透明状态栏
getWindow().addFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_STATUS);
//透明导航栏
getWindow().addFlags(WindowManager.LayoutParams.FLAG_TRANSLUCENT_NAVIGATION);
```

以上两行代码可以实现沉浸式通知栏，但是内容会与状态栏重叠在一起。所以还需要添加一下代码：

```xml
android:fitSystemWindow = "true";
android:clipToPadding = "true";
```

