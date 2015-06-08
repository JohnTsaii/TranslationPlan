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

图3-1
![runloop](/iOS%20Developer%20Library/Threading-Programming-Guide/runloop.jpg)

除了处理输入的源，运行循环也会生成关于运行循环行为的通知。注册*运行循环观察者*可以受到这些通知并使用他们在线程上做更多的处理。你可以使用**Core Foundation**在你的线程安装运行循环观察者。

下面的文章提供了更多关于运行循环的组成和它的操作的模式的信息。他们也描述了在处理事件时的不同时间生成的通知。

## 运行循环模式
一个_运行循环模式_是一个被监测的输入源和计时器的集合，并且属于该集合的观察者会被运行循环通知。每次运行你的运行循环时，你指定（显式或隐式的）一个特定的模式在其中运行。在运行循环期间，只有与该模式相关联的源会被监测并且允许他们提交它们的事件。(相似的，只有与该模式相关的观察者会被通知运行循环的进展。)与其他模式相关联的源，会持有新事件直到随后的循环被传递到适当的模式。

在你的代码中，你定义一个模式通过名称。*Cocoa 和 Core Foundation*都定义了一个默认模式和常用的模式，
在你的代码里通过名称来指定这几种模式。你可以自定义模式并指定它的名称通过简单的指定自定义的字符串。虽然分配给自定义模式的名称是任意的，这些模式的内容则不是。你必须确保为你创建的模式添加一个或多个输入源，计时器，或者运行循环的观察者是有用的。

你可以使用模式指定你的运行循环时过滤来自干扰源的事件。大多时候，你会在系统定义的“默认”模式下运行你的运行循环。然而在模态面板中会在“modal”模式下运行。在这种模式下，只有关于模态面板的源能提交事件到现场。对于一些次要的线程，在严格时间的操作里，你可以使用自定义的模式阻止低优先级源的提交的事件。

>**注意：**模式区别对待基于事件的源，模式并不是事件的类型。例如，你不会使用模式匹配只有鼠标点击事件或者键盘事件，你可以使用模式监听一组不同端口，暂停定时器，或者改变当前监视的源和运行循环观察者。
>

**表 3-1**列出了被Cocoa和Core Foundation定义的标准模式以及它们的描述何时去使用它们。该名称列中列出了你用来在你的代码里指定模式的实际常量。

**表 3-1** 预定义运行循环模式   

| Mode           | Name   |  Descripton                |
|----------------|--------|---------------------------|
| Default        | [NSDefaultRunLoopMode](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSRunLoop_Class/index.html#//apple_ref/c/data/NSDefaultRunLoopMode)(Cocoa) [kCFRunLoopDefaultMode](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFRunLoopRef/index.html#//apple_ref/c/data/kCFRunLoopDefaultMode)(Core Foundation)       | 默认模式是大多数操作之一。大多数的时候，你应该使用这种模式启动你的运行循环和配置你的输入源。|
| Connection     | NSConnectionReplyMode(Cocoa)        | Cocoa框架使用这种模式配合`NSConnection`对象去监听响应。你应该很少使用这种模式                       |
| Modal          | NSModalPanelRunLoopMode(Cocoa)       | Cocoa框架使用这种模式识别用于模态面板的事件                           |
| Event tracking | NSEventTrackingRunLoopMode(Cocoa)       | Cocoa框架使用这种模式限制在鼠标拖动循环和其他类型的用户界面的跟踪循环的传人事件                           |
| Commmon modes  | [NSRunLoopCommonModes](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSRunLoop_Class/index.html#//apple_ref/c/data/NSRunLoopCommonModes)(Cocoa) [kCFRunLoopCommonModes](kCFRunLoopCommonModes)(Core Foundation))     | 这是一个常用模式的可配置组。与之相关联的输入源的相关联的模式都在该群族中。对于Cocoa应用程序，这个集合默认包括了`default,modal和event tracking 模式`。Core Foundation应用程序刚开始只包括了`default`模式。你可以往集合中添加自定义的模式通过使用[CFRunLoopAddCommonMode](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFRunLoopRef/index.html#//apple_ref/c/func/CFRunLoopAddCommonMode)函数                          |

## 输入源
输入源异步提交事件到线程。事件的源取决于输入源的类型，这一般有两类。基于端口的输入源监测你的应用程序的*Mach*端口。自定义的输入源监测自定义源的事件。至于你的运行循环而言，它不应该考虑输入源是否基于端口或者自定义。系统定义实现了两种输入源你只需使用它。这两者唯一的区别在于它们如何被通知的。基于端口的源自动被内核通知，而自定义的源必须从其他的线程手动被通知。但你创建了一个输入源，你把它传递给是运行循环的一个或多哥模式。模式影响输入源在何时被监测。大多时候，你运行运行循环在默认的模式下，但你也可以指定一个自定的模式。如果输入源不在适当的监测模式下，任何在运行循环执行期间生成的事件会被保留知道运行循环在适当的模式下运行。

接下来的段落描述了一些输入源。

### 基于端口输入源
**Cocoa**和**Core Foundation**提供了内置了支持通过使用端口相关的对象和函数创建基于端口输入源。例如，在**Cocoa**中，你不用直接的创建一个输入源，你只需简单的创建一个端口对象并使用[NSPort](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSPort_Class/index.html#//apple_ref/occ/cl/NSPort)的方法添加端口到运行循环。这个端口对象为你处理创建和配置需要的操作。

在**Core Foundation**中，你必须手动的创建接口和它的2运行循环源。在这两种情况下，你使用有关于不透明类型的端口方法([CFMachPortRef](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFMachPortRef/index.html#//apple_ref/c/tdef/CFMachPortRef)[CFMessagePortRef](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFMessagePortRef/index.html#//apple_ref/c/tdef/CFMessagePortRef),[CFSocketRef](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFSocketRef/index.html#//apple_ref/c/tdef/CFSocketRef))创建合适的对象.

如何设置和配置自定义基于端口的源的例子，请参考[Configuring a Port-Based Input Source](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html#//apple_ref/doc/uid/10000057i-CH16-131281)。

### 自定义输入源
为了创建一个自定义的输入源，你必须使用在**Core Foundation**中有关[CFRunLoopSourceRef](https://developer.apple.com/library/ios/documentation/CoreFoundation/Reference/CFRunLoopSourceRef/index.html#//apple_ref/c/tdef/CFRunLoopSourceRef)的不透明类型函数。你配置自定义输入源通过使用几个回调函数。**Core Foundation**调用这些函数在不同的点去配置这个源，处理任何传入的事件，并当它被移除运行循环时拆除这个源。
