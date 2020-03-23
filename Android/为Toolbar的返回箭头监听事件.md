## 为Toolbar的返回箭头监听事件

需要重写`onOptionsItemSelected(MenuItem item)`方法，然后判断点击的id是否为`android.R.id.home`，这个id就是返回箭头对应的id

代码如下

```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    switch(item.getItemId()) {
        case android.R.id.home:
            // 点击返回箭头
            break;
        default:
            break;
    }
    return super.onOptionsItemSelected(item);
}
```

