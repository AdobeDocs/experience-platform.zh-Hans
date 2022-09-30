---
title: 工作单API端点
description: 数据卫生API中的/workorder端点允许您以编程方式管理消费者身份的删除任务。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 83149c4e6e8ea483133da4766c37886b8ebd7316
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 4%

---

# 工作单端点

>[!IMPORTANT]
>
>Adobe Experience Platform中的Adobe卫生功能目前仅适用于已购买Data Healthcare Shield的组织。

的 `/workorder` 数据卫生API中的端点允许您以编程方式在Adobe Experience Platform中管理消费者删除请求。

## 快速入门

本指南中使用的端点是数据卫生API的一部分。 在继续之前，请查看 [概述](./overview.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 创建消费者删除请求 {#delete-consumers}

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
        "displayName": "Example Consumer Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
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
| `action` | 要执行的操作。 值必须设置为 `delete_identity` 用于消费者删除。 |
| `datasetId` | 如果从单个数据集中删除，则此值必须是相关数据集的ID。 如果从所有数据集中删除，请将值设置为 `ALL`.<br><br>如果您指定单个数据集，则数据集关联的体验数据模型(XDM)架构必须定义主标识。 |
| `displayName` | 消费者删除请求的显示名称。 |
| `description` | 消费者删除请求的描述。 |
| `identities` | 一个数组，其中包含您要删除其信息的至少一个用户的标识。 每个身份由 [标识命名空间](../../identity-service/namespaces.md) 和一个值：<ul><li>`namespace`:包含单个字符串属性， `code`，表示身份命名空间。 </li><li>`id`:标识值。</ul>如果 `datasetId` 指定单个数据集，每个实体位于 `identities` 必须使用与架构的主标识相同的标识命名空间。<br><br>如果 `datasetId` 设置为 `ALL`, `identities` 数组不受任何单个命名空间的限制，因为每个数据集可能不同。 但是，您的请求仍会受到组织可用的命名空间的约束，如 [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回用户删除的详细信息。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除顺序的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织ID。 |
| `bundleId` | 与此删除顺序关联的包的ID，用于调试。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于消费者删除，值为 `identity-delete`. |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求影响的数据集的ID。 如果请求适用于所有数据集，则会将值设置为 `ALL`. |

{style=&quot;table-layout:auto&quot;}

## 检索消费者删除的状态(#lookup)

之后 [创建消费者删除请求](#delete-consumers)，则可以使用GET请求检查其状态。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 的 `workorderId` 您正在查找的消费者删除。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回删除操作的详细信息，包括其当前状态。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除顺序的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织ID。 |
| `bundleId` | 与此删除顺序关联的包的ID，用于调试。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于消费者删除，值为 `identity-delete`. |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求影响的数据集的ID。 如果请求适用于所有数据集，则会将值设置为 `ALL`. |
| `productStatusDetails` | 列出与请求相关的下游进程的当前状态的数组。 每个数组对象都包含以下属性：<ul><li>`productName`:下游服务的名称。</li><li>`productStatus`:来自下游服务的请求的当前处理状态。</li><li>`createdAt`:服务发布最新状态的时间戳。</li></ul> |

## 更新消费者删除请求

您可以更新 `displayName` 和 `description` 用户通过发出PUT请求进行删除。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 的 `workorderId` 您正在查找的消费者删除。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `displayName` | 消费者删除请求的更新显示名称。 |
| `description` | 消费者删除请求的更新描述。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功的响应会返回用户删除的详细信息。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除顺序的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织ID。 |
| `bundleId` | 与此删除顺序关联的包的ID，用于调试。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于消费者删除，值为 `identity-delete`. |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求影响的数据集的ID。 如果请求适用于所有数据集，则会将值设置为 `ALL`. |
| `productStatusDetails` | 列出与请求相关的下游进程的当前状态的数组。 每个数组对象都包含以下属性：<ul><li>`productName`:下游服务的名称。</li><li>`productStatus`:来自下游服务的请求的当前处理状态。</li><li>`createdAt`:服务发布最新状态的时间戳。</li></ul> |

{style=&quot;table-layout:auto&quot;}
