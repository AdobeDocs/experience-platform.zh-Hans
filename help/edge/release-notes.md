---
title: Adobe Experience Platform Web SDK 发行说明
description: Adobe Experience Platform Web SDK的最新发行说明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK；发行说明；
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 5%

---


# 发行说明

## 版本 2.3.0

* 增加了一次性支持，以允许更严格的内容安全策略。
* 增加了对单页应用程序的个性化支持。
* 改进了与可能覆盖`window.console` API的其他页面JavaScript代码的兼容性。
* 错误修复：将`documentUnloading`设置为`true`或自动跟踪链接点击时，未使用`sendBeacon`。
* 错误修复：如果锚点元素包含HTML内容，则不会自动跟踪链接。
* 错误修复：某些包含只读`message`属性的浏览器错误未得到适当处理，导致向客户公开了其他错误。
* 错误修复：如果iframe的HTML页来自父窗口的HTML页以外的子域，则在iframe中运行SDK将导致错误。

## 版本 2.2.0

* 错误修复：当`idMigrationEnabled`为`true`时，Opt-in对象阻止Alloy发出调用。
* 错误修复：让Alloy了解应返回个性化优惠以防止出现闪烁问题的请求。

## 版本 2.1.0

* 删除`syncIdentity`命令并支持在`sendEvent`命令中传递这些ID。
* 支持IAB 2.0同意标准。
* 支持在`setConsent`命令中传递其他ID。
* 支持覆盖`sendEvent`命令中的`datasetId`。
* 支持合金监视器（[阅读更多](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)）
* 在实现详细信息上下文数据中传递`environment: browser`。
