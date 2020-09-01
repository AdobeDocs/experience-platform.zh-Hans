---
keywords: Experience Platform;home;popular topics;identity xid;XID
solution: Experience Platform
title: 获取标识的本机ID
topic: API guide
description: 标识命名空间通常作为ID字符串值和在所摄取的XDM数据中的标识提供，并且当提供用于API调用的标识时。 当身份在Identity Service中保留时，将生成一个ID并将其分配给该身份，称为本机XID。 需要身份数据支持的平台API使用这个更紧凑的表单来表示聚合的ID和命名空间。 XID是一个base64编码的字符串。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# 获取身份的XID

标识命名空间通常作为ID字符串值和在所摄取的XDM数据中的标识提供，并且当提供用于API调用的标识时。 当身份被保留在 [!DNL Identity Service]中时，将生成一个ID并将其分配给该标识，称为本机XID。 [!DNL Platform] 需要标识数据支持的API，使用这种更紧凑的表单来表示聚合的ID和命名空间。 XID是一个base64编码的字符串。

>[!NOTE]
>
>此格式主要供内部Adobe使用。 本机XID作为奇异值，空间效率更高，它是内部在解决方案中用 [!DNL Platform] 于存储和序列化的内容。 但是，它不是人类可读的，是不透明的，并且需要单独的调用才能使用它。

使用本节所述的服务获取给定ID值和命名空间的XID。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**请求**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
