# [运行循环](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-SW1)

运行循环是线程编程有关的基础机制的一部分。_运行循环_是一个事件处理循环，你用它来安排工作并协调接受传入事件。循环运行
目的之一是，当有任务需要处理时保持你线程的繁忙，当没有任务时使线程休眠。

运行循环不是完全自动管理的。你仍然必须设计你线程的代码在合适的时候去启动运行循环并响应输入事件。**Cocoa Foundation**
和**Core Foundation**都提供了_运行循环对象_帮助你配置和管理你线程的运行循环。你不必在你的应用程序中明确的去创建这些
对象;每个线程，包括应用程序的主线程，都有一个与之相联系的运行循环对象。然而，只有次要的线程需要明确的执行运行循环。
应用框架会自动的设置和执行在主线程中的运行循环作为应用程序的启动程序的一部分。

接下来的段落提供了更多关于运行循环和怎么为你的应用程序配置他们的信息。更多关于运行循环对象，请参考[NSRunLoop CLass Reference](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSRunLoop_Class/index.html#//apple_ref/doc/uid/TP40003725)和
[CFRunLoop Reference](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFRunLoopRef/index.html#//apple_ref/doc/uid/20001441)。

## 运行循环解析
运行循环闻如其名，它是一个循环的线程入口并用来响应输入事件的执行事件程序。你的代码提供了控制语句用来实现运行循环的实际循环部分--换句话说，你的代码提供了驱动运行循环的`while`或者`for`循环。在你的循环里，你使用运行循环对象去“执行”接受事件并且安装处理程序的事件处理代码。

运行循环接受两种不同类型源的事件。*Input sources*提供异步事件，消息通常来自不同的线程或者不同的应用程序。*Time sources*提供同步事件，通常发生在预定时间或重复的时间间隔。当事件到达时，这两种类型的源使用一个应用特定处理程序处理事件。

图3-1 显示了运行循环的概念结构和多种源。*Input sources*提供了异步事件到相应的处理程序并导致[runUntilDate:](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSRunLoop_Class/index.html#//apple_ref/occ/instm/NSRunLoop/runUntilDate:)方法(在线程相关联的[NSRunLoop](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSRunLoop_Class/index.html#//apple_ref/occ/cl/NSRunLoop)对象上被调用)退出执行。*Timer sources*提供事件到它的处理程序但不会导致运行循环退出执行。

除了处理输入的源，运行循环也会生成关于运行循环行为的通知。注册*运行循环观察者*可以受到这些通知并使用他们在线程上做更多的处理。你可以使用**Core Foundation**在你的线程安装运行循环观察者。

下面的文章提供了更多关于运行循环的组成和它的操作的模式的信息。他们也描述了在处理事件时的不同时间生成的通知。

## 运行循环模式
一个_运行循环模式_是一个被监测的输入源和计时器的集合，并且运行循环的观察者的集合会被通知。每次运行你的运行循环时，你指定（显式或隐式的）一个特定的模式在其中运行。在运行循环期间，只有与该模式相关联的源会被监测并且允许他们提交它们的事件。(相似的，只有与该模式相关的观察者会被通知运行循环的进展。)与其他模式相关联的源，会持有新事件直到随后的循环被传递到适当的模式。

在你的代码中，你定义一个模式通过名称。*Cocoa 和 Core Foundation*都定义了一个默认模式和常用的模式，
在你的代码里通过名称来指定这几种模式。你可以自定义模式并指定它的名称通过简单的指定自定义的字符串。虽然分配给自定义模式的名称是任意的，这些模式的内容则不是。你必须确保为你创建的模式添加一个或多个输入源，计时器，或者运行循环的观察者是有用的。

你可以使用模式指定你的运行循环时过滤来自干扰源的事件。大多时候，你会在系统定义的“默认”模式下运行你的运行循环。然而在模态面板中会在“modal”模式下运行。在这种模式下，只有关于模态面板的源能提交事件到现场。对于一些次要的线程，在严格时间的操作里，你可以使用自定义的模式阻止低优先级源的提交的事件。
