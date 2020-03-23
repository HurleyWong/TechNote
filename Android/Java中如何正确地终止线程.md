## Java中如何正确地终止线程

### Java中API自带的stop()方法终止线程

查阅JDK，不难发现Thread提供了一个stop()方法，但是stop()方法是一个废弃的方法。因为stop()方法太过于暴力，会强行把执行一半的线程终止。这样就不会保证线程的资源正确释放，通常是没有给与线程完成资源释放工作的机会，因此会导致程序工作在不确定的状态下。例如，有可能会造成不同步的例子。

### 使用boolean类型的变量，来终止线程

```java
public static class ChangeObjectThread extends Thread {
  // 用于停止线程
  private boolean stop = true;

  public void stop() {
    stop = false;
  }

  @Override
  public void run() {
    while(stop) {
      try {
        Thread.sleep(2000);
      } catch (InterruptedException e) {
        e.printStackTrace();
      }
      // 让出CPU，给其它线程执行
      Thread.yield();
    }
  }
}
```