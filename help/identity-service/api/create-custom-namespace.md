---
keywords: Experience Platform；主页；热门主题；命名空间;命名空间;命名空间;命名空间；标识命名空间；标识命名空间；标识；标识；标识
solution: Experience Platform
title: 在Identity Service API中创建自定义命名空间
topic-legacy: API guide
description: 使用Identity 命名空间 API，您可以创建仅对您的组织可用的自定义标识命名空间。
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# 在Identity Service API中创建自定义命名空间

使用[!DNL Identity Namespace] API，您可以创建仅对您的组织可用的自定义标识命名空间。

有关创建自定义命名空间的建议，请参阅[Identity Service常见问题解答文档](../troubleshooting-guide.md)。

>[!NOTE]
>
>命名空间是身份的限定符。 因此，一旦创建了命名空间，便无法删除它。

**API格式**

```http
POST /idnamespace/identities
```

**请求**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**响应**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## 后续步骤

继续下一个教程，使用[列表标识的本机ID](./list-native-id.md)
