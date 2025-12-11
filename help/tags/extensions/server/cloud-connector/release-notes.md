---
title: Adobe Experience Platform 云连接器扩展发行说明
description: Adobe Experience Platform 中 Cloud Connector 扩展的最新发行说明。
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 100%

---

# Adobe Experience Platform 云连接器扩展发行说明

## 2023 年 1 月 17 日

v1.0.1

* 修复在 Body Raw 文本区域中粘贴的有效 JSON 被保存为字符串而不是 JSON 的问题。
* 不允许在 GET 或 HEAD 请求上设置 Body。
* 修复保存大于 5kb 的响应会导致规则执行失败的错误。
