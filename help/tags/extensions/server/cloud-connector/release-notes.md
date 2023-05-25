---
title: Adobe Experience Platform Cloud Connector扩展的发行说明
description: Adobe Experience Platform中的Cloud Connector扩展的最新发行说明。
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 22%

---

# Adobe Experience Platform Cloud Connector扩展发行说明

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## 2023 年 1 月 17 日

v1.0.1

* 修复了在Body Raw文本区域中粘贴的有效JSON保存为字符串而不是JSON的问题。
* 不允许在GET或HEAD请求上设置正文。
* 修复了以下错误：保存大于5 kb的响应会导致规则执行失败。
