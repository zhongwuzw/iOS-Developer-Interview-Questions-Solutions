# iOS 开发面试问题

根据[iOS开发面试问题](https://github.com/lzyy/iOS-Developer-Interview-Questions) 写了部分答案。

**Update: 20180228 
突然发现几年前创建了这个`Repo`，还是更新一下吧，Sigh.**

面试 iOS 开发时，切入点很重要，不同的切入点会导致不同的结果，没有找到合适的切入点也无法对应聘者有一个全面的了解。所以这份面试问题列表更多的是提供方向，没有固定的答案，而且可以根据应聘者的回应引出更多有意思深层次的讨论。

如果有不错的问题，欢迎 Pull Request :)

## 一般性问题
* 最近这两天你有学到什么知识/技能么？
* 最近有做过比较酷或者比较有挑战的项目么？
* 最近看过的书/文章有哪些？
* 如何向一个只接触过互联网的孩子解释「电视」？
* 为什么要学习编程，编程对你而言的乐趣在哪儿？
* 如果一个函数10次中有7次正确，3次错误，问题可能出现在哪里？
* 自身最大优点是什么，怎么证明？
* 有没有在 GitHub 上发布过开源代码，参与过开源项目？
* 你最近遇到过的一个技术挑战是什么？怎么解决的？
* 开发常用的工具有哪些？
* 熟悉 CocoaPods 么？能大概讲一下工作原理么？
* 最常用的版本控制工具是什么，能大概讲讲原理么？
* 今年你最想掌握的一门技术是什么？为什么？目前已经做到了哪个程度？
* 你一般是怎么用 Instruments 的？
* 你一般是如何调试 Bug 的？
* 你在你的项目中用到了哪些设计模式？
* 如何实现单例，单例会有什么弊端？
* iOS 是如何管理内存的？

