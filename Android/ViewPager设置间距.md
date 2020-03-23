## ViewPager设置间距

有时候需求会让ViewPager切换的两张图片并不是紧挨在一起，而是必须有一定间距。

1. 先在资源文件中给ViewPager添加属性`android:clipChildren="false"`，表示是否限制子View在其范围内，默认为true
2. 在调用setAdapter方法的方法里面设置ViewPager.setPageMargin()方法（括号里放具体的数值，即表示间距），例如mPager.setPageMargin(12)，即表示间距12dp