## Java中instanceof的用法

Java中的instanceof 是一个二元操作符（运算符）运算符，由于是字母组成，所以是Java的保留关键字，但是和>=，<=，==属同一类，它的作用是用来判断，instanceof 左边对象是否为instanceof 右边类的实例，返回一个boolean类型值。还可以用来判断子父类的所属关系。

### 用法

```java
boolean result = object instanceof class
```

### 参数

- result：布尔类型
- Object：必选项。任意对象表达式
- Class：必选项。任意已定义的对象类

### 说明

如果object是class的一个实例，则instanceof运算符返回true。如果object不是指定类的一个实例，或者object是null，则返回true。