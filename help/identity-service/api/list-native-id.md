---
keywords: Experience Platform；主页；热门主题；身份xid；XID
solution: Experience Platform
title: 获取标识的本机ID
description: 在摄取的XDM数据中，以及在提供身份用于API调用时，身份数据通常作为ID字符串值和身份命名空间提供。 当标识保留在Identity Service中时，将生成一个ID并将其分配给该标识，称为本机XID。 需要身份数据支持的Experience Platform API使用此更紧凑的表单来汇总ID和命名空间。 XID是base64编码字符串。
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 获取标识的本机ID

在摄取的XDM数据中，以及在提供身份用于API调用时，身份数据通常作为ID字符串值和身份命名空间提供。 当标识保留在[!DNL Identity Service]中时，将生成一个ID并将其分配给该标识，称为本机XID。 [!DNL Experience Platform]个API需要使用此更紧凑的表单来获取聚合ID和命名空间，以支持身份数据。 XID是base64编码字符串。

>[!NOTE]
>
>此格式主要供Adobe内部使用。 作为单一值的本机XID空间效率更高，并且是[!DNL Experience Platform]解决方案内部用于存储和序列化的内容。 然而，它不是人类可读的，也是不透明的，需要单独的调用才能获得使用。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
