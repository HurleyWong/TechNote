## 垂直滑动的ViewPager与禁止滑动切换效果

ViewPager默认是只支持左右滑动的，因此如果因为需求问题必须实现上下滑动，就得去看ViewPager的源码是如何实现的，然后自己写一个ViewPager继承自Android原生自带的ViewPager。

### VerticalViewPager

```java
// 垂直滑动的ViewPager
public class VerticalViewPager extends ViewPager {
  public VerticalViewPager(Context context) {
    this(context, null);
  }

  public VerticalViewPager(Context context, AttributeSet attrs) {
    super(context, attrs);
    // 设置ViewPager的动画，在这里设置才能实现垂直滑动的ViewPager
    setPageTransformer(true, new VerticalTransformer());
  }

  // 拦截touch事件
  @Override
  public boolean onInterceptTouchEvent(MotionEvent event) {
    return false;
  }

  @Override
  public boolean onTouchEvent(MotionEvent event) {
    return false;
  }

  private MotionEvent swapEvent(MotionEvent event) {
    // 获取宽高
    float width = getWidth();
    float height = getHeight();
    // 将Y轴的移动距离转变成X轴的移动距离
    float swappedX = (event.getY() / height) * width;
    // 将X轴的移动距离转变成Y轴的移动距离
    float swappedY = (event.getX() / width) * height;
    // 重设event的位置
    event.setLocation(swappedX, swappedY);
    return event;
  }
}
```

### VerticalTransformer

设置切换动画，如果不设置切换动画，则虽然已经是上下滑动，但是动画效果仍然是水平方向的

```java
public class VerticalTransformer implements ViewPager.PageTransformer {
  @Override
  public void transformPage(View view, float position) {
    float alpha = 0;
    if (0 <= position && position <= 1) {
      alpha = 1 - position;
    } else if (-1 < position && position < 0) {
      alpha = position + 1;
    }
    view.setAlpha(alpha);
    float transX = view.getWidth() * -position;
    view.setTranslationX(transX);
    float transY = position * view.getHeight();
    view.setTranslationY(transY);
  }
}
```

### 禁止滑动切换item

即不拦截也不处理触摸事件，所以把onInterceptTouchEvent和onTouchEvent都返回false即可