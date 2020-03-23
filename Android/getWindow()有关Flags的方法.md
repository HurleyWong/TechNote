## getWindow()有关Flags的方法

```java
// 设置窗体全屏
getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,                      WindowManager.LayoutParams.FLAG_FULLSCREEN);
// 设置窗体始终点亮 
getWindow().setFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON,                      WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
// 设置窗体背景模糊  
getWindow().setFlags(WindowManager.LayoutParams.FLAG_BLUR_BEHIND,                      WindowManager.LayoutParams.FLAG_BLUR_BEHIND);
```

使用FLAG_KEEP_SCREEN_ON的方式来标记屏幕常亮

```java
// 添加
getWindow().addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
// 取消
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_KEEP_SCRREN_ON);
```