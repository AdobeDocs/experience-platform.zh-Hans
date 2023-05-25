---
keywords: Experience Platform；主页；热门主题；命名空间列表；列表命名空间
solution: Experience Platform
title: 列出可用的身份命名空间
description: 列出所有可用的命名空间。
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---

# 列出可用的身份命名空间

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

响应包括对象数组，每个对象表示可用的命名空间。 带有“”的命名空间[!UICONTROL 自定义]“ ”的值[!UICONTROL false]&quot;是标准命名空间，而具有&quot;[!UICONTROL 自定义]“ ”的值[!UICONTROL true]“”是您的组织创建的命名空间。

>[!NOTE]
>
>此响应已因空间而被截断。

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

继续下一教程，了解 [创建自定义命名空间](./create-custom-namespace.md)
