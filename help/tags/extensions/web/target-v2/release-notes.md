---
title: Adobe Target v2扩展的发行说明
description: Adobe Experience Platform中Adobe Target v2标记扩展的最新发行说明。
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 824fea41bc7e7082814648efd58184f5208e5e6f
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 36%

---

# Adobe Target v2扩展发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## 2022 年 1 月 28 日

### Adobe Target v2 扩展 0.17.1

- 更新以支持 `at.js` v2.8.1
- 已修复 `pageLoad` 未映射到 `target-global-mbox` 在ODD混合执行模式下
- 修复了 `mbox` 请求
- 升级了开发依赖项以修复安全漏洞

## 2022 年 1 月 7 日

### Adobe Target v2 扩展 0.17.0

- 更新以支持 `at.js` v2.8.0，现在正在收集功能使用情况和性能遥测数据。  不收集个人数据。要选择退出此功能，请设置 `telemetryEnabled` to `false` in `targetGlobalSettings`.

## 2021 年 10 月 28 日

### Adobe Target v2 扩展 0.16.0

- 更新以支持 `at.js` v2.7.0，现在可从Adobe Target下载。

## 2021 年 7 月 20 日

### Adobe Target v2 扩展 0.15.1

- 修复了 `stringify` 函数名称冲突，这会导致为 `sessionId`, `requestId`，等等。

## 2021 年 7 月 16 日

### Adobe Target v2 扩展 0.15.0

- 向Cookie添加安全属性，只要 `at.js` settings secureOnly设置为true
- 现在，使用 `triggerView()`
- 修复了与 `CONTENT_RENDERING_NO_OFFERS` 事件。 现在，当没有从Target返回内容时，可以正确触发该事件
- 使用预取请求时，可正确返回A4T点击量度详细信息
- UUID生成不再使用 `Math.random()`，但依赖于 `window.crypto`
- `sessionId` 每次网络调用时，Cookie到期正确延长
- SPA视图缓存初始化现已得到正确处理，并遵循 `viewsEnable` 设置

## 2021 年 6 月 2 日

### Adobe Target v2 扩展 0.14.2

- 修复最终包中包含两个 `at.js` 版本中，一个具有On-Device Decisioning，一个不具有。

## 2021 年 5 月 19 日

### Adobe Target v2 扩展 0.14.1

- 修复了v0.14版本中引入的回归问题，在该版本中，Load Target操作会触发全局mbox调用

## 2021 年 5 月 14 日

### Adobe Target v2 扩展 0.14

- 添加了新操作Load Target（加载目标） [设备内决策](./overview.md#load-target-with-on-device-decisioning)，加载 `at.js` 2.5，具有设备内决策功能
- 已更新 `at.js` 到2.5


## 2021 年 3 月 25 日

### Adobe Target v2 扩展 0.13.7

- 修复了 mbox 请求中包含的 `targetPageParams` 存在的问题。`targetPageParams` 只应包含在 `pageLoad` 请求。
- 修复了标记扩展中的文档和窗口全局对象的问题，方法是将全局对象依赖项替换为对它们的直接引用。
- 已更新 `at.js` 到2.4.1。

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
- 更新了 `at.js` 版本到2.3.3

## 2020 年 7 月 24 日

### Adobe Target v2 扩展 0.13.3

- 修复了导致 QA 模式链接对闲置活动无效的错误
- 修复了脚本或代码将 `default` 属性添加到 `window` 或 `document` 时扩展失败的错误

## 2020 年 6 月 15 日

### Adobe Target v2 扩展 0.13.2

- 修复了使用CNAME和Edge覆盖时， `at.js` 1.x可能会错误地创建服务器域，从而导致Target请求失败
- 修复了以下问题：当使用适用于Target的v2标记扩展和Adobe Analytics标记扩展时，Target会延迟Analytics sendBeacon调用
- 改进了 `deviceIdLifetime` 设置，使其可通过 `targetGlobalSettings` 覆盖

## 2020 年 3 月 25 日

### Adobe Target v2 扩展 0.13.0

- 已更新 `at.js` 到v2.3。
- 在 adobe.target.getOffer API 中添加了 Target 全局 Mbox 支持
- 修复了参数和页面加载参数无法正确处理的问题

## 2019 年 10 月 10 日

### Adobe Target v2 扩展 0.12.0

- 已更新 `at.js` 到v2.2。
- 改进了Experience CloudID库(ECID)v4.4与 `at.js` 2.2。
- 以前，ECID库会在之前发出两次阻止调用 `at.js` 可以获取体验。 现已减少为一次调用，显著提高了性能。

>[!NOTE]
>请将您的ECID标记扩展升级到v4.4.1以利用此性能增强功能。

## 2019 年 7 月 31 日

### Adobe Target v2 扩展 0.11.1

- 更新了扩展版本以使用 `at.js` 2.1.1
- 添加了处理参数的修复

## 2019 年 6 月 3 日

### Adobe Target v2 扩展 0.11.0

- 要支持的新标记扩展 `at.js` 2.1
