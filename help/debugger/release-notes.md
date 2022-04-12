---
title: 发行说明
description: Adobe Experience Platform Debugger的最新发行说明。
keywords: debugger;experience Platform Debugger 扩展程序;chrome;扩展程序;发行说明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

# 发行说明

## 1.3.0版 — 2022年1月28日

* 添加了关于链接以显示当前发行版本和说明。
* 添加了用于查看Analytics请求的处理后点击的切换开关。 切换在Analytics部分中可用。
* 修复了在调试器外部关闭会话时的远程调试会话问题。
* 修复了在Web SDK边缘事务选项卡中显示的错误通知。
* 修复了当调试器访问_satellite对象时，页面上的Adobe标记弃用警告。
* 修复了在页面上未找到AppMeasurement实例的某些情况。
* 修复了首次打开调试器窗口时发生的页面连接问题。

## 1.2.0版 — 2021年10月26日

* 在“网络”视图中显示所有浏览器选项卡中的事件。 要仅从当前选项卡中查看事件，请选择Debugger右下角的锁图标。
* 更新了品牌策略。

## 1.1.0版 — 2021年10月5日

* 远程调试可视化 — 在Adobe Experience Platform Web SDK >边缘事务部分中，将远程调试事件组织到可视化流程图中。
* 启动新的远程调试会话时，需要页面上使用的Adobe Experience Platform Web SDK IMS组织与登录组织相匹配。
* 仅显示连接选项卡的边缘事务。 Target跟踪日志仍在“日志”>“Edge”部分中可用。
* 允许为页面上Adobe Experience Platform Web SDK的每个实例单独覆盖数据流ID配置。 添加已启用调试的切换开关。
* 修复了Adobe Target跟踪令牌并非总是随Adobe Experience Platform Web SDK的远程调试会话一起发送的问题。

## 1.0.0版 — 2021年5月5日

* Debugger的第一个主要版本。 用于替换Experience Cloud Debugger。
