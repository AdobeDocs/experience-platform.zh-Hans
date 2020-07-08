---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建自定义命名空间
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 5%

---


# 创建自定义命名空间

使用 [!DNL Identity Namespace] API，您可以创建仅对您的组织可用的自定义标识命名空间。

有关创建自定义命名空间的建议，请 [参阅Identity Service常见问题解答文档](../troubleshooting-guide.md)。

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

继续到下一个教程 [以列表标识的本机ID](./list-native-id.md)