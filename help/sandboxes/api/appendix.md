---
keywords: Experience Platform；主页；热门主题；API;API；沙盒；沙盒；沙盒
solution: Experience Platform
title: 沙盒API指南附录
description: 本文档提供了与使用沙盒API相关的补充信息。
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# 沙盒API指南附录

本文档提供了与使用 [!DNL Sandbox] API。

## 使用查询参数 {#query}

的 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) 支持在列出沙箱时使用查询参数来筛选页面和结果。

>[!NOTE]
>
>的 `limit` 和 `offset` 必须一起指定查询参数。 如果仅指定一个，则API将返回错误。 如果指定“无”，则默认限制为50，偏移为0。

| 参数 | 描述 |
| --- | --- |
| `limit` | 响应中要返回的最大记录数。 |
| `offset` | 从第一个记录开始（偏移）响应列表的实体数。 |
