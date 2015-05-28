# 简介
Quartz 2D 是一种先进的使用于iOS应用开发和除了内核之外的所有Mac OS X应用开发的二维绘图引擎。Quart 2D 提供了底层轻量级
的2D渲染，并且无论显示设备或打印设备都能做到高保真。Quartz 2D是于分辨率和设备无关的。当你使用Quartz 2D应用程序编程接
口绘图时，你不必考虑最终的目的。

Quartz 2D API易于使用，并提供了强大的功能，比如透明层，基于路径的绘制，屏幕外渲染，先进的色彩管理，抗锯齿渲染，和PDF
文件的创建，显示和解析。

Quartz 2D API 是**_Core Graphics framework_**的一部分,因此你可以把把他当成**_Core Graphics_**或者更简单，CG.

## 谁需阅读本文件？
此文档是为了iOS和MAC OS X开发者需要使用以下的功能时：
* 绘制图形
* 应用程序需要提供图形编辑能力
* 创建或者显示位图图像
* 使用PDF文档

## 文档结构
此文档由以下文章组成：
* [Overview of Quartz 2D](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_overview/dq_overview.html#//apple_ref/doc/uid/TP30001066-CH202-TPXREF101)
文章介绍了，绘制目的，Quartz 2D 不透明的数据类型，图形状态，坐标和内存管理，而且观察Quartz在“引擎盖下”是如何工作的。
* [Graphics Contexts](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_context/dq_context.html#//apple_ref/doc/uid/TP30001066-CH203-TPXREF101)
介绍了各种绘画目的，并提供一步一步说明创建图形上下文的特色。
* [Paths](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_paths/dq_paths.html#//apple_ref/doc/uid/TP30001066-CH211-TPXREF101)
讨论了组成路径的基本元素，展示如何去创建和绘制他们，展示如何建立剪切区域，并解释了混合模式如何影响绘图。
* [Color and Color Spaces](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_color/dq_color.html#//apple_ref/doc/uid/TP30001066-CH205-TPXREF101)
讨论颜色的值和使用alpha值的透明度，并介绍如何创建一个色彩空间，色彩设置，创建颜色对象，并设置渲染的意向。
