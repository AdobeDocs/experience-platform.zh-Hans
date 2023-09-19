---
title: Adobe Target v2扩展的发行说明
description: Adobe Experience Platform中的Adobe Target v2标记扩展的最新发行说明。
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: 4b87141e94681d9a9f51d4d9b2f2276ca065d6ce
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 22%

---

# Adobe Target v2扩展发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## v0.19.3（2023年9月18日）

- 更新了以支持at.js v2.10.3。
- 修复了在未呈现选件时错误地触发at-content-rendering-succeeded自定义事件的问题。 现在会触发正确的事件at-content-rendering-no-offers 。
- 为at-content-rendering-failed自定义事件的错误对象添加了eventToken和responseTokens。

## v0.19.2（2023年2月14日）

- 修复了允许将超时设置为数据元素的问题。

## v0.19.1（2023年2月3日）

- 更新以支持 `at.js` v2.10.1
- 客户端自定义Mbox参数现在正确支持点表示法
- VEC中不再进行投放调用

## v0.19.0（2022年9月19日）

- 更新以支持 `at.js` v2.10.0
- 添加了跨域跟踪支持。

## v0.18.0（2022年6月1日）

- 更新以支持 `at.js` v2.9.0
- 添加了对用户代理客户端提示的支持。

## v0.17.1（2022年1月28日）

- 更新以支持 `at.js` v2.8.1
- 固定 `pageLoad` 未映射到 `target-global-mbox` 在ODD混合执行模式下
- 修复了“ ”的分析详细信息问题 `mbox` 请求
- 升级了开发依赖关系以修复安全漏洞

## v0.17.0（2022年1月7日）

- 更新以支持 `at.js` v2.8.0，它现在正在收集功能使用情况和性能遥测数据。  不收集个人数据。要选择退出此功能，请设置 `telemetryEnabled` 到 `false` 在 `targetGlobalSettings`.

## v0.16.0（2021年10月28日）

- 更新以支持 `at.js` v2.7.0，现在可从Adobe Target下载。

## v0.15.1（2021年7月20日）

- 修复了的问题 `stringify` 函数名称冲突，这会导致为生成的错误UUID值 `sessionId`， `requestId`，等等。

## v0.15.0（2021年7月16日）

- 每当发生以下情况时，向Cookie添加安全属性 `at.js` 设置secureOnly设置为true
- 现在可以在使用时使用响应令牌 `triggerView()`
- 修复了一个与相关的错误 `CONTENT_RENDERING_NO_OFFERS` 事件。 现在，每当没有从Target返回内容时，就会正确触发该事件
- 使用预回迁请求时，正确返回了A4T点击量度详细信息
- UUID生成功能不再使用 `Math.random()`，但依赖于 `window.crypto`
- `sessionId` 在每次网络调用时都会正确延长Cookie到期日
- SPA视图缓存初始化现在可以被正确处理并遵守 `viewsEnable` 设置

## v0.14.2（2021年6月2日）

- 修复了最终捆绑包中包含两个捆绑包的错误 `at.js` 版本，一个包含“设备上决策”，另一个不包含。

## v0.14.1（2021年5月19日）

- v0.14版本中引入的修复回归，其中Load Target操作会触发全局mbox调用

## v0.14（2021年5月14日）

- 添加了新操作Load Target，用于 [设备上决策](./overview.md#load-target-with-on-device-decisioning)，加载 `at.js` 2.5具有设备上决策功能
- 已更新 `at.js` 到2.5


## v0.13.7（2021年3月25日）

- 修复了 mbox 请求中包含的 `targetPageParams` 存在的问题。`targetPageParams` 只能包含在 `pageLoad` 请求。
- 修复了标记扩展中文档和窗口全局对象的问题，方法是将全局对象依赖项替换为对它们的直接引用。
- 已更新 `at.js` 到2.4.1。

## v0.13.6（2021年1月25日）

- 添加了对统一配置文件/平台 ID 交付 API customerId 的支持
- 修复了无效样式标记注入的问题
- 已将at.s更新至2.4.0
- 解决了未定义参数可能导致投放请求错误的问题

## v0.13.4（2020年11月25日）

- 修复了 mbox 参数不显示在 UI 中的错误
- 品牌更新
- 已更新 `at.js` 版本到2.3.3

## v0.13.3（2020年7月24日）

- 修复了导致 QA 模式链接对闲置活动无效的错误
- 修复了脚本或代码将 `default` 属性添加到 `window` 或 `document` 时扩展失败的错误

## v0.13.2（2020年6月15日）

- 修复了使用CNAME和边缘覆盖时的问题，其中 `at.js` 1.x可能无法正确地创建服务器域，从而导致Target请求失败
- 修复了以下问题：使用Target v2标记扩展和Adobe Analytics标记扩展时，Target会延迟Analytics sendBeacon调用
- 改进了 `deviceIdLifetime` 设置，使其可通过 `targetGlobalSettings` 覆盖

## v0.13.0（2020年3月25日）

- 已更新 `at.js` 到v2.3。
- 在 adobe.target.getOffer API 中添加了 Target 全局 Mbox 支持
- 修复了参数和页面加载参数无法正确处理的问题

## v0.12.0（2019 年 10 月 10 日）

- 已更新 `at.js` 到v2.2。
- 改进了Experience CloudID库(ECID) v4.4与之间集成的性能 `at.js` 2.2.
- 以前，ECID库会进行两次阻止调用，而现在 `at.js` 无法获取体验。 现已减少为一次调用，显著提高了性能。

>[!NOTE]
>请将您的ECID标记扩展升级到v4.4.1以实现此性能提升。

## v0.11.1（2019年7月31日）

- 更新了要使用的扩展版本 `at.js` 2.1.1
- 添加了处理参数的修复

## v0.11.0（2019年6月3日）

- 要支持的新标记扩展 `at.js` 2.1
