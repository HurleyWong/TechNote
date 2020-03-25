## BottomNavigationView的属性

BottomNavigationView是用来实现底部导航栏的View。可以添加1-5个item，但是当item超过3时就会出现偏移动画，并且只有选中当前item时才会出现文字，未选中的item不会出现文字。

可以通过BottomNavigationView的两个属性来解决这个问题。

```xml
app:itemHorizontalTranslationEnabled="false"  
app:labelVisibilityMode="labeled"
```

`app:itemHorizontalTranslationEnabled="false"`禁止item水平平移动画效果，对应的方法为`setItemHorizontalTranslationEnabled(false)`

`app:labelVisibilityMode="labeled"`设置图标下面的文字显示，该属性对应的值有`auto`、`labeled`、`selected`、`unlabeled`

* auto：当item小于等于3时，显示文字；当item大于3个时默认不显示，只有选中才显示文字
* labeled：始终显示文字
* selected：选中时显示文字
* unlabeled：选中时显示文字

该属性对应的方法为`setLabelVisibilityMode(LabelVisibilityMode.LABEL_VISIBILITY_LABELED)`

除此之外，BottomNavigationView还有三个重要的属性

* `app:itemBackground`：设置item的背景，对应`setItemBackgroundResource(int resId)`方法
* `app:itemIconTintUsed`：设置icon的颜色，对应`setItemIconTintList(ColorStateList tint)`方法
* `app:itemTextColor`：设置文字的颜色，对应`setItemTextColor(ColorStateList textColor)`方法