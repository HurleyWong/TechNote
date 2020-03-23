## Android启动页黑/白闪屏的原因及解决方法

### 原因

在启动Activity的`onCreate()`方法里面，执行`setContentView(R.layout.activity_splash);`

出现白屏。 设想，`onCreate---setContentView`这个并不是发生在，窗体绘制的第一步，系统会在执行这个步骤之前，先绘制窗体，这时候布局资源还没加载，于是就使用默认背景色。

这种亮色系，造成白色闪屏

```xml
<style name="ThemeSplash" parent="Theme.AppCompat.Light">
```

这种暗色系，造成黑色闪屏

```xml
<style name="ThemeSplash" parent="ThemeOverlay.AppCompat.Dark">
```

### 解决方法

将下面的代码放入到工程下的style.xml ，将下面的@mipmap/bg_splash 图片改成自己app的启动页图片

```xml
<style name="ThemeSplash" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="android:background">@mipmap/bg_splash</item>
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowFullscreen">true</item>
        <item name="windowActionBar">false</item>
        <item name="windowNoTitle">true</item>
</style>
```

然后将启动页面的theme改成上面的style

```xml
<activity
      android:name=".activity.WelcomeActivity"
      android:configChanges="screenSize|keyboardHidden|orientation"
      android:theme="@style/ThemeSplash">
       <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
       </intent-filter>
</activity>
```