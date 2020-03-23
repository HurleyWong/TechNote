## Fresco代码实现图片圆形效果

### 布局文件

```
<com.facebook.drawee.view.SimpleDrawee
  android:layout_width="100dp"
  android:layout_height="100dp"/>
```

必须设置layout_width和layout_height属性，如果没有在xml中声明这两个属性，就无法正确加载图像

### 设置圆形图片的两种方法

1. `asCircle()`

    ```
    simpleDrawee = (SimpleDraweeView) findViewById(R.id.view);
    GenericDraweeHierarchy hierarchy = GenericDraweeHierarchyBuilder.newInstance(getResource())
             .setRoundingParams(RoundingParams.asCircle())
             .build();
    simpleDrawee.setHierarchy(hierarchy);
    ```

2. `setRoundaAsCircle(boolean roundAscircle)`

    ```java
    simpleDrawee = (SimpleDraweeView) findViewById(R.id.view);
    
    // 初始化圆角圆形参数对象
    RoundingParams params = new RoundingParams();
    // 设置图像是否为圆形
    params.setRoundaAsCircle(true);
    
    // 获取GenericDraweeHierarchy对象
    GenericDraweeHierarchy hierarchy = GenericDraweeHierarchyBuilder.newInstance(getResource())
        // 设置圆形圆角参数
        .setRoundingParams(params)
        .build();
    simpleDrawee.setHierarchy(hierarchy);
    ```

