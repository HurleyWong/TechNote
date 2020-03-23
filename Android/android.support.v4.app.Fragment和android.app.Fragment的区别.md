## android.support.v4.app.Fragment和android.app.Fragment的区别

### 1. 最低支持版本不同

android.app.Fragment兼容的最低版本是android 3.0版本

android.support.v4.app.Fragment兼容的最低版本是android 1.6版本

### 2. 需要导入不同的jar包

android.app.Fragment需要导入android-app.jar

android.support.v4.app.Fragment需要引入包android-support-v4.jar

### 3. 继承的父类不同，在fragmentManager的取法不同

android.support.v4.app.Fragment使用` fragmentManager = getSupportFragmentManager()`获得，并且当前的类必须继承FragmentActivity

android.app.Fragment使用`fragmentManager = getFragmentManager()`获得，继承Activity即可

### 4. <fragment>标签的使用情况

v4包中的Fragment在Activity的布局中是可以用<fragment>标签的

android.app.Fragment在Activity布局中是不可以用<fragment>标签的，需要在程序中通过add或者replace的方式添加

### 5. 冲突问题

要么使用app.Fragment，要么使用support.v4.app.Fragment，否则会产生冲突从而报错

在使用ViewPager + Fragment时，使用ViewPager提供的FragmentPageAdapter的时候，**FragmentPageAdapter**的**FragmentMananger**参数必须是**v4**包下的，当项目里的FragmentManager是app.Fragment的话，就会产生冲突。

原因：FragmentPagerAdapter是继承了PagerAdapter，该类为v4包独有

解决方法：把FragmentPagerAdapter里的代码复制过来重写该类，将里面的v4下的FragmentManager等全部改为app.Fragment，然后使用时，再继承自己复制过来的比如MyFragmentPagerAdapter即可。