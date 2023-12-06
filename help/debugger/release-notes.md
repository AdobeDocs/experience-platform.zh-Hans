---
title: Adobe Experience Platform Debugger发行说明
description: Adobe Experience Platform Debugger 的最新发行说明。
keywords: debugger;experience Platform Debugger 扩展程序;chrome;扩展程序;发行说明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 5ec61e3822cf42bdb89b24a17782b40cbd9dab37
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 4%

---

# Adobe Experience Platform Debugger发行说明

## 1.5.3版 — 2023年12月6日

### 新增功能

* 添加了“打开Debugger时锁定活动选项卡”设置。

### 修复和改进功能

* 修复了专用域中缺少Analytics请求的问题。
* 修复了Analytics请求表中缺少Activity Map数据的问题。
* 修复了查看目标跟踪会导致崩溃的问题。
* 当调试器无法在Firefox中设置页面上的基础结构时添加了警告。

## 版本1.5.1 - 2023年11月2日

### 修复和改进功能

* 修复了Analytics事件将被忽略或重复的问题。
* 修复了超出最大状态存储大小的问题。
* 修复了边缘日志搜索无法过滤事件的问题。

## 1.5.0版 — 2023年10月19日

### 新增功能

* 在标记摘要和日志中显示指向属性、环境和规则的链接。

### 修复和改进功能

* 修复了标记摘要数据未发送的问题。
* 修复了保障会话会发出CORS错误的问题
* 修复了导致无法显示Target跟踪的问题。
* 修复了“发送反馈”按钮。
* 修复了Web SDK摘要(版本≥2.18.0)中缺少“数据流ID”的问题。
* 修复了边缘日志不可搜索的问题。
* 添加了关于某些帐户类型的其他配置文件的说明。

## 版本1.4.1 - 2022年11月1日

* 提高了包含许多Adobe Experience Platform保证事件的页面的性能。

## 版本1.4.0 - 2022年10月3日

* 为Web SDK混合实施添加了AEP保障调试支持。
* 在同一AEP保障会话中添加了对多个选项卡的支持。
* 修复了用户在登录后无法切换用户档案/组织的问题。
   * 对于某些帐户，需要注销并重新登录才能切换组织。
* 添加了启用Target跟踪失败时的错误消息。
* 更新了依赖关系。

## 1.3.3版 — 2022年6月20日

* 修复了阻止从网络事件表中打开弹出窗口的问题。
* 修复了阻止加载页面上Alloy信息的问题。

## 版本1.3.2 - 2022年6月9日

* 添加了用户登录时的默认头像。
* 为日志中的JSON对象添加了语法突出显示。

## 1.3.1版 — 2022年5月24日

* 更新了依赖关系。
* 修复了无法启用后处理点击的Analytics问题。
* 修复了Debugger附加到Adobe登录窗口的问题。
* 修复了日志消息无法在Debugger中显示的AT.js问题。

## 1.3.0版 — 2022年1月28日

* 添加了关于链接以显示当前发行版本和说明。
* 添加了用于查看Analytics请求的后处理点击的切换功能。 该切换在Analytics部分中可用。
* 修复了在调试器之外关闭会话时的远程调试会话问题。
* 修复了在Web SDK的“边缘事务”选项卡中显示的错误通知。
* 修复了Adobe访问_satellite对象时出现的页面弃用警告。
* 修复了在页面上找不到AppMeasurement实例的一些情况。
* 修复了首次打开调试器窗口时发生的页面连接问题。

## 版本1.2.0 - 2021年10月26日

* 在网络视图中显示所有浏览器选项卡中的事件。 要仅查看当前选项卡中的事件，请选择Debugger右下角的锁定图标。
* 更新了品牌。

## 版本1.1.0 - 2021年10月5日

* 远程调试可视化图表 — 在Adobe Experience Platform Web SDK > Edge Transactions部分将远程调试事件组织为可视化流程图。
* 启动新的远程调试会话时，要求页面上使用的Adobe Experience Platform Web SDK组织与登录的组织匹配。
* 仅显示已连接选项卡的边缘事务。 目标跟踪日志仍在“日志”>“边缘”部分中可用。
* 允许为页面上的每个Adobe Experience Platform Web SDK实例覆盖单独的数据流ID配置。 “添加调试已启用”切换开关。
* 修复了Adobe Target跟踪令牌未始终随Adobe Experience Platform Web SDK的远程调试会话一起发送的问题。

## 1.0.0版 — 2021年5月5日

* Experience PlatformDebugger的第一个主要版本。 旨在更换Experience Cloud Debugger。
