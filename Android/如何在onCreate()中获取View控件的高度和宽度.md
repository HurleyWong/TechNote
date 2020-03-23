## 如何在onCreate()中获取View控件的高度和宽度

因为在xml布局文件中，在写控件的高度和宽度时不是固定的，而是需要根据用户手机屏幕的宽高来展示控件的宽高，即需要在Java代码中动态地改变控件的宽高。

我们知道，获取控件的宽度或高度可以使用View.getWidth()和View.getHeight()的方法得到宽高。但是经过测试发现，在onCreate()方法中使用上述两个方法得到的宽度和高度都是0

### 原因

这跟View的绘制机制有关。因为View绘制是通过两个遍历来完成的，一个是measure过程，一个是layout过程。只有经过了“测量”和“布局”过程之后，View才会正确地完成绘制。这一切是发生在onCreate()方法之后的。所以在onCreate()方法中直接使用View.getWidth()和View.getHeight()方法是无法得到正确的值的，因为View还没有绘制完成。

### 解决方法

1. 通过线程的方式解决

    通过View.post()方法获取到View的宽高，该方法传递一个Runnable参数，然后将其添加到消息队列中，最后在UI线程中执行。

    ```java
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    
        view.post(new Runnable() {
            public void run() {
                // 在这里使用View.getWidth()和View.getHeight()方法可以得到正确的宽高值
                view.getWidth();
                view.getHeight();
            }
        })
    }
    ```