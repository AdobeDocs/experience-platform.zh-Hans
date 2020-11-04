---
title: Adobe Experience PlatformWeb SDK发行说明
seo-title: Adobe Experience PlatformWeb SDK发行说明
description: Adobe Experience Platform Web SDK 发行说明。
seo-description: Adobe Experience Platform Web SDK 发行说明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 8%

---


# 发行说明

## 版本 2.3.0

* 增加了一次支持，以允许更严格的内容安全策略。
* 增加了对单页应用程序的个性化支持。
* 改进了与可能覆盖API的其他页面JavaScript代码的兼 `window.console` 容性。
* 错误修复： `sendBeacon` 设置为或自动 `documentUnloading` 跟踪链 `true` 接单击时不使用。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：某些包含只读属性的浏览器错 `message` 误未得到适当处理，导致向客户暴露了不同的错误。
* 错误修复：如果iframe的HTML页面来自父窗口的HTML页面以外的子域，则在iframe中运行SDK将导致错误。

## 版本 2.2.0

* 错误修复：Opt-in对象阻止Alloy在调用时进 `idMigrationEnabled` 行调 `true`用。
* 错误修复：让合金了解应返回个性化优惠以防出现闪烁问题的请求。

## 版本 2.1.0

* 删除命 `syncIdentity` 令并支持在命令中传递这些 `sendEvent` ID。
* 支持IAB 2.0同意标准。
* 支持在命令中传递其 `setConsent` 他ID。
* 支持覆盖 `datasetId` 命令 `sendEvent` 中的。
* 支持合金显示器([阅读更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 在实 `environment: browser` 施详细信息上下文数据中传递。
