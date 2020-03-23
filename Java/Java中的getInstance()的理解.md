## Java中的getInstance()的理解

`getInstance()`在单例模式下使用。

单例模式：一个类有且只有一个实例，不用Object object = new Object();这种方式实例化后去使用。

## getInstance()与new的区别

### new的使用

```
Object object = new Object();
```

这样就必须知道其它的Object的存在，而第二个Object也经常在当前的应用程序域中，可以被直接调用。

### getInstance()的使用

在主函数开始时调用，返回一个实例化对象，此对象是static的，在内存中保留着它的引用，即内存中有一块区域专门用来存放静态方法和变量，可以直接使用，调用多次返回同一个对象。

### 两者区别

大部分类（非抽象类/接口）等都可以使用new，new就是通过生产一个新的实例对象，或者在栈中声明一个对象，每部分的调用都是一个新的对象。

getInstance()是少部分类才有的一个方法，各自的实现也不同。getInstance()在单例模式（保证一个类仅有一个实例，并提供一个访问它的全局访问点）的类中常见，用来生成唯一的实例，getInstance()往往是static的。

- 对象使用之前通过getInstance()得到而不需要自己定义，用完之后不需要delete
- new一定要生成一个新的对象，分配内存；getInstance()则不一定要再次创建，它可以把一个已存在的引用给使用，所以在性能上优于new
- new创建后只能当次使用，而getInstance()可以跨栈区域使用，或者远程区域使用，所以getInstance()通常是创建static静态实例方法的