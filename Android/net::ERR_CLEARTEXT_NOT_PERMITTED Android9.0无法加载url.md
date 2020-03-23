## net::ERR_CLEARTEXT_NOT_PERMITTED Android9.0无法加载url

从Andriod 9.0（API28）开始，默认情况下禁用明文支持。因此http的url均无法在webview中加载。

解决方法：

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ...>
    <uses-permission android:name="android.permission.INTERNET" />
    <application
        ...
        android:usesCleartextTraffic="true"
        ...>
        ...
    </application>
</manifest>
```

主要是加上`android:usesCleartextTraffic="true"`



