## getActivity()与getContext()的区别

Activity与Application都是Context的子类。Context是上下文的意思，在实际应用中起到管理上下文环境中各个参数和变量的作用，方便简单的访问各种资源。

虽然Activity和Application都是Context的子类，但是它们维护的生命周期不一样。前者维护一个Activity的生命周期，所以会其对应的Context也只能访问该activity内的资源。后者是维护一个Application的生命周期。

`getActivity()`和`getContext()`其实差不多，一般在Fragment中使用。