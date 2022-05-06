---
keywords: Experience Platform；主页；热门主题；列出沙箱
solution: Experience Platform
title: 沙盒类型API端点
topic-legacy: developer guide
description: 通过向/sandboxTypes端点发出GET请求，可以检索组织支持的沙盒类型列表。
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 2%

---

# 沙盒类型端点

通过向 `/sandboxTypes` 端点。

## 快速入门

本指南中使用的API端点是 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 检索支持的沙盒类型列表

通过向 `/sandboxTypes` 端点。

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

成功的响应会返回您的组织支持的沙盒类型列表。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
