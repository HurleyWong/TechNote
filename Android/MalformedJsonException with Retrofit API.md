## MalformedJsonException with Retrofit API

有时候返回的JSON数据的格式可能会不是完全符合规范，从而导致报以下错误

```json
MalformedJsonException with Retrofit API
```

这里主要有两种解决办法

### 创建一个自己的GsonConverter继承至GsonConverter

```java
public class LenientGsonConverter extends GsonConverter {
private Gson mGson;

public LenientGsonConverter(Gson gson) {
    super(gson);
    mGson = gson;
}

public LenientGsonConverter(Gson gson, String charset) {
    super(gson, charset);
    mGson = gson;
}

@Override
public Object fromBody(TypedInput body, Type type) throws ConversionException {
    boolean willCloseStream = false; // try to close the stream, if there is no exception thrown using tolerant  JsonReader
    try {
        JsonReader jsonReader = new JsonReader(new InputStreamReader(body.in()));
        jsonReader.setLenient(true);
        Object o = mGson.fromJson(jsonReader,type);
        willCloseStream = true;
        return o;
    } catch (IOException e) {
        e.printStackTrace();
    }finally {
        if(willCloseStream) {
            closeStream(body);
        }
    }

    return super.fromBody(body, type);
}

private void closeStream(TypedInput body){
        try {
            InputStream in = body.in();
            in.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

然后在创建Retrofit时，就可以通过以下方式创建，而不是原先的GsonConverterFactory

```java
 Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("http://whatever.com")
        .addConverterFactory(LenientGsonConverterFactory.create(gson))
        .build();
```

