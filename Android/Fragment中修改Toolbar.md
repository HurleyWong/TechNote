## Fragment中修改Toolbar

主界面是一个Activity，里面是ViewPager+Fragment。当滑到不同Fragment时，上面的Toolbar需要跟着改变。

### 让Fragment支持并修改Toolbar

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setHasOptionsMenu(true);
}

@Override
public void onCreateOptionsMenu(Menu menu, MenuInflater inflater) {
    // 清除其它Fragment的Toolbar中的menu
    menu.clear();
    inflater.inflate(R.menu.nav, menu);
    super.onCreateOptionsMenu(menu, inflater);
}
```

### 让Toolbar的menu显示图标

```java
@Override
public void onCreateOptionsMenu(Menu menu, MenuInflater inflater) {
    // 这里设置另外的menu
    menu.clear();
    inflater.inflate(R.menu.notes, menu);

    // 通过反射让menu的图标可见
    if (menu != null) {
        if (menu.getClass() == MenuBuilder.class) {
            try {
                Method m = menu.getClass().getDeclaredMethod("setOptionalIconsVisible", Boolean.TYPE);
                m.setAccessible(true);
                m.invoke(menu, true);
            } catch (Exception e) {

            }
        }
    }

    // 这一行不能忘，否则看不到图标
    // 拿到ActionBar后，可以进行设置
    ((AppCompatActivity) getActivity()).getSupportActionBar();
    super.onCreateOptionsMenu(menu, inflater);
}
```

