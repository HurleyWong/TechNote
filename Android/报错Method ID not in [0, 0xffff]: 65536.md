## 报错 Method ID not in [0, 0xffff]: 65536

错误原因：App中所引用的方法已经超过了最大数65536个方法！

### 解决办法

1. 步骤一

    ```xml
     defaultConfig {
     		multiDexEnabled true
     }
    ```

2. 步骤二

    ```xml
     dependencies {
     		implementation 'com.android.support:multidex:1.0.3'
     }
    ```

3. 步骤三

    如果没有重写Application，则可以在AndroidManifest.xml中设置

    ```xml
     <application
             android:name="android.support.multidex.MultiDexApplication" >
     </application>
    ```

    如果自己重写了Application，那么就让自己的App继承至MultiDexApplication

    ```java
    public class App extends MultiDexApplication {
        @Override
        protected void attachBaseContext(Context base) {
            super.attachBaseContext(base);
            MultiDex.install(this);
        }
    }
    ```