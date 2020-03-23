## Android中的scaleType属性

`android:scaleType`是控制图片如何resized/moved来匹配ImageView的size。

### CENTER / center

按图片原来的size居中显示，当图片长/宽超过View的长/宽，则截取图片的居中部分显示

### CENTER_CROP / center

按比例扩大图片的size居中显示，使得图片长（宽）大于或等于View的长（宽）

### CENTER_INSIDE / centerInside

将图片的内容完整居中显示，通过按比例缩小或保持原来的size使得图片长（宽）小于或等于View的长（宽）

### FIT_CENTER / fitCenter

把图片按比例扩大/缩小到View的宽度，居中显示

### FIT_END / fitEnd

把图片按比例扩大/缩小到View的宽度，显示在View的下部分位置

### FIT_START / fitStart

把图片按比例扩大/缩小到View的宽度，显示在View的上部分位置

### FIT_XY / fitXY

把图片不按比例扩大/缩小到View的大小显示

### MATRIX / matrix

用矩阵来绘制