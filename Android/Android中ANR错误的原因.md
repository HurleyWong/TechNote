## Android中ANR错误的原因

### 定义

ANR：在Android中，如果应用程序没有响应，则会出现ANR（Application Not Responding）错误。

### 原因

- 按键或触摸事件5s内无反应
- BroadcastReceiver在10s内无法完成处理
- Service在20s内无法处理完成
- UI主线程被其它操作阻塞
- 主线程存在耗时操作（本地IO操作、网络访问、循环等）

### 如何避免

- 合理使用UI主线程，耗时操作放入其它线程操作
- 合理使用Handler异步消息处理机制来处理其它线程请求
- 合理使用并遵循Android生命周期，避免在onCreate()和onResume()中做过多的事情
- 使用一些架构形成规范来避免内存等问题，例如：MVP模式、RxJava响应式编程等
- 避免内存泄漏引起的ANR
- 避免加载大图片引起内存不足导致ANR

### 总结

ANR异常主要的解决办法是不要在主线程中做耗时的操作，而应放在子线程中来实现，比如采用Handler+Message的方式，或者有时候需要做一些和网络交互的耗时操作就采用AsyncTask异步任务的方式（底层也是Handler+Message只不过是线程池）。