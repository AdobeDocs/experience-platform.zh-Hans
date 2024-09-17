---
title: Adobe Experience Platform 云连接器扩展发行说明
description: Adobe Experience Platform 中 Cloud Connector 扩展的最新发行说明。
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '128'
ht-degree: 100%

---

# Adobe Experience Platform 云连接器扩展发行说明

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

## 2023 年 1 月 17 日

v1.0.1

* 修复在 Body Raw 文本区域中粘贴的有效 JSON 被保存为字符串而不是 JSON 的问题。
* 不允许在 GET 或 HEAD 请求上设置 Body。
* 修复保存大于 5kb 的响应会导致规则执行失败的错误。
