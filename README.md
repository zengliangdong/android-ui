# 从setContentView开始了解View的加载过程

Actvity中的onCreate方法中的setContentView到底做了些什么？\(PS:以下代码是基于Android 25\)

我们看下Activity的setContentView源码，发现最终有掉用Window的setContentView方法（其实是Window的子类PhoneWindow的setContentView方法）。![](/assets/import.png)继续查看PhoneWindow 类中的setContentView![](/assets/import1.png)mContentParent 是一个ViewGroup，如果mContentParent为null，则执行installDecor方法![](/assets/import3.png)![](/assets/import4.png)![](/assets/import5.png)mDecor是DecorView（继承自FrameLayout）。generateDecor中会创建并返回DecorView。

generateLayout方法中会通过getWindowStyle方法返回Window的TypedArray（包括Window\_windowFullscreen

 、Window\_windowTranslucentStatus、Window\_windowContentTransitions等等）同时非常关键的是在该方法中掉用DecorView的onResourcesLoaded方法\(该方法会把layoutResource对应的布局文件返回的View添加到DecorView中\)

![](/assets/import6.png) 

 最后generateLayout方法中通过findViewById\(ID\_ANDROID\_CONTENT\)返回一个ViewGroup。



PS：requestFeature为什么要在setContentView之前调用？

![](/assets/import7.png)

 可以看到requestFeature方法有对mFeatures、mLocalFeatures进行赋值，Activity掉用setContentView方法最终会掉用PhoneWindow的generateLayout方法同时通过getLocalFeatures方法返回mLocalFeatures，通过mLocalFeatures值加载不同的系统布局文件\(layoutResource\)，传给mDecor.onResourcesLoaded\(mLayoutInflater,layoutResource\)。



 

 

 

 

 

