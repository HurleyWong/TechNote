## 自定义Dialog——宽度充满屏幕并位于屏幕底部

在Android5.0之后的版本，如果使用普通的Dialog，就会发现Dialog一直位于屏幕的中央，并且尽管设置宽度为match_parent，但是宽度仍然无法充满屏幕，两边都会有去不掉的边距。

所以需要使用一些方法自定义Dialog去解决该问题。

### 1. 定义style

定义自定义Dialog通用的style

```xml
<!-- Dialog style -->
<style name="Theme.Light.NoTitle.Dialog" parent="@android:style/Theme.Dialog">
  <item name="android:windowBackground">@android:color/transparent</item>
  <item name="android:windowNoTitle">true</item>
  <item name="android:windowIsFloating">true</item>
  <item name="android:windowFrame">@null</item>
</style>
```

### 2. Dialog进入离开动画（可选）

### 3. Dialog构造器

```java
public static void showDialog(Context context) {
  int dialogTheme = R.style.defaultDialogTheme;
  final Dialog dialog = new Dialog(context, dialogTheme);
  View contentView = LayoutInflater.from(context).inflate(R.layout.dialog, null);
  dialog.setContentView(contentView);
  // 设置dialog宽度充满屏幕且位于屏幕底部
  setBottomLayout(editDialog);
}
```

### 4. 通过WindowManager设置布局

```java
public static void setBottomLayout(Dialog dialog) {
  Window window = dialog.getWindow();
  if (window != null) {
    window.getDecorView().setPadding(0, 0, 0, 0);
    WindowManager.LayoutParams layoutParams = window.getAttributes();
    layoutParams.width = WindowManager.LayoutParams.MATCH_PARENT;
    layoutParams.height = WindowManager.LayoutParams.WRAP_CONTENT;
    window.setAttribute(layoutParams);
    // 设置Dialog布局位于屏幕底部
    window.setGravity(Gravity.BOTTOM);
  }
}
```

有时候会有需求要求，Dialog位于底部但是距离底部屏幕仍然有一定的间距。这时候就需要设置layoutParams.y这个属性。

```java
layoutParams.y = 16;
dialog.getWindow().setAttributes(params);
dialog.show();
```