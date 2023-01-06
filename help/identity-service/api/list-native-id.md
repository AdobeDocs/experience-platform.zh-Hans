---
keywords: Experience Platform；主页；热门主题；身份xid;XID
solution: Experience Platform
title: 获取标识的本机ID
description: 在摄取的XDM数据中，以及在提供标识以供在API调用中使用时，身份数据通常作为ID字符串值和身份命名空间提供。 当标识保留在Identity服务中时，将生成一个ID并将其分配给该标识，称为本机XID。 需要身份数据支持的平台API使用这个更紧凑的表单来获取聚合ID和命名空间。 XID是一个base64编码字符串。
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 获取标识的本机ID

在摄取的XDM数据中，以及在提供标识以供在API调用中使用时，身份数据通常作为ID字符串值和身份命名空间提供。 在中保留身份时 [!DNL Identity Service]，则会生成一个ID并将其分配给该标识，称为本机XID。 [!DNL Platform] 需要身份数据支持的API使用这个更紧凑的形式表示聚合的ID和命名空间。 XID是一个base64编码字符串。

>[!NOTE]
>
>此格式主要供内部Adobe使用。 本机XID作为奇异值更有空间效率，是内部使用的 [!DNL Platform] 存储和序列化解决方案。 但是，该函数不可读，且不透明，需要单独调用才能使用。

使用本节中描述的服务获取给定ID值和命名空间的XID。

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
