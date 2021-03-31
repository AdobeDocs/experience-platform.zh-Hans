---
keywords: Experience Platform；主页；热门主题；列表沙箱
solution: Experience Platform
title: 列表API中支持的沙箱类型
topic: 开发人员指南
description: 通过向/sandboxTypes端点发出列表请求，可以检索组织的受支持沙箱类型GET。
translation-type: tm+mt
source-git-commit: ca3de18c093d7b692b582045afea4401d7133b9b
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 2%

---


# 列表API中支持的沙箱类型

您可以通过向`/sandboxTypes`端点发出GET请求，为组织检索支持的沙箱类型列表。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**响应**

成功的响应会返回一列表您的组织支持的沙箱类型。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
