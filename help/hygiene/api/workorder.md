---
title: 工单API端点
description: 数据卫生API中的/workorder端点允许您以编程方式管理标识的删除任务。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 8e21bcc7b9d7fe3f4d26f80f953d454f090b0928
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 3%

---

# [!BADGE 测试版]{type=Informational}工作单终结点 {#work-order-endpoint}

此 `/workorder` 数据卫生API中的端点允许您在Adobe Experience Platform中以编程方式管理记录删除请求。

>[!IMPORTANT]
> 
>记录删除功能当前为测试版，仅在 **限量发行**. 并非所有客户都可使用。 记录删除请求仅适用于受限版本中的组织。
>
>记录删除旨在用于数据清理、匿名数据删除或数据最小化。 他们是 **非** 用于数据主体权利请求（符合），与通用数据保护条例(GDPR)等隐私法规相关。 对于所有合规性用例，使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而是。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看 [概述](./overview.md) 有关相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 创建记录删除请求 {#create}

您可以通过对POST发出请求，从单个数据集或所有数据集中删除一个或多个标识。 `/workorder` 端点。

**API格式**

```http
POST /workorder
```

**请求**

取决于 `datasetId` API调用在请求有效负载中提供，它将删除您指定的所有数据集或单个数据集中的身份。 以下请求从特定数据集中删除三个身份。

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
        "displayName": "Example Record Delete Request",
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
| `action` | 要执行的操作。 该值必须设置为 `delete_identity` 用于记录删除。 |
| `datasetId` | 如果您要从单个数据集中删除，此值必须是相关数据集的ID。 如果要从所有数据集中删除，则将该值设置为 `ALL`.<br><br>如果要指定单个数据集，则该数据集的关联体验数据模型(XDM)架构必须定义主标识。 |
| `displayName` | 记录删除请求的显示名称。 |
| `description` | 记录删除请求的描述。 |
| `identities` | 一个数组，其中包含您要删除其信息的至少一个用户的身份。 每个身份都由 [身份命名空间](../../identity-service/namespaces.md) 和一个值：<ul><li>`namespace`：包含单个字符串属性， `code`，表示身份命名空间。 </li><li>`id`：身份值。</ul>如果 `datasetId` 指定单个数据集，每个实体位于 `identities` 必须使用与架构的主身份相同的身份命名空间。<br><br>如果 `datasetId` 设置为 `ALL`， `identities` 数组不受任何单个命名空间的限制，因为每个数据集可能不同。 但是，如所报告，您的请求仍会限制您的组织可用的命名空间 [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**响应**

成功的响应将返回记录删除的详细信息。

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
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 删除订单的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织 ID。 |
| `bundleId` | 与此删除顺序关联的捆绑包的ID，用于调试目的。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于记录删除，值为 `identity-delete`. |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求约束的数据集的ID。 如果请求适用于所有数据集，则该值将设置为 `ALL`. |

{style="table-layout:auto"}

## 检索记录删除的状态(#lookup)

之后 [创建记录删除请求](#create)，您可以使用GET请求检查其状态。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 此 `workorderId` 您正在查找的记录删除的日志。 |

{style="table-layout:auto"}

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

成功的响应将返回删除操作的详细信息，包括其当前状态。

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
  "displayName": "Example Record Delete Request",
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
| `workorderId` | 删除订单的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织 ID。 |
| `bundleId` | 与此删除顺序关联的捆绑包的ID，用于调试目的。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于记录删除，值为 `identity-delete`. |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求约束的数据集的ID。 如果请求适用于所有数据集，则该值将设置为 `ALL`. |
| `productStatusDetails` | 一个数组，列出与请求相关的下游进程的当前状态。 每个数组对象包含以下属性：<ul><li>`productName`：下游服务的名称。</li><li>`productStatus`：来自下游服务的请求的当前处理状态。</li><li>`createdAt`：服务发布最新状态的时间戳。</li></ul> |

## 更新记录删除请求

您可以更新 `displayName` 和 `description` 请求删除PUT记录。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 此 `workorderId` 您正在查找的记录删除的日志。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X PUT \
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
| `displayName` | 记录删除请求的更新显示名称。 |
| `description` | 更新了记录删除请求的描述。 |

{style="table-layout:auto"}

**响应**

成功的响应将返回记录删除的详细信息。

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
| `workorderId` | 删除订单的ID。 这可用于稍后查找删除的状态。 |
| `orgId` | 您的组织 ID。 |
| `bundleId` | 与此删除顺序关联的捆绑包的ID，用于调试目的。 多个删除订单捆绑在一起，由下游服务处理。 |
| `action` | 工作单正在执行的操作。 对于记录删除，值为 `identity-delete`. |
| `createdAt` | 创建删除顺序的时间戳。 |
| `updatedAt` | 上次更新删除顺序的时间戳。 |
| `status` | 删除顺序的当前状态。 |
| `createdBy` | 创建删除顺序的用户。 |
| `datasetId` | 受请求约束的数据集的ID。 如果请求适用于所有数据集，则该值将设置为 `ALL`. |
| `productStatusDetails` | 一个数组，列出与请求相关的下游进程的当前状态。 每个数组对象包含以下属性：<ul><li>`productName`：下游服务的名称。</li><li>`productStatus`：来自下游服务的请求的当前处理状态。</li><li>`createdAt`：服务发布最新状态的时间戳。</li></ul> |

{style="table-layout:auto"}
