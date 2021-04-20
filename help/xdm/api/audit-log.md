---
keywords: Experience Platform；主页；热门主题；api;API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；审计；审计日志；更改日志；rpc;
solution: Experience Platform
title: 审核日志API端点
description: 模式 Registry API中的/auditlog端点允许您检索对现有XDM资源所做更改的按时间顺序列表。
topic: developer guide
translation-type: tm+mt
source-git-commit: 0727ffa0c72bcb6a85de1a13215b691b97889b70
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---


# 审核日志端点

对于每个体验数据模型(XDM)资源，[!DNL Schema Registry]会保留在不同更新之间发生的所有更改的日志。 [!DNL Schema Registry] API中的`/auditlog`端点允许您检索由ID指定的任何类、混音、数据类型或模式的审核日志。

## 入门指南

本指南中使用的端点是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)的一部分。 在继续之前，请查阅[快速入门指南](./getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南以及成功调用任何Experience PlatformAPI所需标头的重要信息。

`/auditlog`端点是[!DNL Schema Registry]支持的远程过程调用(RPC)的一部分。 与[!DNL Schema Registry] API中的其他端点不同，RPC端点不需要额外的标头，如`Accept`或`Content-Type`，也不使用`CONTAINER_ID`。 相反，他们必须使用`/rpc`命名空间，如以下API调用中所示。

## 检索资源的审核日志

您可以通过在到`/auditlog`端点的GET请求路径中指定资源的ID，检索模式库中任何类、混合、数据类型或模式的审核日志。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 要检索其审计日志的资源的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求将检索`Restaurant`混音的审核日志。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回对资源所做更改的时间列表，从最近到最近。

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| 属性 | 描述 |
| --- | --- |
| `auditTrails` | 对象的数组，每个对象表示对指定资源或其从属资源之一所做的更改。 |
| `id` | 已更改的资源的`$id`。 此值通常表示在请求路径中指定的资源，但如果是更改的源，则可能表示从属资源。 |
| `action` | 所做更改的类型。 |
| `path` | 一个[JSON Pointer](../../landing/api-fundamentals.md#json-pointer)字符串，指示已更改或添加的特定字段的路径。 |
| `value` | 分配给新字段或已更新字段的值。 |