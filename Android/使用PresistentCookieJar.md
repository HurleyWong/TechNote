## 使用PersistentCookieJar

结合RxJava和Retrofit一起使用PersistentCookieJar

```java
PersistentCookieJar cookieJar = new PersistentCookieJar(new SetCookieCache(), SharedPrefsCookiePersistor(App.getContext());
// 实例化OkHttp
OkHttpClient client = new OkHttpClient.Builder()
		.retryOnConnectionFailure(true)
		.connectTime(10, TimeUnit.SECONDS)
		.readTimeout(15, TimeUnit.SECONDS)
		.writeTimeout(45, TimeUnit.SECONDS)
		// 添加拦截器
		.addInterceptor(某个拦截器)
		.cookieJar(cookieJar)
		.build();

// 实例化Retrofit
Retrofit retrofit = new Retrofit.Builder()
		.baseUrl(baseUrl)
		.client(client)
		.addConverterFactory(GsonConverterFactory.create())
		.addCallAdapterFactory(RxJava2CallAdapterFactory.create())
		.build();
```

主要是new一个PersistentCookieJar然后在创建OkHttp实例的时候用.cookieJar添加该实例即可，最后在创建Retrofit时结合OkHttp

