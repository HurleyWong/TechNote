## Android中OOM异常的解决方法之一

### OOM

OOM:Out of Memory，内存溢出，即不良代码创建了太多的对象实例，且使用完之后没有及时释放，导致运行内存超过了系统分配的上限，从而使应用异常退出的现象。

### 解决方法

及时释放Bitmap资源

```java
public void recycleBitmap() {
  Bitmap bitmap = BitmapFactory.decodeFile(PATH_NAME)；
  if (bitmap != null && !bitmap.isRecycled)) {
    bitmap.recycle();
    bitmap = null;
  }
  System.gc();
}
```

bitmap本身调用recycle()方法也是相当于通过呼叫垃圾回收器来回收资源，并不是立刻释放资源。

### 使用BitmapFactory.decodeStream

通常在加载本地图片资源时，会使用decodeResource()方法。通过查看源码，发现decodeResource在解析时会对Bitmap根据当前设备屏幕像素密度densityDpi的值进行缩放适配操作，使得解析出来的Bitmap与当前设备的分辨率匹配，达到一个最佳的显示效果，并且Bitmap的大小将比原始的大。所以，尽量多地使用decodeStream来加载图片资源。

### 使用软引用持有资源

普通的Bitmap对象都是强引用对象，正在使用时难以释放资源造成OOM。所以使用软引用来代替强引用，以达到内存不足的情况下会强制释放部分资源，以保持程序的正常运行

### 三级缓存策略

很多时候从网上加载图片资源，为了防止过多的访问网络资源，而导致流量使用过大，而采取的一种图片资源加载策略。

![https://upload-images.jianshu.io/upload_images/2590942-7c400728509a0307.png?imageMogr2/auto-orient/strip|imageView2/2/w/553](https://upload-images.jianshu.io/upload_images/2590942-7c400728509a0307.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/553)

![https://upload-images.jianshu.io/upload_images/2590942-7c400728509a0307.png?imageMogr2/auto-orient/strip|imageView2/2/w/553](https://upload-images.jianshu.io/upload_images/2590942-7c400728509a0307.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/553)