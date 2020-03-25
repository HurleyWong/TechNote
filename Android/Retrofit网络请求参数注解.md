## Retrofit网络请求参数注解

### Retrofit使用步骤

1. 添加Retrofit库依赖
2. 创建接收服务器返回数据的类
3. 创建用于描述网络请求的接口
4. 创建Retrofit实例
5. 创建网络请求接口实例并配置网络请求参数
6. 发送网络请求（异步 / 同步）
7. 处理数据

### 注解类型

![img](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/20171231162846585.png)

### GET

- http://localhost/api/leeds

    ```
     //最简单的get请求(没有任何参数)
     @GET("leeds")
     Call<Leeds> getItem();
    ```

- http://localhost://api/leeds/{userId}

    ```
     //简单的get请求(URL中带有参数)
     @GET("leeds/{userId}")
     Call<Leeds> getItem(@Path("userId") String userId);
     
     //简单的get请求(URL中带有两个参数)
     @GET("leeds/{userId}")
     Call<Leeds> getItem(@Path("userId") String userId, @Path("type") String type);
    ```

- https://localhost/api/leeds?userId={userId}

    ```
     //参数才url问号之后
     @GET("leeds")
     Call<Leeds> getItem(@Query("userId") String userId);
    ```

- http://localhost/api/leeds?userId={userId}&type={type}

    ```
     @GET("leeds")
     Call<Leeds> getItem(@Query("userId") String userId, @Query("type") String type);
     
     @GET("leeds")
     Call<Leeds> getItem(@QueryMap Map<String, String> map);
     
     @GET("leeds")
     Call<Leeds> getItem(@Query("userId") String userId, @QueryMap Map<String, String> map);
    ```

    - http://localhost/api/leeds/{userId}

        ```
         //需要补全URL，post的数据只有一条reason
         @FormUrlEncoded
         @POST("leeds/{userId}")
         Call<Leeds> postResult(@Path("userId") String userId, @Field("reason") String reason);
        ```

    - http://localhost/api/leeds/{userId}?token={token}

        ```
         //需要补全URL，问号后需要加token，post的数据只有一条reason
         @FormUrlEncoded
         @POST("leeds/{userId}")
         Call<Leeds> postResult(@Path("userId") String userId, 
                                @Path("token") String token,
                                @Path("reason") String reason);
         
         //post一个对象
         @POST("leeds/{userId}")
         Call<Leeds> postResult(@Path("userId") String userId,
                                @Query("token") String token, 
                                @Body Leeds leeds);
         
         //用不同的注解post一个实体
         @POST("leeds/{userId}")
         Call<Leeds> postResult(@Part("entity") Leeds leeds);
        ```

        - Path是网址中的参数，例如leeds/{userId}
        - Query是问号后面的参数，例如leeds/{userId}?token={token}
        - QueryMap相当于多个@Query
        - Field用于Post请求，提交单个数据，然后要在上面加@FormUrlEncoded
        - Body相当于多个@Field，以对象的方式提交
        - @Streaming用于加载大文件
        - @Header  | @Headers 加请求头

        ### 总结

    ### POST