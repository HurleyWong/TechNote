## Android中ImageView实现平铺多张图片

Android中实现平铺图片有两种方式：

### 在drawable中定义平铺的Bitmap

```xml
<?xml version="1.0" encoding="utf-8"?>
<bitmap xmlns:android="<http://schemas.android.com/apk/res/android>"
    android:src="@drawable/splash_top_bg_shadow"
    android:tileMode="repeat" />
```

然后在ImageView中引用该文件

```xml
<ImageView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@drawable/a_repeat_curtains_shadow"/>
```

这里主要使用到了bitmap的一个属性`android:tileMode="repeat"`

tileMode(平铺)，效果类似于让背景小图不是拉伸而是多个重复。

### 在Java代码中设置

```java
private void initViewBg(ViewHolder holder) {
    //设置内容区域平铺的小圆角背景
    Bitmap topBitmap = BitmapFactory.decodeResource(mContext.getResources(), R.mipmap.ic_left);
    BitmapDrawable leftDrawable = new BitmapDrawable(mContext.getResources(), topBitmap);
    leftDrawable.setTileModeY(Shader.TileMode.REPEAT);
    
    Bitmap bottomBitmap = BitmapFactory.decodeResource(mContext.getResources(), R.mipmap.ic);
    BitmapDrawable rightDrawable = new BitmapDrawable(mContext.getResources(), bottomBitmap);
    rightDrawable.setTileModeY(Shader.TileMode.REPEAT);

    if (Build.VERSION_SDK_INT >= Build.VERSION_CODES.JELIY_BEAN) {
    	holder.favourItemBgLeft.setBackground(leftDrawable);
    	holder.favourItemBgRight.setBackground(rightDrawable);
    } else {
    	holder.favourItemBgLeft.setBackgroundDrawable(leftDrawable);
    	holder.favourItemBgRight.setBackgroundDrawable(rightDrawable);
    }
}
```

其中第一种在xml文件中通过设置android:tileMode=”repeat”的方式可能会在不同的机型中出现适配问题，所以更推荐使用代码的方式实现对图片的平铺效果