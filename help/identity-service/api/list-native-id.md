---
keywords: Experience Platform；主页；热门主题；身份xid;XID
solution: Experience Platform
title: 获取标识的本机ID
topic-legacy: API guide
description: 标识数据通常作为ID字符串值和在摄取的XDM数据中的标识命名空间提供，并且当提供用于API调用的标识时提供。 当身份在Identity Service中保留时，将生成一个ID并将其分配给该身份，称为本机XID。 需要标识数据支持的平台API，使用这个更紧凑的表单进行聚合ID和命名空间。 XID是一个base64编码的字符串。
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 获取标识的本机ID

标识数据通常作为ID字符串值和在摄取的XDM数据中的标识命名空间提供，并且当提供用于API调用的标识时提供。 在[!DNL Identity Service]中保留身份时，将生成一个ID并将其分配给该身份，称为本机XID。 [!DNL Platform] 需要标识数据支持的API，使用此更紧凑的表单进行聚合ID和命名空间。XID是一个base64编码的字符串。

>[!NOTE]
>
>此格式主要用于内部Adobe。 本机XID作为单值更有空间效率，是[!DNL Platform]解决方案内部用于存储和序列化的内容。 但是，它不是人可读的，是不透明的，并且需要单独的调用才能使用。

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
