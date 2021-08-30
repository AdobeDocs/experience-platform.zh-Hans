---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；审核；审核日志；更改日志；RPC;
solution: Experience Platform
title: 审核日志API端点
description: 通过架构注册表API中的/auditlog端点，可以按时间顺序检索对现有XDM资源所做更改的列表。
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 3%

---

# 审核日志端点

对于每个体验数据模型(XDM)资源， [!DNL Schema Registry]会维护一个日志，其中包含不同更新之间发生的所有更改。 [!DNL Schema Registry] API中的`/auditlog`端点允许您检索由ID指定的任何类、架构字段组、数据类型或架构的审核日志。

## 快速入门

本指南中使用的端点是[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的一部分。 在继续操作之前，请查阅[快速入门指南](./getting-started.md) ，以获取相关文档的链接、本文档中API调用示例的阅读指南，以及成功调用任何Experience PlatformAPI所需的标头的重要信息。

`/auditlog`端点是[!DNL Schema Registry]支持的远程过程调用(RPC)的一部分。 与[!DNL Schema Registry] API中的其他端点不同，RPC端点不需要诸如`Accept`或`Content-Type`之类的额外标头，也不使用`CONTAINER_ID`。 相反，它们必须使用`/rpc`命名空间，如以下API调用中所示。

## 检索资源的审核日志

您可以通过在`/auditlog`端点的GET请求路径中指定资源的ID，来检索架构库中任何类、字段组、数据类型或架构的审核日志。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 要检索其审核日志的资源的`meta:altId`或URL编码的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求将检索`Restaurant`字段组的审核日志。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回对资源所做更改（从最近到最近）的时间顺序列表。

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
| `auditTrails` | 对象数组，每个对象表示对指定资源或其从属资源之一所做的更改。 |
| `id` | 已更改的资源的`$id`。 此值通常表示在请求路径中指定的资源，但如果是更改的来源，则可能表示从属资源。 |
| `action` | 所做更改的类型。 |
| `path` | [JSON Pointer](../../landing/api-fundamentals.md#json-pointer)字符串，用于指示已更改或添加的特定字段的路径。 |
| `value` | 分配给新字段或更新字段的值。 |

{style=&quot;table-layout:auto&quot;}
