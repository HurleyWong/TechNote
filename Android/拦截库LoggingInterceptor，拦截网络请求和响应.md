## 拦截库LoggingInterceptor，拦截网络请求和响应

### 导入步骤

* 在build.gradle(app)文件中，添加

    ```groovy
    dependencies {
        implementation ('com.github.ihsanbal:LoggingInterceptor:3.0.0') {
            exclude group: 'org.json', module: 'json'
        }
    }
    ```

* 在build.gradle(module)文件中，添加

    ```groovy
    allprojects {
        repositories {
            jcenter()
            //添加如下代码
            mavenCentral()
            maven {
                url "https://jitpack.io"
            }
        }
    }
    ```

### 使用方法

* 创建OkHttpClient.Builder对象设置拦截属性，然后创建OkHttpClient对象，最后配置在Retrofit对象中

    ```java
    OkHttpClient.Builder builder = new OkHttpClient.Builder();
    builder.addInterceptor(new LoggingInterceptor.Builder()
            .loggable(BuildConfig.DEBUG)
            .setLevel(Level.BASIC)
            .log(Platform.INFO)
            .request("Request")
            .response("Response")
            .build());
    client = builder.build();
    retrofit = new Retrofit.Builder()
        .baseUrl(UrlHelper.BASE_URL)
        .client(client)
        .addCallAdapterFactory(RxJavaCallAdapterFactory.create())
        .addConverterFactory(GsonConverterFactory.create())
        .build();
    ```

* 在logcat中的Info中就可以看到网络请求和响应的JSON数据



