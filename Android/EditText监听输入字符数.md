## EditText监听输入字符数

根据用户输入的字符数，实时显示用户已输入多少字和还能输入多少个字符（有输入字数限制）

```java
final TextView textView = contentView.findViewById(R.id.dialog_mysay_num);
textView.setText(editText.getText().length() + "/" + num);
// 设置光标在最后
editText.setSelection(editText.getText().length());
editText.addTextChangedListener(new TextWatcher() {
	private CharSequence temp;
	private String temps;
	private int selectionStart;
	private int selectionEnd;

	@Override
	public void beforeTextChanged(CharSequence s, int start, int count, int after) {

	}

	@Override
	public void onTextChanged(CharSequence s, int start, int before, int count) {
		temp = s;
		temps = temp.length() + "/" + num;
		textView.setText(temps);
	}

	@Override
	public void afterTextChanged(Editable s) {
		selectionStart = editText.getSelectionStart();
		selectionEnd = editText.getSelectionEnd();
		// 如果输入字数超出限制
		if (temp.length() > num) {
			s.delete(selectionStart - 1, selectionEnd);
			editText.setText(s);
			// 设置光标在最后 
            editText.setSelection(editText.getText().length());
		}

		// 禁止回车
		for (int i = s.length(); i > 0; i--) {
			if (s.subSequence(i - 1, i).toString().equals("\\n"))
				s.replace(i - 1, i, "");
		}
	}
})
```