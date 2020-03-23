## EditText隐藏/自动弹出输入法

有时候需要在弹出输入框的同时，无须点击EditText的内容就自动弹出输入法。

因为弹出的对话框里含有EditText的话，show方法会与输入法的实现冲突，就不会自动弹出。所以需要用handler延时的方式显示输入法。

```java
private static InputMethodManager inputMethodManager;

// 显示输入法键盘
public static void showInputMethod(Context c, View v) {
  if (inputMethodManager == null) {
    inputMethodManager = (InputMethodManager) c.getSystemService(Context.INPUT_METHOD_SERVICE);
    try {
      inputMethodManager.showSoftInput(v, 0);
    } catch (NullPointException e) {

    }
  }
}

// 隐藏虚拟键盘
public static void HideKeyboard(View v) {
  InputMethodManager imm = (InputMethodManager) v.getContext().getSystemService(Context.INPUT_METHOD_SERVICE);
  if (imm.isActive()) {
    imm.hideSoftInputFromWindow(v.getApplicationWindowToken(), 0);
  }
}

// 显示对话框后，用handler延时显示输入法键盘
public static void showInputMethod(final Context c, final View v, int delayMills) {
  new Handler().postDelayed(new Runnable() {
    @Override
    public void run() {
      showInputMethod(c, v);
    }
  }, delayMills);
}
```