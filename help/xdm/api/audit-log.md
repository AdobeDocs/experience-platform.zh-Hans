---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；审核；审核日志；更改日志；更改日志；rpc；
solution: Experience Platform
title: 审核日志API端点
description: 架构注册表API中的/auditlog端点允许您检索对现有XDM资源所做的更改的时间顺序列表。
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# 审核日志端点

对于每个Experience Data Model (XDM)资源， [!DNL Schema Registry] 维护在不同更新之间发生的所有更改的日志。 此 `/auditlog` 中的端点 [!DNL Schema Registry] API允许您检索ID指定的任何类、架构字段组、数据类型或架构的审核日志。

## 快速入门

本指南中使用的端点是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

此 `/auditlog` 终结点是远程过程调用(RPC)的一部分，该调用受 [!DNL Schema Registry]. 与中的其他端点不同 [!DNL Schema Registry] API、RPC端点不需要其他标头，例如 `Accept` 或 `Content-Type`，并且不要使用 `CONTAINER_ID`. 相反，他们必须使用 `/rpc` 命名空间，如下面的API调用中所示。

## 检索资源的审核日志

通过在GET请求的路径中指定资源的ID，可以检索架构库中任何类、字段组、数据类型或架构的审核日志。 `/auditlog` 端点。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 此 `meta:altId` 或URL编码 `$id` 要检索其审核日志的资源的。 |

{style="table-layout:auto"}

**请求**

以下请求检索架构的审核日志。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回按时间顺序排列的对资源所做更改的列表，从最近到最短。

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| 属性 | 描述 |
| --- | --- |
| `updates` | 一个对象数组，每个对象表示对指定资源或其依赖资源之一所做的更改。 |
| `id` | 此 `$id` 已更改的资源。 此值通常表示在请求路径中指定的资源，但如果该资源是更改的来源，则可能表示从属资源。 |
| `xdmType` | 已更改的资源的类型。 |
| `action` | 所做的更改类型。 |
| `path` | A [JSON指针](../../landing/api-fundamentals.md#json-pointer) 指示已更改或添加的特定字段的路径的字符串。 |
| `value` | 分配给新字段或更新字段的值。 |

{style="table-layout:auto"}
