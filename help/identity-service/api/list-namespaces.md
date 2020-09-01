---
keywords: Experience Platform;home;popular topics;namespace list;list namespace
solution: Experience Platform
title: 列表可用命名空间
topic: API guide
description: 列表所有可用命名空间。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 5%

---


# 列表可用命名空间

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

响应包括对象的数组，每个对象表示可用命名空间。 值为“[!UICONTROL false]”的命名空间是标准[!UICONTROL 命名空间，而值为“]true[!UICONTROL ”的是]您的组织创建的命名空间。

>[!NOTE]
>
>此响应已被截断为空间。

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

继续到下一个教程以 [创建自定义命名空间](./create-custom-namespace.md)