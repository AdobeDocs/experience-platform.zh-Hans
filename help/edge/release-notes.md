---
title: Adobe Experience PlatformWeb SDK发行说明
seo-title: Adobe Experience PlatformWeb SDK发行说明
description: Adobe Experience Platform Web SDK 发行说明。
seo-description: Adobe Experience Platform Web SDK 发行说明。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 16%

---


# 发行说明

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
