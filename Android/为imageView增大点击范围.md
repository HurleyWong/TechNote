## 为imageView增大点击范围

1. 在Java代码中设置
2. 在imageView的外部再嵌套一层范围更大的layout布局，然后为layout布局设置点击事件，实际上点击imageView就是点击外面嵌套的布局（坏处：要尽可能的少嵌套布局）
3. 设置padding的方式为imageView增大范围