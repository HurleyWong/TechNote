## Thymeleaf基础知识点

Thymeleaf是搭配Springboot使用的模板引擎。

### **导入依赖**

```xml
<dependency>     
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId> 
</dependency>
```

### 配置文件设置

可以在application.yaml或者application.properties中配置

```xml
# 模板的模式，支持如：HTML、XML、TEXT、JAVASCRIPT等 
spring.thymeleaf.mode=HTML5 
# 编码，可不用配置 
spring.thymeleaf.encoding=UTF-8 
# 内容类别，可不用配置 
spring.thymeleaf.servlet.content-type=text/html 
# 开发配置为false，避免修改模板还要重启服务器 
spring.thymeleaf.cache=false 
# 配置模板路径，默认就是templates，可不用配置 
spring.thymeleaf.prefix=classpath:/templates/
```

### 常用标签

```
th:action   定义后台控制器路径 
th:each     循环语句 
th:field    表单字段绑定 
th:href     定义超链接 
th:id       div标签中的id声明 
th:if       条件判断语句 
th:include  布局标签，替换内容到引入文件 
th:fragment 布局标签，定义一个代码片段，方便其它地方引用 
th:object   替换对象 
th:src      图片类地址引入 
th:text     显示文本 
th:value    属性赋值
```

### **配置文件配置**

1. Themeleaf解决字符串过长显示的问题（截取显示部分字符串）

    ```
    th:text="${#string.abbreviate(twitter.text, 150)}"
    ```

