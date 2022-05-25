---
title: 工作单API端点
description: 数据卫生API中的/workorder端点允许您以编程方式管理消费者身份的删除任务。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 3%

---

# 工作单端点

>[!IMPORTANT]
>
>Adobe Experience Platform中的Adobe卫生功能目前仅适用于已购买Data Shield for Healthcare的组织。

的 `/workorder` 数据卫生API中的端点允许您以编程方式管理Adobe Experience Platform中消费者身份的删除任务。

## 快速入门

本指南中使用的端点是数据卫生API的一部分。 在继续之前，请查看 [概述](./overview.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 删除标识 {#delete-identities}

您可以通过向 `/workorder` 端点。

**API格式**

```http
POST /workorder
```

**请求**

根据 `datasetId` 在请求负载中提供，API调用将从您指定的所有数据集或单个数据集中删除用户身份。 以下请求会从特定数据集中删除三个客户身份。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `action` | 要执行的操作。 值必须设置为 `delete_identity` 删除身份时。 |
| `datasetId` | 如果从单个数据集中删除，则此值必须是相关数据集的ID。 如果从所有数据集中删除，请将值设置为 `ALL`.<br><br>如果您指定单个数据集，则数据集关联的体验数据模型(XDM)架构必须定义主标识。 |
| `identities` | 一个数组，其中包含您要删除其信息的至少一个用户的标识。 每个身份由 [标识命名空间](../../identity-service/namespaces.md) 和一个值：<ul><li>`namespace`:包含单个字符串属性， `code`，表示身份命名空间。 </li><li>`id`:标识值。</ul>如果 `datasetId` 指定单个数据集，每个实体位于 `identities` 必须使用与架构的主标识相同的标识命名空间。<br><br>如果 `datasetId` 设置为 `ALL`, `identities` 数组不受任何单个命名空间的限制，因为每个数据集可能不同。 但是，您的请求仍会受到组织可用的命名空间的约束，如 [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回身份删除的详细信息。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除顺序的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您组织的ID。 |
| `batchId` | 与此删除顺序关联的批次的ID，用于调试。 多个删除订单将捆绑在一个批次中，以供下游服务处理。 |
| `bundleOrdinal` | 将此删除订单捆绑到批处理中以进行下游处理时收到该订单的顺序。 用于调试。 |
| `payloadByteSize` | 创建此删除顺序的请求有效负载中提供的身份列表的大小（以字节为单位）。 |
| `operationCount` | 此删除顺序适用的标识数。 |
| `createdAt` | 创建删除顺序的时间戳。 |
| `responseMessage` | 系统返回的最新响应。 如果在处理过程中发生错误，则此值将是一个JSON字符串，其中包含详细的错误信息，以帮助您了解可能出了什么问题。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |

{style=&quot;table-layout:auto&quot;}

## 列出所有身份删除的状态 {#list}

您可以通过发出GET请求来列出所有身份删除的状态。

**API格式**

```http
GET /workorder?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMS}` | 列表调用的可选查询参数列表，其中多个参数以 `&` 字符。 已接受的查询参数如下：<ul><li>`data`  — 一个布尔值，当设置为 `true`，包括收到的所有其他删除订单请求和响应数据。 默认为 `false`。</li><li>`start`  — 搜索删除订单的时间范围开始的时间戳。</li><li>`end`  — 用于搜索删除订单的时间范围结束的时间戳。</li><li>`page`  — 要返回的特定响应页面。</li><li>`limit`  — 每页要显示的记录数。</li></ul> |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回所有删除操作的详细信息，包括其当前状态。 以下示例响应已被截断为空格。

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `results` | 包含删除订单列表及其详细信息。 有关删除顺序属性的更多信息，请参阅 [查找删除顺序](#lookup). |
| `total` | 根据当前过滤器找到的删除订单总数。 |
| `count` | 在响应的每个页面上找到的删除订单总数。 |
| `_links` | 包含分页信息，可帮助您探索其余响应：<ul><li>`next`:包含响应中下一页的URL。</li><li>`page`:包含一个URL模板，用于在响应中访问其他页面或调整每个页面上返回的项目数。</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 检索身份删除的状态(#lookup)

向发送请求后 [删除身份](#delete-identities)，则可以使用GET请求检查其状态。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 的 `workorderId` 的身份删除。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回删除操作的详细信息，包括其当前状态。

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除顺序的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您组织的ID。 |
| `batchId` | 与此删除顺序关联的批次的ID，用于调试。 多个删除订单将捆绑在一个批次中，以供下游服务处理。 |
| `bundleOrdinal` | 将此删除订单捆绑到批处理中以进行下游处理时收到该订单的顺序。 用于调试。 |
| `payloadByteSize` | 创建此删除顺序的请求有效负载中提供的身份列表的大小（以字节为单位）。 |
| `operationCount` | 此删除顺序适用的标识数。 |
| `createdAt` | 创建删除顺序的时间戳。 |
| `responseMessage` | 系统返回的最新响应。 如果在处理过程中发生错误，则此值将是一个JSON字符串，其中包含详细的错误信息，以帮助您了解可能出了什么问题。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
