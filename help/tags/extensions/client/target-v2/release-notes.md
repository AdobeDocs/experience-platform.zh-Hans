---
title: Adobe Target v2扩展的发行说明
description: Adobe Experience Platform中的Adobe Target v2标记扩展的最新发行说明。
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 15%

---

# Adobe Target v2扩展发行说明

## v0.20.3（2024年1月23日）

- 更新以支持`at.js` 2.11.4
- 修复了阻止将无效地理数据发送到交付API的错误。

## v0.20.2（2023年11月29日）

- 更新以支持`at.js` 2.11.3
- 修复了导致无法在at-content-rendering-failed事件上发送响应令牌的错误。

## v0.20.1（2023年11月3日）

- 更新以支持`at.js` 2.11.2。
- 修复了在自定义事件上发送的响应令牌中导致不一致的问题。

## v0.20.0（2023年10月9日）

- 更新以支持`at.js` 2.11.0。
- 添加了对在targetGlobalSettings中设置自定义Adobe Experience Platform sandboxId和sandboxName的支持，这些设置将传递到getOffer/getOffers调用上的交付API。
- 选择器中链接:eq()的影子DOM修复。

## v0.19.3（2023年9月18日）

- 更新以支持`at.js` v2.10.3。
- 修复了在未呈现选件时错误地触发at-content-rendering-succeeded自定义事件的问题。 现在会触发正确的事件at-content-rendering-no-offers 。
- 为at-content-rendering-failed自定义事件的错误对象添加了eventToken和responseTokens。

## v0.19.2（2023年2月14日）

- 修复了允许将超时设置为数据元素的问题。

## v0.19.1（2023年2月3日）

- 更新以支持`at.js` v2.10.1
- 客户端自定义Mbox参数现在正确支持点表示法
- VEC中不再进行投放调用

## v0.19.0（2022年9月19日）

- 更新以支持`at.js` v2.10.0
- 添加了跨域跟踪支持。

## v0.18.0（2022年6月1日）

- 更新以支持`at.js` v2.9.0
- 添加了用户代理客户端提示支持。

## v0.17.1（2022年1月28日）

- 更新以支持`at.js` v2.8.1
- 修复了`pageLoad`在ODD混合执行模式下未映射到`target-global-mbox`的问题
- 修复了`mbox`请求的分析详细信息问题
- 升级了开发依赖关系以修复安全漏洞

## v0.17.0（2022年1月7日）

- 更新以支持`at.js` v2.8.0，它现在正在收集功能使用情况和性能遥测数据。  不收集个人数据。要选择退出此功能，请在`telemetryEnabled`中将`false`设置为`targetGlobalSettings`。

## v0.16.0（2021年10月28日）

- 更新了以支持`at.js` v2.7.0，现在可从Adobe Target下载。

## v0.15.2（2021年8月16日）

- 更新以支持`at.js` 2.6.1。
- 独立于页面加载事件在启动时初始化设备上决策。
- 现在，可在下载工件后的首次访问中使用设备上决策。

## v0.15.1（2021年7月20日）

- 修复了`stringify`函数名称冲突的问题，该问题会导致为`sessionId`、`requestId`等生成的UUID值不正确。

## v0.15.0（2021年7月16日）

- 当`at.js`设置secureOnly设置为true时，向Cookie添加安全属性
- 现在可以在使用`triggerView()`时使用响应令牌
- 修复了与`CONTENT_RENDERING_NO_OFFERS`事件相关的错误。 现在，每当没有从Target返回内容时，就会正确触发该事件
- 使用预回迁请求时，正确返回了A4T点击量度详细信息
- UUID生成不再使用`Math.random()`，而是依赖于`window.crypto`
- 在每次网络调用时都正确延长`sessionId` Cookie到期日
- SPA视图缓存初始化现在可以被正确处理，并且它遵循`viewsEnable`设置

## v0.14.2（2021年6月2日）

- 修复了最终捆绑包包含两个`at.js`版本的错误，一个版本带有“设备端决策”功能，另一个版本没有。

## v0.14.1（2021年5月19日）

- v0.14版本中引入的修复回归，其中Load Target操作会触发全局mbox调用

## v0.14（2021年5月14日）

- 添加了一个具有[设备上决策](./overview.md#load-target-with-on-device-decisioning)的新操作Load Target，该操作通过设备上决策功能加载`at.js` 2.5
- 已将`at.js`更新至2.5


## v0.13.7（2021年3月25日）

- 修复了 mbox 请求中包含的 `targetPageParams` 存在的问题。`targetPageParams`应仅包含在`pageLoad`请求中。
- 修复了标记扩展中文档和窗口全局对象的问题，方法是将全局对象依赖项替换为对它们的直接引用。
- 已将`at.js`更新至2.4.1。

## v0.13.6（2021年1月25日）

- 添加了对统一轮廓/平台 ID 交付 API customerId 的支持
- 修复了无效样式标记注入的问题
- 已将at.s更新至2.4.0
- 解决了未定义参数可能导致投放请求错误的问题

## v0.13.4（2020年11月25日）

- 修复了 mbox 参数不显示在 UI 中的错误
- 品牌更新
- 已将`at.js`版本更新为2.3.3

## v0.13.3（2020年7月24日）

- 修复了导致 QA 模式链接对闲置活动无效的错误
- 修复了脚本或代码将 `default` 属性添加到 `window` 或 `document` 时扩展失败的错误

## v0.13.2（2020年6月15日）

- 修复了在使用CNAME和边缘覆盖时，`at.js` 1.x可能无法正确地创建服务器域，从而导致Target请求失败的问题
- 修复了以下问题：使用Target v2标记扩展和Adobe Analytics标记扩展时，Target会延迟Analytics sendBeacon调用
- 改进了 `deviceIdLifetime` 设置，使其可通过 `targetGlobalSettings` 覆盖

## v0.13.0（2020年3月25日）

- 已将`at.js`更新至v2.3。
- 在 adobe.target.getOffer API 中添加了 Target 全局 Mbox 支持
- 修复了参数和页面加载参数无法正确处理的问题

## v0.12.0（2019年10月10日）

- 已将`at.js`更新至v2.2。
- 改进了Experience Cloud ID库(ECID) v4.4和`at.js` 2.2之间集成的性能。
- 以前，在`at.js`获取体验之前，ECID库会进行两次阻止调用。 现已减少为一次调用，显著提高了性能。

>[!NOTE]
>请将您的ECID标记扩展升级到v4.4.1以实现此性能提升。

## v0.11.1（2019年7月31日）

- 更新了扩展版本以使用`at.js` 2.1.1
- 添加了处理参数的修复

## v0.11.0（2019年6月3日）

- 支持`at.js` 2.1的新标记扩展
