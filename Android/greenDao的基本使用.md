## greenDao的基本使用

### greenDao简介

greenDao是一个将对象映射到SQLite数据库中的轻量且快速的ORM解决方案。

### greenDao特点

* 性能最大化，可能是Android平台上最快的ORM框架
* 易于使用的API
* 最小的内存开销
* 依赖体积小
* 支持数据库加密
* 强大的社区支持

### greenDao配置

#### 在build.gradle(Module:app)中添加如下代码：

```groovy
apply plugin: 'org.greenrobot.greendao'

dependencies {
    // greenDAO包：https://github.com/greenrobot/greenDAO
    implementation 'org.greenrobot:greendao:3.2.2'
}

greendao {
    // 数据库版本号
    schemaVersion 1
    // 设置DaoMaster、DaoSession、Dao目录
    // 这行代码与高版本gradle冲突，会报API 'variant.getJavaCompiler()'的warn，将在2019年末移除
    targetGenDir 'src/main/java'
    // 设置DaoMaster、DaoSession、Dao包名
    daoPackage 'com.example.hurley.wanandroid.dao'
    // 设置生成单元测试目录
    // targetGenDirTest
    // 设置自动生成单元测试用例
    // generateTests
}
```

#### 在build.gradle(Project)中添加如下代码：

```groovy
buildscript {
    repositories {
        mavenCentral()
    }
    
    dependencies {
        classpath 'org.greenrobot:greendao-gradle-plugin:3.2.2'
    }
}
```

其中，在build.gradle(Module:app)中对greenDao进行的配置可以让greenDao根据实体类，点击Make Project或Make Module 'app'自动创建DaoSession、DaoMaster、BeanDao三个类。

### greenDao核心类

#### DaoMaster

DaoMaster 保存数据库对象（SQLiteDatabase）并管理特定模式的 DAO 类（而不是对象）。它有静态方法来创建表或删除它们。它的内部类 OpenHelper 和 DevOpenHelper 是 SQLiteOpenHelper 实现，它们在 SQLite 数据库中创建模式。

#### DaoSession

管理特定模式的所有可用 DAO 对象，您可以使用其中一个getter方法获取该对象。DaoSession 还提供了一些通用的持久性方法，如实体的插入，加载，更新，刷新和删除。

#### XXXDao

据访问对象（DAO）持久存在并查询实体。对于每个实体，greenDAO 生成DAO。它具有比 DaoSession 更多的持久性方法，例如：count，loadAll 和 insertInTx。

#### Entities

可持久化对象。通常, 实体对象代表一个数据库行使用标准 Java 属性(如一个POJO 或 JavaBean )。

(![](https://raw.githubusercontent.com/HurleyJames/ImageHosting/master/greenDao%E6%A0%B8%E5%BF%83%E7%B1%BB.png))

### 实体类注解

```java
@Entity
public class User {
    @Id(autoincrement = true)
    private Long id;
    private String name;
    private int age;
}
```

相关注解说明：

#### 实体@Entity注解

使用@Entity注解让greenDao为其自动生成必要的代码

* schema：告知greenDao当前实体属于哪一个schema
* active：标记一个实体处于活跃状态，活动实体有更新、删除和刷新方法
* nameInDb：在数据库中使用的别名，默认使用的是实体的类名
* indexes：定义索引，可以跨越多个列
* createInDb：标记创建数据库表

#### 基础属性注解

* @Id：主键Long型，可以通过`d(autoincrement = true)`设置自增长
* @Property：设置一个非默认关系映射所对应的列名，默认是使用字段名，例如：`@Property(nameInDb = "name")`
* @NotNull：设置数据库表当前列不能为空
* @Transient：添加此标记后不会生成数据库表的列

#### 索引注解

* @Index：使用@Index作为一个属性来创建一个索引，通过name设置索引别名，也可以通过unique给索引添加约束
* @Unique：向数据库添加了一个唯一的约束

#### 关系注解

* @ToOne：定义与另一个实体（一个实体对象）的关系
* @ToMany：定义与多个实体对象的关系

### greenDao初始化

在Application或自定义的继承Application的类中进行初始化，维持全局会话。所以在此进行数据库的初始化操作：

```java
private DaoSession mDaoSession;

private void initGreenDao() {
    DaoMaster.DevOpenHelper helper = new DaoMaster.DevOpenHelper(this, "xxx.db");
    SQLiteDatabase db = helper.getWritableDatabase();
    DaoMaster daoMaster = new DaoMaster(db);
    daoMaster = daoMaster.newSession();
}

public DaoSession getDaoSession() {
    return mDaoSession;
}
```

