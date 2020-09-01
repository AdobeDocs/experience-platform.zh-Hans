---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;delete
solution: Experience Platform
title: 删除资源
describe: It may occasionally be necessary to remove resource from the Schema Registry. Only resources that you create in the tenant container may be deleted. This is done by performing a DELETE request using the $id of the resource you wish to delete.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# 删除资源

有时可能需要从中删除(DELETE)资源 [!DNL Schema Registry]。 只能删除您在租户容器中创建的资源。 这是通过使用要删除的资 `$id` 源执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_TYPE}` | 要从中删除的资源类型 [!DNL Schema Library]。 有效类 `datatypes`型 `mixins`有、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的 `meta:altId` URI或URI。 |

**请求**

DELETE请求不需要接受标头。

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对资源进行查找(GET)请求来确认删除。 您需要在请求中包含一个“接受”头，但应收到HTTP状态404（未找到），因为该资源已从中删除 [!DNL Schema Registry]。