## jdbcTemplate中的queryForInt()方法废弃

现在的queryForInt()方法已经废弃，全部改用`queryForObject()`

例如

```java
int count = jdbcTemplate.queryForObject(sql, new Object[] { user_id }, Integer.class);
```

