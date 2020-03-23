## Retrofit2实现单文件上传

### 单文件上传

```java
public interface ApiService {
    @Multipart
    @POST("upload")
    Call<ResponseBody> upload(@Part MultipartBody.Part file);
}
```

这个方法不再需要使用@FormUrlEncoded，而是换成了@Multipart，里面的参数只需要增加Part就可以了。

```java
ApiService apiService = RetrofitManager.create(ApiService.class);
File file = new File(文件的路径URI);
RequestBody requestBody = RequestBody.create(MediaType.parse("application/otcet-stream"), file);
MultipartBody.Part body = MultipartBody.Part.createFormData("File", file.getName(), requestBody);

Call<ResponseBody> call = apiService.upload(body);
call.enqueue(new Callback<ResponseBody>() {
    @Override
    public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
        LogUtils.e("success");
    }

    @Override
    public void onFailure(Call<ResponseBody> call, Throwable t) {
        t.printStackTrace();
    }
}
```

