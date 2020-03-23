## 改变ViewPager的切换速度

通过观察ViewPager的源码，可以发现最终控制速度的都是mScroller，所以我们需要自定义Scroller

### 自定义Scroller

```java
public class MyScroller extends Scroller {
  private long mDuration;

  public MyScroller(Context context) {
    super(context);
  }

  public MyScroller(Context context, Interpolator interpolator) {
    super(context, interpolator);
  }

  public MyScroller(Context context, Interpolator interpolator, boolean flywheel) {
    super(context, interpolator, flywheel);
  }

  public long getmDuration() {
    return mDuration;
  }

  public void setmDuration(long mDuration) {
    this.mDuration = mDuration;
  }

  @Override
  public void startScroll(int startX, int startY, int dx, int dy) {
    super.startScroll(startX, startY, dx, dy, this.getDuration());
  }

  @Override
  public void startScroll(int startX, int startY, int dx, int dy, int duration) {
    super.startScroll(startX, startY, dx, dy, this.getDuration());
  }
}
```

### 反射

由于ViewPager中的mScroll是private的，所以需要考虑反射

```java
public class ScrollUtils {
  public static void setViewPagerScrollerSpeed(ViewPager viewPager, int speed) {
    try {
      Field field = ViewPager.class.getDeclaredField("mScroller");
      field.setAccessible(true);
      // AccelerateInterpolator是匀加速插值器
      MyScroller scroller = new MyScroller(viewPager.getContext(), new AccelerateInterpolator());
      field.set(viewPager, viewPagerScroller);
      scroller.setmDuration(speed);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

### 调用

```java
// 速度为1000ms=1s
ScrollUtils.setViewPagerScrollerSpeed(pager, 1000);
```

注意，经测试，这种方法在自定义的数值滑动的ViewPager中设置速度似乎不起作用。 