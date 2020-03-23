## 获取RadioButton选中值

### 第一种方式

通过RadioGroup的setOnCheckedChangeListener()来监听选中哪一个单选按钮

```java
radioGroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
    @Override
    public void onCheckedChanged(RadioGroup group, int checkedId) {
        // 通过RadioGroup.getCheckedRadioButtonId()来得到选中的RadioButton的Id，从而得到RadioButton进而获取选中值
        RadioButton rb = MainActivity.this.findViewById(radioGroup.getCheckedRadioButtonId());
        String text = rb.getText().toString();
    }
}
```

### 第二种方式

利用以下三个方法，对RadioGroup中组件进行循环，依次判断isChecked()，从而找\到选中的组件

- getChildCount()：获取RadioGroup中子组件RadioButton的数目

- getChildAt()：根据索引获取当前索引对应的RadioButton

- isChecked()：判断当前组件是否被选中

    ```java
    for (int i = 0; i < radioGroup.getChildCount(); i++) {
        RadioButton rb = (RadioButton) radioGroup.getChildAt(i);
        if (rb.isChecked()) {
            String text = rb.getText().toString();
            break;
        }
    }
    ```

    

    