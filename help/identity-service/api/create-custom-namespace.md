---
keywords: Experience Platform；主页；热门主题；命名空间；命名空间；命名空间；身份命名空间；身份命名空间；身份；身份
solution: Experience Platform
title: 在Identity服务API中创建自定义命名空间
topic-legacy: API guide
description: 使用身份命名空间API，您可以创建仅适用于贵组织的自定义身份命名空间。
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# 在Identity服务API中创建自定义命名空间

使用 [!DNL Identity Namespace] API中，您可以创建仅供贵组织使用的自定义身份命名空间。

有关创建自定义命名空间的建议，请参阅 [Identity Service常见问题解答文档](../troubleshooting-guide.md).

>[!NOTE]
>
>命名空间是身份的限定符。 因此，创建命名空间后，将无法删除该命名空间。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

继续下一个教程以 [列出标识的本机ID](./list-native-id.md)
