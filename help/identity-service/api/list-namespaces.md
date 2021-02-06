---
keywords: Experience Platform；主页；热门主题；命名空间列表;列表命名空间
solution: Experience Platform
title: 列表可用身份命名空间
topic: API guide
description: 列表所有可用命名空间。
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---


# 列表可用身份命名空间

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

响应包括对象的数组，每个对象表示可用命名空间。 “[!UICONTROL custom]”值为“[!UICONTROL false]”的命名空间是标准命名空间，而“[!UICONTROL custom]”值为“[!UICONTROL true]”的命名空间是您的组织创建的。

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

进入下一个教程，[创建自定义命名空间](./create-custom-namespace.md)