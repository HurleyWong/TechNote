## Android P http网络请求问题

Google表示，为保证用户数据和设备的安全，针对下一代 Android 系统(Android P) 的应用程序，将要求默认使用加密连接，这意味着 Android P 将禁止 App 使用所有未加密的连接，因此运行 Android P 系统的安卓设备无论是接收或者发送流量，未来都不能明码传输，需要使用下一代(Transport Layer Security)传输层安全协议，而 Android Nougat 和 Oreo 则不受影响。

所以在Android P 使用HttpUrlConnection进行http请求时会出现以下异常：

`java.io.IOException: Cleartext HTTP traffic to **** not permitted`

使用OkHttp请求则会出现：

`java.net.UnknownServiceExceptionn: CLEARTEXT communication ** not permitted by network security policy`

在Android P 系统，如果应用使用的是非加密的明文流量的http网络请求，则会导致该应用无法进行网络请求，https则不会受影响。同样，如果应用嵌套了webview，则webview也只能使用https请求。

### 解决方案

* App改用https请求

* `targetSdkVersion`降到版本27以下

* 在res目录下新增一个`xml`目录，然后创建名为：`network_security_config.xml` 文件(名字可自定义)

    ```xml
    <?xml version="1.0" encoding="utf-8"?> 
    <network-security-config> 
      <base-config cleartextTrafficPermitted="true" /> 
    </network-security-config>
    ```

    然后在AndroidManifest.xml文件下的application标签下添加以下属性：

    ```xml
    <application
             android:networkSecurityConfig="@xml/network_security_config"/>
    ```

    