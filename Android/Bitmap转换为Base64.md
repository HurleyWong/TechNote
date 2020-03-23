## Bitmap转换为Base64

1. 由本地路径获取图片
2. 将Bitmap转换成Base64字符串

```java
public static String bitmap2Base64(String pathString){
    Bitmap bitmap = null;
    try {
        File file = new File(pathString);
        if (file.exists()) {
            bitmap = BitmapFactory.decodeFile(pathString);
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
    ByteArrayOutputStream bos = new ByteArrayOutputStream();
    // 参数2：压缩率，40表示压缩掉60%; 如果不压缩是100，表示压缩率为0
    bitmap.compress(Bitmap.CompressFormat.JPEG, 100, bos);
    byte[] bytes = bos.toByteArray();
    return Base64.encodeToString(bytes, Base64.DEFAULT);
}
```