## SearchView的使用方法

### 创建菜单文件

在res文件夹下的menu文件夹中创建menu_search.xml文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
          android:id="@+id/home_search"
        	android:title="@string/home_search"
        	app:actionViewClass="android.support.v7.widget.SearchView"
        	app:showAsAction="ifRoom" />
</menu>
```

`app:actionViewClass="android.support.v7.widget.SearchView"`这是在告知toolbar这里是SearchView

### 配置SearchView

* 输入类型`android:inputType`
* 最大宽度`mSearchView.setMaxWidth()`
* 搜索图标是否显示在搜索框内`mSearchView.setIconifiedByDefault(true)`
* 设置搜索框展开时是否显示提交按钮`mSearchView.setSubmitButtonEnabled(true)`
* 将软键盘的回车键设置为搜索`mSearchView.setImeOptions(EditorInfo.IME_ACTION_SEARCH)`
* 搜索框是否展开，false表示展开`mSearchView.setIconified(false)`
* 获取焦点`mSearchView.setFocusable(true);mSearchView.requestFocusFromTouch();`
* 设置提示词`mSearchView.setQueryHint("请输入关键字")`

### 设置监听

`setOnQueryTextListener`包括搜索和内容发生改变的两个事件

`setOnCloseListener`是关闭按钮的监听

`setOnSearchClickListener`是点击搜索按钮的监听

`setOnSuggestionListener`是提示内容被选中时的监听

```java
mSearchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
    @Override
    public boolean onQueryTextSubmit(String s) {          
        // 搜索后，收起软键盘
        mSearchView.clearFocus();
        return true;
    }

    @Override
    public boolean onQueryTextChange(String s) {
        return false;
    }
});
```