## 知识性问题
* 什么是响应链，它是怎么工作的？ 

 **具体可参考**[iOS事件处理之Hit-Testing](https://zhongwuzw.github.io/2016/09/12/iOS%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E4%B9%8BHit-Testing/)

* 如何访问并修改一个类的私有属性？ 

 1. **通过KVC,`setValue:forKeyPath:`方法。**
 2. **对于property，可以使用`- (id)performSelector:(SEL)aSelector withObject:(id)anObject`，不过注意，属性值只能是`id`，也就是`Objective-C`类型**。
 3. **使用`NSInvocation`来进行设置**。
 4. **通过`objc_msgSend`发送`setProperty`来进行设置**。
 5. **通过`class_getInstanceMethod`拿到`Method`，再调用`method_invoke(id receiver, Method m, ...)`来调用`setter`**。
 6. **其它运行时方法不再赘述**。
 
* iOS Extension 是什么？能列举几个常用的 Extension 么？
 
 **通过使用扩展，可以让我们在应用外实现一些自定义的功能，这样，我们可以在其它的`App`或系统中进行交互。我们经常用的比如输入法，照片编辑、分享等等。**
 
* 如何把一个包含自定义对象的数组序列化到磁盘？

 **对象实现NSCoding协议，其父类同样需要实现。**
 
* Apple Pay 是什么？它的大概工作流程是怎样的？

 **不赘述，参见**[Apple Pay实现原理](https://www.zhihu.com/question/40502548)

* iOS 的沙盒目录结构是怎样的？ App Bundle 里面都有什么？ 

 **包括`Documents`、`Library`、`tmp`等。`Application Bundle`包括`Info.plist`，可执行文件，资源文件及其它文件，比如`frameworks`**。

* iOS 的签名机制大概是怎样的？
* iOS 7的多任务添加了哪两个新的 API? 各自的使用场景是什么？<p>**定时fetch内容以及push唤醒并下载内容。**
* Objective-C 的 `class` 是如何实现的？`Selector` 是如何被转化为 C 语言的函数调用的？

 **几句话很难讲清楚，直接上源码吧，我创建的项目，加了中文注释。**[objc4-cn](https://github.com/zhongwuzw/objc4-cn)

* `UIScrollView` 大概是如何实现的，它是如何捕捉、响应手势的？
 
 **改变一个视图的bounds.origin后，它每一个单独的子视图都会被移动，这就是UIScrollView工作的原理，当你设置它的contentOffset属性时它改变scroll view.bounds的origin。手势应该是使用手势识别器实现的。**
 
* Objective-C 如何对已有的方法，添加自己的功能代码以实现类似记录日志这样的功能？
 
 **利用OC的运行时特性，运用swizzling Method方法即可实现。**
 
* `+load` 和 `+initialize` 的区别是什么？

 **时机不一样；当涉及到继承、类别等时，调用的情况也不一样**。参见[源码](https://github.com/zhongwuzw/objc4-cn)
 
* 如何让 Category 支持属性？

 **使用关联引用。**
 
* `NSOperation` 相比于 GCD 有哪些优势？

 **NSOperation加入到queue的操作可以取消，NSOperation优先级设置、依赖等比较方便。**
 
* `strong` / `weak` / `unsafe_unretained` 的区别？

 **weak会在对象引用计数变为0时置为nil，而unsafe_unretained不会，所以当指向对象释放后，再访问时可能导致崩溃。**
 
* 如何为 Class 定义一个对外只读对内可读写的属性?

 **在头文件中定义属性，关键字为readonly，在实现文件中定义扩展，在扩展中重新定义属性即可，默认可读写。**
 
* Objective-C 中，meta-class 指的是什么？

 **元类中包含类方法，isa及superclass指针。参考[objc4-cn](https://github.com/zhongwuzw/objc4-cn)**
 
* `UIView` 和 `CALayer` 之间的关系？

 **UIView依靠CALayer来做渲染管理。**
 
* `+[UIView animateWithDuration:animations:completion:]` 内部大概是如何实现的？
 **封装了CABasic动画。**
 
* 什么时候会发生「隐式动画」？

 **改变视图非基础图层的CALayer时。**
 
* 如何处理异步的网络请求？
* `frame` 和 `bounds` 的区别是什么？

 **frame相对于父视图坐标系，bounds是自己的坐标系，供子视图参考。**
 
* 如何把一张大图缩小为1/4大小的缩略图？

 **使用GraphicContext**
 
* 一个 App 会处于哪些状态？

 ![](https://raw.githubusercontent.com/zhongwuzw/zhongwuzw.github.io.resource/master/images/app-state.png)

* Push Notification 是如何工作的？
* 什么是 Runloop？

 具体实现可以参考[源码]([objc4-cn](https://github.com/zhongwuzw/objc4-cn))，简单可以理解成，`RunLoop`就是一个`while(1){}`的循环，每次进行循环时，获取需要处理的事件分发，当没有任何事件需要处理时则休眠。

* Toll-Free Bridging 是什么？什么情况下会使用？

 **C和OC之间的转换，涉及到对象所有权的管理。**
 
* 当系统出现内存警告时会发生什么？

 **除了调用方法让用户处理外，系统默认移除当前不可见的controller的view。**
 
* 什么是 `Protocol`，Delegate 一般是怎么用的？
* autorelease 对象在什么情况下会被释放？

 `autorelease`对象内存由`NSAutoreleasePool`进行管理，当程序离开其范围时，向管理的`autorelease`对象发送`release`进行。

* UIWebView 有哪些性能问题？有没有可替代的方案。

 **UIWebView存在内存泄露，`JavaScript`渲染引擎受限，在主线程进行大量操作；使用私有`API`开启`WebThread`线程渲染，如`_setDrawInWebThread`/`_setDrawsCheckeredPattern`等；使用WKWebView替换。**
 
* 为什么 NotificationCenter 要 removeObserver? 如何实现自动 remove?

 **如果不remove，当observer释放后，NotificationCenter会继续向其发送通知，此时会导致崩溃。实现自动remove方法：使用一个对象作为其关联对象，当对象释放时会调用关联对象的dealloc方法，在该方法中移除即可。注意，如果`App`的`target`是`iOS9.0`及以后，则不再需要进行`removeObserver`操作**
 
 
* 当 `TableView` 的 `Cell` 改变时，如何让这些改变以动画的形式呈现？
* 什么是 `Method Swizzle`，什么情况下会使用？

## 经验类问题
* 为什么 `UIScrollView` 的滚动会导致 `NSTimer` 失效？

 **NSTimer涉及到RunLoop Mode，当滑动时，模式处于UITrackingRunLoopMode，导致原模式下的Timer失效。**
 
* 为什么当 Core Animation 完成时，layer 又会恢复到原先的状态？
 **动画的过程涉及到绘图原理，动画是在presentationLayer上实现，而Layer原来的状态都是保存在modelLayer，改变presentationLayer属性并不会改变modelLayer的值。**
 
* 你会如何存储用户的一些敏感信息，如登录的 token。

 **使用keychain。**
 
* 有用过一些开源组件吧，能简单说几个么，大概说说它们的使用场景实现。
* 什么时候会发生 `EXC BAD ACCESS` 异常？

 **访问僵尸对象。**
 
* 什么时候会使用 Core Graphics，有什么注意事项么？
* NSNotification 和 KVO 的使用场景？
* 使用 Block 时需要注意哪些问题？

 **循环引用吧。**
 
* `performSelector:withObject:afterDelay:` 内部大概是怎么实现的，有什么注意事项么？
* 如何播放 GIF 图片，有什么优化方案么？
* 使用 `NSUserDefaults` 时，如何处理布尔的默认值？(比如返回 NO，不知道是真的 NO 还是没有设置过)

 **先使用objectForKey判断是否为nil。**
 
* 有哪几种方式可以对图片进行缩放，使用 CoreGraphics 缩放时有什么注意事项？
* 哪些途径可以让 ViewController 瘦下来？
* 有哪些常见的 Crash 场景？

 **对象无法响应selector；未移除observer；访问已释放对象；数组越界**
 

## 综合类问题
* 设计一个可以无限滚动并且支持自动滚动的 SlideShow。
* 设计一个进度条。
* 设计一套大文件（如上百M的视频）下载方案。

 切片分段多线程并发下载。

* 如果让你来实现 `dispatch_once`，你会怎么做？

 使用原子变量，做好内存序使所有线程可见。
 
* 设计一个类似 iOS 主屏可以下拉出现 Spotlight 的系统。(对 UIScrollView 的理解程度)

## 编程实现
* 简述[「Snakes and Ladders」](http://en.wikipedia.org/wiki/Snakes_and_Ladders)的实现思路(这道题比较容易阐述清楚，且难度适中)

## 参考

* http://way2ios.com/development/ios-development-2/iphone-interview-question-answers/
* https://blackpixel.com/writing/2013/04/interview-questions-for-ios-and-mac-developers-1.html
* https://github.com/CameronBanga/iOS-Developer-and-Designer-Interview-Questions


