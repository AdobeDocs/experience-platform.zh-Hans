---
keywords: Experience Platform；首頁；熱門主題；名稱空間清單；清單名稱空間
solution: Experience Platform
title: 列出可用的身分名稱空間
description: 列出所有可用的名稱空間。
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---

# 列出可用的身分名稱空間

**API格式**

```http
GET /idnamespace/identities
```

**请求**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應包含物件陣列，每個物件代表可用的名稱空間。 具有「」的名稱空間[!UICONTROL 自訂]「 」的值[!UICONTROL false]&quot;是標準名稱空間，而具有&quot;[!UICONTROL 自訂]「 」的值[!UICONTROL true]&quot;是您的組織建立的名稱空間。

>[!NOTE]
>
>此回應已因空格而截斷。

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## 后续步骤

繼續下一教學課程，前往 [建立自訂名稱空間](./create-custom-namespace.md)
