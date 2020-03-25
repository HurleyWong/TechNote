## Android中shape属性详解

### 简单使用

#### 新建shape文件

首先在res/drawable文件夹下，新建一个文件，命名为a_shape_match_tip_bg.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <solid android:color="#ffffefe8" />
    <corners android:radius="20dp" />
</shape>
```

#### 添加到控件中

添加到控件中，一般是使用设置background属性，将其设为背景图片

```xml
<TextView
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:layout_marginLeft="30dp"            
  android:layout_gravity="center_vertical"            
  android:text="鱼丸粗面"            
  android:textColor="#ffff9060"            
  android:textSize="12sp"            
  android:background="@drawable/a_shape_match_tip_bg"/>                          
```

### 基本属性

shape的基本属性包括corners、gradient、padding、size、solid、stroke（shape的子标签）

#### corners

```xml
<corners	//定义圆角
  //dimension指具体的尺寸dp
  android:radius="dimension"	//全部的圆角半径
  android:topLeftRadius="dimension"	//左上角的圆角半径
  android:topRightRadius="dimension"	//右上角的圆角半径
  android:bottomLeftRadius="dimension"	//左下角的圆角半径
  android:bottomRightRadius="dimension"/>	//右下角的圆角半径
```

corners标签是用来定义圆角的，其中radius与其它四个并不能共同使用

#### solid

solid用来指定内部填充色，它只有color一个属性

```xml
<solid android:color="#ffff00"/>
```

#### gradient

gradient用以定义渐变色，可以定义两色渐变和三色渐变及渐变样式

```xml
<gradient
  //共有3中渐变类型，线性渐变(默认)、放射渐变、扫描式渐变
  android:type=["linear" | "radial" | "sweep"]
  android:angle="integer"	//渐变角度，必须为45的倍数，0为从左到右，90为从上到下
  android:centerX="float"	//渐变中心X的位置，范围为0~1
  android:centerY="float"	//渐变中心Y的位置，范围为0~1
  android:startColor="color"	//渐变开始点的颜色
  android:centerColor="color" //渐变中间点的颜色，在开始与结束之间
  android:endColor="color"	//渐变结束点的颜色
  android:gradientRadius="float"	//渐变的半径，只有当渐变类型为radial时才能使用
  //使用LevelListDrawable时要设置为true，设置为fasle时才有渐变效果
  android:useLevel=["true" | "false"]
```

* 在构造放射性渐变时，需要加上`android:gradientRadius`属性（渐变半径），即必须指定渐变半径的大小才会起作用
* `android:angle=“integer"`angle属性只对线性渐变有效
* centerX、centerY两个属性用于设置渐变的中心点位置，仅当渐变类型为放射渐变时才有效，类型为分数或小数，不接受dimension，超出该范围后会看不出渐变效果。centerX、centerY的取值其实是宽和高的百分比
* useLevel属性通常不使用。该属性用于指定是否将该shape当成一个LevelListDrawable来使用，默认值为false

#### stroke

描边属性，可以定义描边的宽度、颜色、虚实线等

```xml
<stroke
  android:width="dimension"	//描边的宽度
  android:color="color"	//描边的颜色
  //以下两个属性设置虚线
  android:dashWidth="dimension"	//虚线的宽度，值为0时时实线
  android:dashGap="dimension"/>	//虚线的间隔
```

#### size和padding

这两个属性基本不常使用，因为它们具有的功能，控件本身也可以实现。  

size是用来定义图形的大小

```xml
<size
  android:width="dimension"
  android:height="dimension"/>
```

padding是用来定义内部边距

```xml
<padding
  android:left="dimension"
  android:top="dimension"
  android:right="dimension"
  android:bottom="dimension"/>
```

### shape的属性

shape可以通过shape属性定义当前shape的形状，比如矩形、椭圆形、线形等

```xml
<shape
  xmlns:android="http://schemas.android.com/apk/res/android"
  //shape的形状，默认为矩形，可以设置为矩形、椭圆、线形形状、环形
  android:shape=["rectange" | "oval" | "line" | "ring"]
  //以下属性只有当形状为环形(ring)时可用
  android:innerRadius	//尺寸，内环的半径
  android:innerRadiusRatio	//浮点型，以环的宽度比率来表示内环的半径  
  android:thickness	//尺寸，环的厚度                                                    
  android:thicknessRatio	//浮点型，以环的宽度比率来表示环的厚度                                                    
  android:useLevel	//boolean值，如果是LevelListDrawable使用时值为true，否则为false                                                    
```

无论shape设置为什么形状，它的子标签都是可用的，但是不一定会有效果。比如shape为椭圆时，corners标签就不会有效果