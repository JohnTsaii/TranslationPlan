# [引言](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503-CH1-SW2)

## 关于视图窗口和视图  
  在iOS系统中，你使用视图窗口和视图去呈现你的应用内容在屏幕上。视图窗口本身是没有任何可视内容，但是，他为你的应用视
图提供了一个基础的容器(作者:就是作为一个视图容器的作用)。视图定义了视图窗口需要填充的一部分内容。例如，你可能有视
图用来显示图片，文本，图形，或者他们的一些组合内容。你也可以使用视图去组织和管理其他的视图。

## 概览
  每个应用至少有一个视图窗口和一个视图去呈现它的内容。UIKit以及其他的系统框架提供了一些已定义的视图，你可以使用它们来呈现你的内容。这些视图的种类从简单的按钮和文本标签到复杂的视图，比如列表视图，选择视图，和滚动视图。在某些场合系统已定义的视图满足不了你的需求，你可以定义自己的视图和管理视图的绘制和视图的事件处理。  

## 视图管理你的应用的可视化内容
视图是UIView类（或者是他的基类）的实例，它管理一个在视图窗口中的矩形区域。视图负责绘制内容，处理多点触摸事件，并管理子视图的布局。绘图涉及使用图形技术,如Core Graphics,OpenGL ES,或者UIKit来绘制形状，图像和视图的矩形区域内的文本。视图响应在它的矩形区域内的触摸事件通过手势识别或者直接处理触摸事件。在视图层次结构中，父视图负责确定位置和设置子视图的坐标并且能动态的设置坐标和大小。这种能力能够动态的改变子视图让你的视图适应不断变化的条件，比如界面的旋转和变化。

> 相关文章：[视图和视图窗口的结构](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/WindowsandViews/WindowsandViews.html#//apple_ref/doc/uid/TP40009503-CH2-SW1),[视图](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingViews/CreatingViews.html#//apple_ref/doc/uid/TP40009503-CH5-SW1)

## 视图在视图窗口坐标的显示
视图窗口是[UIWindow](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/cl/UIWindow)的实例它负责处理应用程序的用户界面整体的外观。视图窗口作用于管理视图（和其所属的视图管理器）上的交互和改变。在大多数情况下，你的应用的视图窗口永远不会改变。在视图窗口被创建后，它保持不变并且只能改变视图的显示。每个应用程序至少有一个视图窗口来显示在设备主界面的用户界面。如果一个应用外部显示的界面被连接到设备，应用也会在屏幕上创建第二个视图窗口来呈现内容。

> 相关文章：[视图窗口](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/CreatingWindows/CreatingWindows.html#//apple_ref/doc/uid/TP40009503-CH4-SW1)

## 动画为用户界面改变提供了可视的反馈
动画为用户提供了可视的反馈当你的视图层级改变时。系统为展示模态视图和不同群体视图的转换定义了标准的动画。然而视图的许多属性可以直接通过动画处理。比如，通过动画可以改变视图的透明度，在屏幕上的位置，它的大小，它的背景颜色，或者其它属性。并且如果你直接操作视图动画通过**_Core Animation_**层的对象，你也可以通过它执行其它许多动画。

> 相关文章：[动画](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/AnimatingViews/AnimatingViews.html#//apple_ref/doc/uid/TP40009503-CH6-SW1)

## 界面构建器的作用
界面构建器是应用用来图形化构建并设置你的应用的视图窗口和视图。使用界面构建器，你可以在[nib 文件](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009503)里组件你的视图，它是存储视图固定的版本和其他目标文件的资源文件。当你运行时加载nib文件，里面的目标文件会被恢复成实际的对象，你可以通过代码手动管理它们。

界面构建器大大简化了你在创建应用程序用户界面所需的工作。因为对界面构建器和nib文件的支持是被纳入整个iOS的，只需一点努力你可以纳入nib文件到你的应用程序。
更多关于如何使用界面构建器的资料，请参考_Interface Builder User Guide_.关于视图控制器如何管理在它们视图里的nib文件的资料，请参考[Creating Custom Content View Controllers](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/BasicViewControllers/BasicViewControllers.html#//apple_ref/doc/uid/TP40007457-CH101)在[View Controller Programming Guide for iOS](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/BasicViewControllers/BasicViewControllers.html#//apple_ref/doc/uid/TP40007457-CH101)。

## 另请参考
因为视图是非常复杂和灵活多变的对象，不可能在一个文档中覆盖它所有的行为特性。然而，其他文件可以帮助你了解其他关于作为一个整体去管理视图和你的用户界面。
* 视图控制器作为管理你应用程序视图是一个重要的部分。视图控制器管理所有的视图在单个视图层次上，并且能便捷的呈现视图在屏幕上。更多关于视图控制器和它的作用，请参考[View Controller Programming Guide for iOS](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40007457)。
* 在你的应用程序中视图是手势和触摸时间的关键接受方。更多关于直接使用手势识别和处理触摸事件，请参考[Event Handling Guide for iOS](https://developer.apple.com/library/ios/documentation/EventHandling/Conceptual/EventHandlingiPhoneOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009541)。
* 自定义视图必须使用现有的技术区渲染它们的内容。更多关于使用这些技术绘制你的视图，请参考[Drawing and Printing Guide for iOS](https://developer.apple.com/library/ios/documentation/2DDrawing/Conceptual/DrawingPrintingiOS/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010156)。
* 如果标准的视图动画满足不了你的需求，尼克使用_核心动画_。更多关于使用_核心动画_实现动画，请参考[Core Animation Programming Guide](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CoreAnimation_guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004514)。
