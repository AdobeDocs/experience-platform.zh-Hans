---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；审核；审核日志；更改日志；RPC;
solution: Experience Platform
title: 审核日志API端点
description: 通过架构注册表API中的/auditlog端点，可以按时间顺序检索对现有XDM资源所做更改的列表。
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 3%

---

# 审核日志端点

对于每个体验数据模型(XDM)资源， [!DNL Schema Registry] 维护一个日志，其中包含在不同更新之间发生的所有更改。 的 `/auditlog` 的端点 [!DNL Schema Registry] API允许您检索由ID指定的任何类、架构字段组、数据类型或架构的审核日志。

## 快速入门

本指南中使用的端点是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

的 `/auditlog` 端点是远程过程调用(RPC)的一部分，该调用受 [!DNL Schema Registry]. 与 [!DNL Schema Registry] API、RPC端点不需要其他标头，例如 `Accept` 或 `Content-Type`、和不使用 `CONTAINER_ID`. 相反，他们必须使用 `/rpc` 命名空间，如下面API调用中所示。

## 检索资源的审核日志

您可以在架构库中检索任何类、字段组、数据类型或架构的审核日志，方法是在GET请求的路径中指定资源的ID，该ID位于 `/auditlog` 端点。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 的 `meta:altId` 或URL编码 `$id` 要检索其审核日志的资源。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会检索架构的审核日志。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回对资源所做更改（从最近到最近）的时间顺序列表。

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
| `updates` | 对象数组，每个对象表示对指定资源或其从属资源之一所做的更改。 |
| `id` | 的 `$id` 更改的资源。 此值通常表示在请求路径中指定的资源，但如果是更改的源，则可能表示从属资源。 |
| `xdmType` | 已更改的资源类型。 |
| `action` | 所做更改的类型。 |
| `path` | A [JSON指针](../../landing/api-fundamentals.md#json-pointer) 字符串，指示已更改或添加的特定字段的路径。 |
| `value` | 分配给新字段或更新字段的值。 |

{style=&quot;table-layout:auto&quot;}
