# [运行循环](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1)

运行循环是线程编程有关的基础机制的一部分。_运行循环_是一个事件处理循环，你用它来安排工作并协调接受传入事件。循环运行
目的之一是，当有任务需要处理时保持你线程的繁忙，当没有任务时使线程休眠。

运行循环不是完全自动管理的。你仍然必须设计你线程的代码在合适的时候去启动运行循环并响应输入事件。**Cocoa Foundation**
和**Core Foundation**都提供了_运行循环对象_帮助你配置和管理你线程的运行循环。你不必在你的应用程序中明确的去创建这些
对象;每个线程，包括应用程序的主线程，都有一个与之相联系的运行循环对象。然而，只有次要的线程需要明确的执行运行循环。
应用框架会自动的设置和执行在主线程中的运行循环作为应用程序的启动程序的一部分。

接下来的段落提供了更多关于运行循环和怎么为你的应用程序配置他们的信息。更多关于运行循环对象，请参考[NSRunLoop CLass Reference](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSRunLoop_Class/index.html#//apple_ref/doc/uid/TP40003725)和
[CFRunLoop Reference](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFRunLoopRef/index.html#//apple_ref/doc/uid/20001441)。
