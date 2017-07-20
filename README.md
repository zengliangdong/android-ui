#              从setContentView开始了解View的加载过程

Actvity中的onCreate方法中的setContentView到底做了些什么？

我们看下Activity的setContentView源码，发现最终有掉用Window的setContentView方法（其实是Window的子类PhoneWindow的setContentView方法）。![](/assets/import.png)继续查看PhoneWindow 类中的setContentView![](/assets/import1.png)

