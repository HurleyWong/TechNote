## WordCount

使用Hadoop时，一般都会遇到这个示例程序WordCount.java文件。

但是因为版本迭代问题，又是会已经废弃的代码。

例如以下代码就已经过期了：

```java
Configuration conf = new Configuration();
Job job = new Job(conf);
```

要改成：

```java
Configuration conf = new Configuration();
Job job = Job.getInstance(conf, "WordCount");
```

