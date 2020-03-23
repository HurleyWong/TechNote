## Android自定义TextView，文字大小自动调整仅显示一行

目前在做一个高级计算器的应用，因为当数字输入过多时，如果换了很多行会显得不美观，所以需要缩小字体，让其自动调整大小，仅显示在一行中。

这里需要自定义TextView

```java
@SuppressLint("AppCompatCustomView")
public class SingleLineZoomTextView extends TextView {
    private static final String TAG = "SingleLineZoomTextView";

    private Paint mPaint;
    private float mTextSize;

    public SingleLineZoomTextView(Context context) {
        super(context);
    }

    public SingleLineZoomTextView(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public SingleLineZoomTextView(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
    }


    // getTextSize返回值是以像素（px）为单位，而setTextSize默认是以sp为单位
    // 所以需要传入像素单位setTextSize(TypedValue.COMPLEX_UNIT_PX, size);
    private void refitText(String text, int textWidth) {
        if (textWidth > 0) {
            mTextSize = this.getTextSize();
            mPaint = new Paint();
            mPaint.set(this.getPaint());
            int drawWid = 0;
            Drawable[] draws = getCompoundDrawables();
            for (int i = 0; i < draws.length; i++) {
                if (draws[i] != null) {
                    drawWid += draws[i].getBounds().width();
                }
            }

            // 获得当前TextView的有效宽度
            int availableWidth = textWidth - this.getPaddingLeft()
                - this.getPaddingRight() - getCompoundDrawablePadding() - drawWid;
            // 所有字符所占像素宽度
            float textWidths = getTextLength(mTextSize, text);
            while (textWidths > availableWidth) {
                // 这里传入单位为px
                mPaint.setTextSize(--mTextSize);
                textWidths = getTextLength(mTextSize, text);
            }
            // 这里设置单位为px
            this.setTextSize(TypedValue.COMPLEX_UNIT_PX, mTextSize);
        }
    }

    // 字符串所占像素宽度
    private float getTextLength(float textSize, String text) {
        mPaint.setTextSize(textSize);
        return mPaint.measureText(text);
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        refitText(getText().toString(), this.getWidth());
    }

}
```