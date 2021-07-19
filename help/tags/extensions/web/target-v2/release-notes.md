---
title: Adobe Target v2扩展的发行说明
description: Adobe Experience Platform中Adobe Target v2标记扩展的最新发行说明。
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 55%

---

# Adobe Target v2扩展发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch正在Experience Platform中被重新命名为一套数据收集技术。 因此，在产品文档中推出了一些术语更改。 有关术语更改的统一参考，请参阅以下[文档](../../../term-updates.md)。

## 2021 年 5 月 19 日

### Adobe Target v2 扩展 0.14.1

- 修复了v0.14版本中引入的回归问题，在该版本中，Load Target操作会触发全局mbox调用

## 2021 年 5 月 14 日

### Adobe Target v2 扩展 0.14

- 添加了新的操作Load Target with [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning)，该工具加载了at.js 2.5，且具备设备决策功能
- 已将at.js更新到2.5


## 2021 年 3 月 25 日

### Adobe Target v2 扩展 0.13.7

- 修复了 mbox 请求中包含的 `targetPageParams` 存在的问题。`targetPageParams` 只应包含在请 `pageLoad` 求中。
- 修复了标记扩展中的文档和窗口全局对象的问题，方法是将全局对象依赖项替换为对它们的直接引用。
- 已将at.js更新到2.4.1。

## 2021 年 1 月 25 日

### Adobe Target v2 扩展 0.13.6

- 添加了对统一配置文件/平台 ID 交付 API customerId 的支持
- 修复了无效样式标记注入的问题
- 已将at.s更新至2.4.0
- 解决了未定义参数可能导致投放请求错误的问题

## 2020 年 11 月 25 日

### Adobe Target v2 扩展 0.13.4

- 修复了 mbox 参数不显示在 UI 中的错误
- 品牌更新
- 已将 at.js 版本更新到 2.3.3

## 2020 年 7 月 24 日

### Adobe Target v2 扩展 0.13.3

- 修复了导致 QA 模式链接对闲置活动无效的错误
- 修复了脚本或代码将 `default` 属性添加到 `window` 或 `document` 时扩展失败的错误

## 2020 年 6 月 15 日

### Adobe Target v2 扩展 0.13.2

- 修复了以下问题：使用 CNAME 和 Edge 覆盖时，at.js 1.x 可能会错误地创建服务器域，从而导致 Target 请求失败
- 修复了以下问题：当使用适用于Target的v2标记扩展和Adobe Analytics标记扩展时，Target会延迟Analytics sendBeacon调用
- 改进了 `deviceIdLifetime` 设置，使其可通过 `targetGlobalSettings` 覆盖

## 2020 年 3 月 25 日

### Adobe Target v2 扩展 0.13.0

- 已将 at.js 更新至 v2.3。
- 在 adobe.target.getOffer API 中添加了 Target 全局 Mbox 支持
- 修复了参数和页面加载参数无法正确处理的问题

## 2019 年 10 月 10 日

### Adobe Target v2 扩展 0.12.0

- 已将 at.js 更新至 v2.2。
- 改进了 Experience Cloud ID 库 (ECID) v4.4 和 at.js 2.2 之间集成的性能。
- 以前，ECID 库要发出两次阻止调用，at.js 才能获取体验。现已减少为一次调用，显著提高了性能。

>[!NOTE]
>请将您的ECID标记扩展升级到v4.4.1以利用此性能增强功能。

## 2019 年 7 月 31 日

### Adobe Target v2 扩展 0.11.1

- 更新了扩展版本以使用 at.js 2.1.1
- 添加了处理参数的修复

## 2019 年 6 月 3 日

### Adobe Target v2 扩展 0.11.0

- 新的标记扩展可支持at.js 2.1
