## Retrofit2&OkHttp3添加统一的请求头Header

在使用Retrofit时，有时候需要设置Set-Cookie等请求头，如果每一个url都需要，那么直接来个拦截器就好了。

```java
/**
 * 添加Header拦截器
 */ 
private static final Interceptor mHeaderInterceptor = chain -> {
    Request request = chain.request()
        .newBuilder()
        .addHeader("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8")
        .addHeader("Accept-Encoding", "gzip, deflate")
        .addHeader("Connection", "keep-alive")
        .addHeader("Accept", "*/*")
        .build();
    return chain.proceed(request);
};

/**
 * 对OkHttpClient进行配置
 */
private static OkHttpClient getOkHttpClient() {
    if (mOkHttpClient == null) {
        synchronized (RetrofitManager.class) {
            Cache cache = new Cache(new File(App.getAppContext().getCacheDir(), "HttpCache"), 1024 * 1024 * 100);
            if (mOkHttpClient == null) {
                mOkHttpClient = new OkHttpClient.Builder()
                    .cache(cache)
                    .connectTimeout(CONNECT_TIMEOUT, TimeUnit.SECONDS)
                    .readTimeout(READ_TIMEOUT, TimeUnit.SECONDS)
                    .writeTimeout(WRITE_TIMEOUT, TimeUnit.SECONDS)
                    .addInterceptor(mRewriteCacheControlInterceptor)
                    .addInterceptor(mLoggingInterceptor)
                    .cookieJar(new CookiesManager())
                    .build();
            }
        }
    }
    return mOkHttpClient;
}
```

让网络请求附上Token：

```java
Interceptor mTokenInterceptor = new Interceptor() {
    @Override
    public Response intercept(Chain chain) throws IOException {
        if (你的Token == null || alreadyHasAuthorizationHeader(originalRequest)) {
            return chain.proceed(originalRequest);
          }
        Request authorised = originalRequest.newBuilder()
            .header("Authorization", 你的Token)
            .build();
        return chain.proceed(authorised);
    }
}
```

创建Retrofit

```java
public static <T> T create(Class<T> clazz) {
    Retrofit retrofit = new Retrofit.Builder()
        .baseUrl(UrlContainer.baseUrl)
        .client(getOkHttpClient())
        .addConverterFactory(GsonConverterFactory.create())
        .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
        .build();
    return retrofit.create(clazz);
}
```