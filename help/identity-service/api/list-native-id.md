---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 获取标识的本机ID
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# 获取XID以获取身份

标识数据通常作为ID字符串值和在摄取的XDM数据中的标识命名空间提供，并且当提供标识以用于API调用时。 当身份在Identity Service中保留时，将生成一个ID并将其分配给该标识，称为本机XID。 需要标识数据支持的平台API使用这个更紧凑的表单来表示聚集的ID和命名空间。 XID是一个base64编码的字符串。

>[!NOTE] 此格式主要供内部Adobe使用。 本机XID作为单值更加有空间效率，是平台解决方案内部用于存储和序列化的内容。 但是，它不是人类可读的，它是不透明的，并且需要单独的调用才能使用它。

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
