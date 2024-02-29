---
keywords: Experience Platform；主页；热门主题；身份xid；XID
solution: Experience Platform
title: 获取标识的本机ID
description: 在摄取的XDM数据中，以及在提供身份用于API调用时，身份数据通常作为ID字符串值和身份命名空间提供。 当标识保留在Identity Service中时，将生成一个ID并将其分配给该标识，称为本机XID。 需要身份数据支持的平台API将使用此更紧凑的表单来表示聚合ID和命名空间。 XID是base64编码字符串。
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 获取标识的本机ID

在摄取的XDM数据中，以及在提供身份用于API调用时，身份数据通常作为ID字符串值和身份命名空间提供。 当身份保留在 [!DNL Identity Service]，则会生成一个ID并将其分配给该标识，称为本机XID。 [!DNL Platform] 需要身份数据支持的API使用此更紧凑的表单来表示聚合ID和命名空间。 XID是base64编码字符串。

>[!NOTE]
>
>此格式主要供内部Adobe使用。 原生XID作为单一值可节省空间，并且可在内部使用 [!DNL Platform] 存储和序列化解决方案。 然而，它不是人类可读的，也是不透明的，需要单独的调用才能获得使用。

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
