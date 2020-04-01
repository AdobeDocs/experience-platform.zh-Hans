---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列表支持的沙箱类型
topic: developer guide
translation-type: tm+mt
source-git-commit: b4741cdfd065bbaed7f2feeafe8619191e4b8f6c

---


# 列表支持的沙箱类型

您可以通过向端点发出GET请求，为组织检索一列表受支持的沙箱类 `/sandboxTypes` 型。

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
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回组织支持的列表沙箱类型。

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
