## ViewPager的smoothScroll控制速度

### 问题

ViewPager可以通过`mViewPager.setCurrentItem(index, true)`来切换动画时进行平滑的滑动，但是如果需要控制滑动时间，则发现ViewPager没有提供这个方法。

查看ViewPager的源码：

```Java
public void setCurrentItem(int item, boolean smoothScroll) {
  mPopulatePending = false;
  setCurrentItemInternal(item, smoothScroll, false);
}
```

即发现setCurrentItem里调用的是setCurrentItemInternal方法，继续查看

```Java
void setCurrentItemInternal(int item, boolean smoothScroll, boolean always) {
  setCurrentItemInternal(item, smoothScroll, always, 0);
}
```

这个方法调用的`void setCurrentItemInternal(int item, boolean smoothScroll, boolean always, int velocity)`貌似是可以指定速度的，但是这个方法不是public的。不过可以用反射来解决。继续查看源码，发现smoothScrollTo方法中有一句

```Java
duration = Math.min(duration, MAX_SETTLE_DURATION);
```

发现在ViewPager中有一个定义常量

```Java
private static final int MAX_SETTLE_DURATION = 600;   //ms
```

即设置的duration最大速度不会超过600ms。但是我们发现在duration后，还需要调用mScroller.startScroll(sx, sy, dx, dy, duration)方法，所以只需要反射修改mScroller

### 解决方法

#### 重写Scroller类

```Java
/**
 *利用这个类来修正ViewPager的滑动速度
 *重写startScroll方法，忽略传过来的duration属性
 *而是采用自己设置的时间
 */
public class FixedSpeedScroller extends Scroller {
  public int mDuration = 1200;    //ms

  public FixedSpeedScroller(Context context) {
    super(context);
  }

  public FixedSpeedScroller(Context context, interpolator interpolator) {
    super(context, interpolator);
  }

  public FixedSpeedScroller(Context context, Interpolator interpolator, boolean flywheel) {
    super(context, interpolator, flywheel);
  }

  @Override
  public void startScroll(int startX, int startY, int dx, int dy) {
    startScroll(startX, startY, dx, dy, mDuration);
  }

  @Override
  public void startScroll(int startX, int startY, int dx, int dy, int duration) {
    super.startScroll(startX, startY, dx, dy, mDuration);
  }

  public int getmDuration() {
    return mDuration;
  }

  public void setmDuration(int duration) {
    mDuration = duration;
  }
}
```

#### 反射

利用反射把FixedSpeedScroller类设置给ViewPager

```Java
/**
 *通过反射来修改 ViewPager的mScroller属性
 */
try {
  Class clazz=Class.forName("android.support.v4.view.ViewPager");
  Field field=clazz.getDeclaredField("mScroller");
  FixedSpeedScroller fixedSpeedScroller=new FixedSpeedScroller(this,new LinearOutSlowInInterpolator());
  fixedSpeedScroller.setmDuration(2000);
  field.setAccessible(true);
  field.set(mViewPager,fixedSpeedScroller);
} catch (Exception e) {
  e.printStackTrace();
}
```

这时再设置`mViewPager.setCurrentItem(index, true)`就可以看到滑动速度的效果了。