---
keywords: Experience Platform；主页；热门主题；列表沙盒
solution: Experience Platform
title: 沙盒类型API端点
description: 您可以通过向/sandboxTypes端点发出GET请求来检索贵组织支持的沙盒类型列表。
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 2%

---

# 沙盒类型端点

您可以向以下网站发出GET请求，检索贵组织支持的沙盒类型列表 `/sandboxTypes` 端点。

## 快速入门

本指南中使用的API端点是 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索支持的沙盒类型列表

您可以向以下网站发出GET请求，检索贵组织支持的沙盒类型列表 `/sandboxTypes` 端点。

**API格式**

```http
GET /sandboxTypes
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的响应将返回您的组织支持的沙盒类型列表。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
