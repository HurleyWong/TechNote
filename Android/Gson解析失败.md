## Gson解析失败

报错 Use JsonReader.setLenient(true) to accept malformed JSON at line 1 column 1 path $

因为某些接口的问题，导致返回JSON异常信息。

所以有两种解决方式：

### 1. 重写一个GsonConverterFactory类

例如可以命名为LenientGsonConverterFactory类

```java
public class LenientGsonConverterFactory extends Converter.Factory {
 
    /**
     * Create an instance using a default {@link Gson} instance for conversion. Encoding to JSON and
     * decoding from JSON (when no charset is specified by a header) will use UTF-8.
     */
    public static LenientGsonConverterFactory create() {
        return create(new Gson());
    }
 
    /**
     * Create an instance using {@code gson} for conversion. Encoding to JSON and
     * decoding from JSON (when no charset is specified by a header) will use UTF-8.
     */
    public static LenientGsonConverterFactory create(Gson gson) {
        return new LenientGsonConverterFactory(gson);
    }
 
    private final Gson gson;
 
    private LenientGsonConverterFactory(Gson gson) {
        if (gson == null) throw new NullPointerException("gson == null");
        this.gson = gson;
    }
 
    @Override
    public Converter<ResponseBody, ?> responseBodyConverter(Type type, Annotation[] annotations,
                                                            Retrofit retrofit) {
        TypeAdapter<?> adapter = gson.getAdapter(TypeToken.get(type));
        return new LenientGsonResponseBodyConverter<>(gson, adapter);
    }
 
    @Override
    public Converter<?, RequestBody> requestBodyConverter(Type type,
                                                          Annotation[] parameterAnnotations, Annotation[] methodAnnotations, Retrofit retrofit) {
        TypeAdapter<?> adapter = gson.getAdapter(TypeToken.get(type));
        return new LenientGsonRequestBodyConverter<>(gson, adapter);
    }
    public class LenientGsonResponseBodyConverter<T> implements Converter<ResponseBody, T> {
        private final Gson gson;
        private final TypeAdapter<T> adapter;
 
        LenientGsonResponseBodyConverter(Gson gson, TypeAdapter<T> adapter) {
            this.gson = gson;
            this.adapter = adapter;
        }
 
        @Override
        public T convert(ResponseBody value) throws IOException {
            JsonReader jsonReader = gson.newJsonReader(value.charStream());
            jsonReader.setLenient(true);
            try {
                return adapter.read(jsonReader);
            } finally {
                value.close();
            }
        }
    }
    public class LenientGsonRequestBodyConverter<T> implements Converter<T, RequestBody> {
        private  final MediaType MEDIA_TYPE = MediaType.parse("application/json; charset=UTF-8");
        private  final Charset UTF_8 = Charset.forName("UTF-8");
 
        private final Gson gson;
        private final TypeAdapter<T> adapter;
 
        LenientGsonRequestBodyConverter(Gson gson, TypeAdapter<T> adapter) {
            this.gson = gson;
            this.adapter = adapter;
        }
 
        @Override
        public RequestBody convert(T value) throws IOException {
            Buffer buffer = new Buffer();
            Writer writer = new OutputStreamWriter(buffer.outputStream(), UTF_8);
            JsonWriter jsonWriter = gson.newJsonWriter(writer);
            jsonWriter.setLenient(true);
            adapter.write(jsonWriter, value);
            jsonWriter.close();
            return RequestBody.create(MEDIA_TYPE, buffer.readByteString());
        }
    }
}
```

然后在创建Retrofit

```java
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl(UrlContainer.baseUrl)
    .client(client.build())
    .addConverterFactory(LenientGsonConverterFactory.create(gson))
    .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
    .build();
```

### 2. 在创建Gson实例时，设置setLenient()

```java
Gson gson = new GsonBuilder()
    .setLenient()
    .create();
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl(UrlContainer.baseUrl)
    .client(client.build())
    .addConverterFactory(GsonConverterFactory.create(gson))
    .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
    .build();
```

这时只需正常地添加`addConverterFactory(GsonConverterFactory.create())`即可