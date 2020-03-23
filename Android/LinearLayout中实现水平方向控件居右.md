## LinearLayout中实现水平方向控件居右

在LinearLayout中直接设置子控件

```xml
android:layout_gravity="left"
android:layout_gravity="right"
```

是无效的。

可以改用比重的方法来达到控件一左一右，代码如下

```xml
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal" >
		
    <Button
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="按钮1" />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="按钮2" />
</LinearLayout>
```

主要代码就是设置左边的width为0dp，然后权重为1，就可以让该控件充满屏幕，将下一个控件挤到最右端，就可以解决LinearLayout中实现水平方向控件居右