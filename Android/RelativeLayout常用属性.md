## RelativeLayout常用属性

RelativeLayout常用属性：居中、边缘距离、相对距离

### 一、居中

```xml
//垂直居中
android:layout_centerVertical="true"
//水平居中
android:layout_centerHorizontal="true"
//相对于父元素完全居中
android:layout_centerInParent="true"
```

### 二、边缘

```xml
//一、属性值为true或false
//贴紧父元素的下边缘
android:layout_alignParentBottom
//贴紧父元素的左边缘
android:layout_alignParentLeft
//贴紧父元素的右边缘
android:layout_alignParentRight
//贴紧父元素的上边缘
android:layout_alignParentTop
//如果无法找到对应的兄弟元素就以父元素作为参照物
android:layout_alignWithParentIfMissing

//二、属性值必须为id的引用名"@id/id-name"
//在某元素的下方
android:layout_below
//在某元素的上方
android:layout_above
//在某元素的左边
android:layout_toLeftOf
//在某元素的右边
android:layout_toRightOf

//该元素的上边缘和某元素的上边缘对齐
android:layout_alignTop
//该元素的左边缘和某元素的左边缘对齐
android:layout_alignLeft
//该元素的下边缘和某元素的下边缘的对齐
android:layout_alignBottom
//该元素的右边缘和某元素的右边缘对齐
android:layout_alignRight
```

### 三、距离

```xml
//属性值为具体的像素值，如30dip，40px
//离某元素底边缘的距离
android:layout_marginBottom
//离某元素左边缘的距离
android:layout_marginLeft
//离某元素右边缘的距离
android:layout_marginRight
//离某元素上边缘的距离
android:layout_marginTop
```



