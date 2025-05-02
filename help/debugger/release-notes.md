---
title: Adobe Experience Platform Debugger 发行说明
description: Adobe Experience Platform Debugger 的最新发行说明。
keywords: debugger;experience Platform Debugger 扩展程序;chrome;扩展程序;发行说明
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: a5af5c194bc6b3bf9a6e119a2f147efa85f263f0
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 92%

---

# Adobe Experience Platform Debugger 发行说明

## 1.6.3版 — 2025年4月30日

### 修复和改进功能

* 修复了Debugger会导致DTM和Tags功能无法正常运行的问题。
* 修复了Analytics后处理点击不会显示在日志中的问题。
* 修复了日语等非ASCII语言的数据在日志中无法正确显示的问题。

## 版本1.6.2 - 2024年10月1日

### 修复和改进功能

* 修复了调试器对所有CSP错误过于敏感的问题

## 版本 1.6.1，2024 年 7 月 25 日

### 修复和改进功能

* 修复了阻止用户向没有标记的页面添加新标记嵌入代码的问题。

## 版本 1.6.0，2024 年 7 月 11 日

### 新增功能

* 允许用户选择启用/禁用技术和个人数据收集。

### 修复和改进功能

* 修复 Firefox 脚本注入和隐私政策链接。
* 捕获缺失的 Analytics 请求。
* 修复包含大量复杂控制台消息的页面崩溃问题。
* 将 Adobe Experience Platform Debugger 更新为 Manifest v3 扩展。

## 版本 1.5.4，2023 年 12 月 19 日

### 修复和改进功能

* 修复了无法保留设置的问题。
* 修复了查看 Analytics 后处理命中时导致 Debugger 崩溃的问题。

## 版本 1.5.3，2023 年 12 月 6 日

### 新增功能

* 添加了“打开 Debugger 时锁定到活动选项卡”的设置。

### 修复和改进功能

* 修复了专用域上缺少 Analytics 请求的问题。
* 修复了 Analytics 请求表中缺少活动地图数据的问题。
* 修复了查看 Target Trace 会导致崩溃的问题。
* 添加了当 Debugger 无法在 Firefox 中设置页面基础结构时会发出的警告。

## 版本 1.5.2 - 2023 年 11 月 10 日

（仅限 Firefox）

### 修复和改进功能

* 更新了对文件的组织形式。

## 版本 1.5.1 - 2023 年 11 月 2 日

### 修复和改进功能

* 修复了 Analytics 事件被忽略或重复的问题。
* 修复了超出最大状态存储大小的问题。
* 修复了 Edge Logs 搜索无法过滤事件的问题。

## 版本 1.5.0 - 2023 年 10 月 19 日

### 新增功能

* 在标记摘要和日志中显示属性、环境和规则的链接。

### 修复和改进功能

* 修复了未发送标记摘要数据的问题。
* 修复了 Assurance 会话会出现 CORS 错误的问题
* 修复了导致 Target Trace 无法出现的问题。
* 修复了“发送反馈”按钮。
* 修复了 Web SDK 摘要中版本≥2.18.0 内缺少的“数据流 ID”。
* 修复了 Edge 日志不可搜索的问题。
* 添加了关于某些帐户类型的附加轮廓的注释。

## 版本 1.4.1 - 2022 年 11 月 1 日

* 具有许多 Adobe Experience Platform Assurance 事件的页面的性能得到了提高。

## 版本 1.4.0 - 2022 年 10 月 3 日

* 增加了对 Web SDK 混合实施的 AEP Assurance 调试支持。
* 添加了对同一 AEP Assurance 会话中的多个选项卡的支持。
* 修复了用户登录后无法切换轮廓/组织的问题。
   * 对于某些帐户，需要注销并重新登录才能切换组织。
* 添加了启用 Target Trace 失败时发出的错误信息。
* 更新了依赖项。

## 1.3.3 版，2022 年 6 月 20 日 

* 修复了阻止从网络事件表打开弹出窗口的问题。
* 修复了阻止页面 Alloy 信息加载的问题。

## 1.3.2 版，2022 年 6 月 9 日 

* 增加了用户登录时的默认头像。
* 为日志中的 JSON 对象添加了语法突出显示功能。

## 1.3.1 版，2022 年 5 月 24 日 

* 更新了依赖项。
* 修复了无法启用后处理命中功能的 Analytics 问题。
* 修复了Debugger 会附加到 Adobe 登录窗口的问题。
* 修复了 AT.js 问题，该问题导致日志消息无法在 Debugger 中显示。

## 1.3.0 版，2022 年 1 月 28 日

* 添加了“关于”链接，以显示当前发布版本和说明。
* 添加了切换按钮，以查看 Analytics 请求的后处理命中情况。该切换按钮可在“分析”部分中使用。
* 修复了在 Debugger 外部关闭会话时会出现的远程调试会话问题。
* 修复了 Web SDK Edge Transactions 选项卡中可以看到的错误通知。
* 修复了当 Debugger 访问 _satellite 对象时页面上会出现 Adobe Tags 弃用警告的问题。
* 修复了一些在页面上找不到 AppMeasurement 实例的情况。
* 修复首次打开 Debugger 窗口时出现的页面连接问题。

## 版本 1.2.0 - 2021 年 10 月 26 日

* 在网络视图中显示所有浏览器选项卡的事件。要仅查看当前选项卡的事件，请选择 Debugger 右下角的锁定图标。
* 品牌化更新。

## 版本 1.1.0 - 2021 年 10 月 5 日

* 远程调试可视化功能：在 Adobe Experience Platform Web SDK > Edge Transactions 部分中将远程调试事件组织成可视化流程图。
* 在启动新的远程调试会话时，要求页面上使用的 Adobe Experience Platform Web SDK 组织与登录的组织相匹配。
* 仅显示已连接选项卡的 Edge Transactions。Target Trace 日志在“日志”>“边缘”部分中仍然可用。
* 允许对页面上的每个 Adobe Experience Platform Web SDK 实例进行单独的数据流 ID 配置覆盖。添加启用调试的切换功能。
* 修复了 Adobe Target 跟踪令牌并不总是通过 Adobe Experience Platform Web SDK 的远程调试会话发送的问题。

## 1.0.0 版 — 2021 年 5 月 5 日 

* Experience Platform Debugger 的第一个主要版本。旨在取代 Experience Cloud Debugger。
