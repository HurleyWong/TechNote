## Volley原理

### 代码

```
// 创建一个RequestQueue
RequestQueue queue=Volley.newRequestQueue(this);
String url=" ";

// StringRequest是Volley提供的一个专门用于请求字符串类型数据的Request
// 第一个参数url是请求访问的地址
// 第二个参数是一个回调接口，在onResponse()方法里进行操作，因为Volley将已经加工好的数据直接返回给主线程
// 第三个参数是在出现错误后的一个回调接口，在onErrorResponse()中可以得到错误细信息，在主线程中工作
StringRequest request=new StringRequest(url,new Response.Listener(){
  @Override
  public void onResponse(String response){
    // 请求成功的操作
  }
},new Response.ErrorListener(){
  @Override
  public void onErrorResponse(VollerError error){
    // 请求失败的操作
  }
});
// 将request添加到RequestQueue中，Volley就开始工作
queue.add(request);
```

### 工作流程

![https://upload-images.jianshu.io/upload_images/2590942-a17c7d270fca06fb.png?imageMogr2/auto-orient/strip|imageView2/2/w/526](https://upload-images.jianshu.io/upload_images/2590942-a17c7d270fca06fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/526)

其中蓝色的是主线程，绿色的是缓存线程，黄色的是网络线程。

1. 当一个Request请求添加到RequestQueue中，Volley就开始工作。RequestQueue请求队列中持有一个CacheDispatcher缓存管家和一组NetworkDispatcher网络管家。
2. RequestQueue会先让CacheDispatcher缓存管家去检查当前请求的数据是否在cache中。如果在缓存中，就把数据从cache中取出来，经过一番加工，将加工好的数据交付给主线程；如果不在cache中，执行第3步。
3. RequestQueue让NetworkDispatcher(其实是一个线程池)，默认情况下会启动4个线程去网络下载数据。RequestQueue给空闲的NetworkDispatcher分配任务。
4. RequestQueue让NetworkDispatcher(其实是一个线程池)，默认情况下会启动4个线程去网络下载数据。RequestQueue给空闲的NetworkDispatcher分配任务。