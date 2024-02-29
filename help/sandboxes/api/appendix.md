---
keywords: Experience Platform；主页；热门主题；API；API；沙盒；沙盒；沙盒
solution: Experience Platform
title: 沙盒API指南附录
description: 本文档提供有关使用沙盒API的补充信息。
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---

# 沙盒API指南附录

本文档提供有关使用 [!DNL Sandbox] API。

## 使用查询参数 {#query}

此 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) 在列出沙盒时，支持使用查询参数来页面和筛选结果。

>[!NOTE]
>
>此 `limit` 和 `offset` 查询参数必须一起指定。 如果您只指定一个，则API将返回错误。 如果指定“无”，则缺省限制为50，偏移为0。

| 参数 | 描述 |
| --- | --- |
| `limit` | 响应中返回的最大记录数。 |
| `offset` | 从第一个记录开始（偏移）响应列表的实体数。 |
