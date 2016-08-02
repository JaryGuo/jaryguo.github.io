---
layout: post
title: 虚幻引擎札记
categories: ComputerScience
---

	今天开始学习虚幻引擎，在这里记录看的过程的一些心得

## 如何获取源码

1. 官网注册
2. 完善Profile，在Profile中绑定自己的github账号
3. 在Github接受邀请，便可以去到UnrealEngine的Github页面。

## 源码

### 目录说明

引擎代码在Engine/Source/Runtime文件夹中。文件夹下分许多模块，每个模块都有2个目录:Private、Public。Private存放引擎底层代码（C++）实现, Public存放接口头文件。另外还有一个C#文件: *.Build.cs文件，应该是用来构建程序的文件。

引擎入口: LaunchWindows.cpp(on Windows) or LaunchMac.cpp(on Mac)

### LaunchWindows.cpp内容

- 入口:`WinMain`
- 宏: 
	- UE_BUILD_DEBUG: debug
	- UE_BUILD_SHIPPING: release
	- WITH_EDITOR: 带有编辑器模式
- MutexName: 设置互斥体，用来判断是否第一个打开的引擎实例。使用`CreateMutex`。
- 引擎入口:`GuardedMain`，如果要捕捉C++的Exception，则调用:`GuardedMainWrapper`。
- 退出: FEngineLoop::AppExit();

### Launch.cpp

- `GuardedMain`在Launch.cpp中定义。
- GEngineLoop为引擎实例，以下步骤皆为对这个对象的操作。
- 预初始化`EnginePreInit`。
- 如果是`WITH_EDITOR`，则调用`EditorInit`，正常情况调用`EngineInit`。
- 进入引擎循环`EngineTick`，通过全局变量GIsRequestingExit判断是否退出。
- 退出EditorExit，调用`GEngineLoop.Exit();`。



