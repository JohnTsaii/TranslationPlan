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
视图窗口是[UIWindow](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIWindow_Class/index.html#//apple_ref/occ/cl/UIWindow)的实例[这是个连接](https://github.com/JohnTsaii/TranslationPlan/edit/master/iOS%20Developer%20Library/ViewProgrammingGuideforiOS/Introduction.md/ "概览")
