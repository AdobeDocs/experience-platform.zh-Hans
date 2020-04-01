---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 删除资源
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0

---


# 删除资源

有时可能需要从模式注册表中删除（删除）资源。 只能删除您在租户容器中创建的资源。 这是通过使用要删除的资 `$id` 源执行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_TYPE}` | 要从模式库中删除的资源类型。 有效类 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{RESOURCE_ID}` | 资源的URL编 `$id` 码的URI `meta:altId` 或URI。 |

**请求**

DELETE请求不需要接受标题。

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态204（无内容）和空白正文。

您可以通过尝试对资源进行查找(GET)请求来确认删除。 您需要在请求中包含一个“接受”标头，但应接收HTTP状态404（“找不到”），因为该资源已从模式注册表中删除。