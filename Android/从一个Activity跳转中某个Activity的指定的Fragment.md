## 从一个Activity跳转中某个Activity的指定的Fragment

首先在该Activity通过Intent跳转时传递一个名为result的参数，然后在跳转到的Activity中的onResume()方法中接受到该参数，如果正确就进行操作，跳转到指定的Fragment

当前Activity的代码

```java
Intent intent = new Intent(this, MainActivity.class);
intent.putExtra("result", 1);            
startActivity(intent);                
```

跳转到的Activity的代码

```java
@Override
protected void onResume() {
    // 0是默认值
    int result = getIntent().getIntExtra("result", 0);
    if (result == 1) {
        mVpMain.setCurrentItem(2);
    }    
    super.onResume();    
}    
```

因为我是使用Fragment绑定ViewPager的方式，所以切换到指定的Fragment只需要让ViewPager显示对应的Item即可。

如果没有使用ViewPager，则需要使用FragmentManger去切换Fragment

```java
@Override
protected void onResume() {
    // 0是默认值
    int result = getIntent().getIntExtra("result", 0);
    if (result == 1) {
        getSupportFragmentManager()
            .beginTransaction()
            .replace(R.id.fragmennt_container, new UserFragment())
            .addToBackStack(null)
            .commit();
    }
}   
```

`R.id.fragment_container`是对应的FrameLayout的id