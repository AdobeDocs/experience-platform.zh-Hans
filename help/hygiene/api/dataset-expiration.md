---
title: 数据集过期API端点
description: 数据卫生API中的/ttl端点允许您以编程方式计划Adobe Experience Platform中的数据集过期时间。
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: e4cc78591d0d3b4abd660956b1263092697d63d5
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 4%

---

# 数据集过期端点

>[!IMPORTANT]
>
>目前，Adobe Experience Platform中的Adobe卫生功能仅适用于已购买Analytics Healthcare Shield或Privacy Shield的组织。

的 `/ttl` 数据卫生API中的端点允许您为Adobe Experience Platform中的数据集计划过期日期。

数据集过期只是一个定时延迟的删除操作。 在此期间，数据集未受到保护，因此在数据集过期之前，可能会通过其他方式将其删除。

>[!NOTE]
>
>尽管将到期指定为特定的及时间，但在实际删除开始之前，在到期后可能会有长达24小时的延迟。 启动删除后，可能最多需要七天时间才能从Platform系统中删除数据集的所有跟踪。

在实际启动数据集删除之前，您可以随时取消过期时间或修改其触发时间。 取消数据集过期后，您可以通过设置新的过期时间来重新打开数据集。

启动数据集删除后，其过期作业将标记为 `executing`，且不得进一步更改。 数据集本身最多可恢复七天，但只能通过通过Adobe服务请求启动的手动流程来恢复。 请求执行时，数据湖、Identity Service和实时客户配置文件会开始单独的进程，以从各自的服务中删除数据集的内容。 从所有这三项服务中删除数据后，过期时间将标记为 `executed`.

>[!WARNING]
>
>如果数据集设置为过期，您必须手动更改任何可能将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

## 快速入门

本指南中使用的端点是数据卫生API的一部分。 在继续之前，请查看 [概述](./overview.md) 有关相关文档的链接，请参阅本文档中的API调用示例指南，以及有关成功调用任何Experience PlatformAPI所需标头的重要信息。

## 列出数据集过期日期 {#list}

您可以通过发出GET请求，列出贵组织的所有数据集过期日期。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 可选查询参数列表，其中多个参数之间以 `&` 字符。 常见参数包括 `size` 和 `page` 中，用于分页。 有关支持的查询参数的完整列表，请参阅 [附录节](#query-params). |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%Jane Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会列出生成的数据集过期日期。 以下示例已截断空格。

```json
{
  "totalRecords": 3,
  "ttlDetails": [
    {
      "status": "completed",
      "workorderId": "SDc17a9501345c4997878c1383c475a77b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "f440ac301c414bf1b6ba419162866346",
      "expiry": "2021-07-07T13:14:15Z",
      "updatedAt": "2021-07-07T13:14:15Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD8ef60b33dbed444fb81861cced5da10b",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "80f0d38820a74879a2c5be82e38b1a94",
      "expiry": "2099-02-02T00:00:00Z",
      "updatedAt": "2021-02-02T13:00:00Z",
      "updatedBy": "John Q. Public <jqp@example.com> 93220281bad34ed0@AdobeId"
    },
    {
      "status": "pending",
      "workorderId": "SD2140ad4eaf1f47a1b24c05cce53e303e",
      "imsOrgId": "885737B25DC460C50A49411B@AdobeOrg",
      "datasetId": "9e63f9b25896416ba811657678b4fcb7",
      "expiry": "2099-01-01T00:00:00Z",
      "updatedAt": "2021-01-01T13:00:00Z",
      "updatedBy": "Jane Doe <jane.doe@example.com> d741b5b877bf47cf@AdobeId"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `totalRecords` | 与列表调用参数匹配的数据集过期次数计数。 |
| `ttlDetails` | 包含返回的数据集过期日期的详细信息。 有关数据集过期属性的更多详细信息，请参阅做出 [对照调用](#lookup). |

{style=&quot;table-layout:auto&quot;}

## 查找数据集过期时间 {#lookup}

您可以通过GET请求查找数据集过期日期。

**API格式**

```http
GET /ttl/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找其过期时间的数据集的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会查找数据集的过期详细信息 `62759f2ede9e601b63a2ee14`:

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回数据集过期的详细信息。

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2023-12-31T23:59:59Z",
    "updatedAt": "2022-05-11T15:12:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Dataset Expiration Request",
    "description": "A dataset expiration request that will execute at the end of 2023"
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 数据集过期的ID。 |
| `datasetId` | 此过期时间所应用的数据集的ID。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集过期的当前状态。 |
| `expiry` | 删除数据集的计划日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的描述。 |

{style=&quot;table-layout:auto&quot;}

### 目录到期标记

使用 [目录API](../../catalog/api/getting-started.md) 要查找数据集详细信息，如果数据集具有活动过期时间，则将列在 `tags.adobe/hygiene/ttl`.

以下JSON表示数据集详细信息从“目录”中截断的响应，该响应的过期值为 `32503680000000`. 标记的值会将到期编码为自Unix纪元开始以来的整数毫秒数。

```json
{
  "63212313c308d51b997858ba": {
    "name": "TTL Test Dataset",
    "description": "A piecrust promise, made to be broken",
    "imsOrg": "0FCC747E56F59C747F000101@AdobeOrg",
    "sandboxId": "8dc51b90-d0f9-11e9-b164-ed6a398c8b35",
    "tags": {
      "adobe/hygiene/ttl": [ "32503680000000" ],
      ...
    },
    ...
  }
}
```

## 创建或更新数据集过期时间 {#create-or-update}

您可以通过PUT请求为数据集创建或更新过期日期。

**API格式**

```http
PUT /ttl/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要计划过期时间的数据集的ID。 |

**请求**

以下请求计划一个数据集 `5b020a27e7040801dedbf46e` 于2022年底（格林威治标准时间）删除。 如果找不到数据集的现有过期时间，则会创建新的过期时间。 如果数据集已具有待处理的过期时间，则该过期时间将更新为 `expiry` 值。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/5b020a27e7040801dedbf46e \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2022-12-31T23:59:59Z",
        "displayName": "Example Expiration Request",
        "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `expiry` | 删除数据集的时间的ISO 8601时间戳。 |
| `displayName` | 过期请求的显示名称。 |
| `description` | 到期请求的可选描述。 |

{style=&quot;table-layout:auto&quot;}

**响应**

成功响应会返回数据集过期的详细信息，如果更新了预先存在的过期，则HTTP状态为200（确定）；如果没有预先存在的过期，则返回201（已创建）。

```json
{
    "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "{ORG_ID}",
    "status": "pending",
    "expiry": "2032-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "{USER_ID}",
    "displayName": "Example Expiration Request",
    "description": "Cleanup identities required by JIRA request 12345 across all datasets in the prod sandbox."
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 数据集过期的ID。 |
| `datasetId` | 此过期时间所应用的数据集的ID。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集过期的当前状态。 |
| `expiry` | 删除数据集的计划日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |

{style=&quot;table-layout:auto&quot;}

## 取消数据集过期 {#delete}

您可以通过发出DELETE请求来取消数据集过期。

>[!NOTE]
>
>只有状态为 `pending` 可以取消。 尝试取消已执行或已取消的过期时间会返回HTTP 404错误。

**API格式**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPIRATION_ID}` | 的 `workorderId` 要取消的数据集过期时间的值。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会取消ID为的数据集过期 `SD5cfd7a11b25543a9bcd9ef647db3d8df`:

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）和过期时间 `status` 属性设置为 `cancelled`.

## 检索数据集的过期状态历史记录

您可以使用查询参数查找特定数据集的过期状态历史记录 `include=history` 在查找请求中。 结果包括有关创建数据集过期时间、已应用的任何更新及其取消或执行（如果适用）的信息。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找其过期历史记录的数据集的ID。 |

{style=&quot;table-layout:auto&quot;}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14?include=history \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回数据集过期的详细信息，其中包含 `history` 提供其详细信息的阵列 `status`, `expiry`, `updatedAt`和 `updatedBy` 属性。

```json
{
  "workorderId": "SD5cfd7a11b25543a9bcd9ef647db3d8df",
  "datasetId": "62759f2ede9e601b63a2ee14",
  "datasetName": "Example Dataset",
  "sandboxName": "prod",
  "displayName": "Expiration Request 123",
  "description": "Expiration Request 123 Description",
  "imsOrg": "{ORG_ID}",
  "status": "cancelled",
  "expiry": "2022-05-09T23:47:30.071186Z",
  "updatedAt": "2022-05-09T23:47:30.071186Z",
  "updatedBy": "{USER_ID}",
  "history": [
    {
      "status": "created",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:38:40.393115Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "updated",
      "expiry": "2032-12-31T23:59:59Z",
      "updatedAt": "2022-05-09T22:41:46.731002Z",
      "updatedBy": "{USER_ID}"
    },
    {
      "status": "cancelled",
      "expiry": "2022-05-09T23:47:30.071186Z",
      "updatedAt": "2022-05-09T23:47:30.071186Z",
      "updatedBy": "{USER_ID}"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 数据集过期的ID。 |
| `datasetId` | 此过期时间所应用的数据集的ID。 |
| `datasetName` | 此过期时间所适用的数据集的显示名称。 |
| `sandboxName` | 目标数据集所在的沙盒名称。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的描述。 |
| `imsOrg` | 您组织的ID。 |
| `history` | 将过期时间的更新历史记录列为对象数组，每个对象都包含 `status`, `expiry`, `updatedAt`和 `updatedBy` 属性。 |

{style=&quot;table-layout:auto&quot;}

## 附录

### 已接受的查询参数 {#query-params}

下表概述了 [列出数据集过期日期](#list):

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `size` | 介于1到100之间的整数，用于指示要返回的最大过期次数。 默认为25。 | `size=50` |
| `page` | 一个整数，指示要返回的过期页面。 | `page=3` |
| `orgId` | 匹配组织ID与参数ID匹配的数据集过期日期。 此值默认为 `x-gw-ims-org-id` 标头，和将被忽略，除非请求提供服务令牌。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | 以逗号分隔的状态列表。 包含后，响应将匹配数据集过期日期，数据集当前状态属于所列状态之一。 | `status=pending,cancelled` |
| `author` | 匹配过期日期，其 `created_by` 是搜索字符串的匹配项。 如果搜索字符串以开头 `LIKE` 或 `NOT LIKE`，则其余部分将被视为SQL搜索模式。 否则，整个搜索字符串将被视为必须与 `created_by` 字段。 | `author=LIKE %john%` |
| `sandboxName` | 匹配沙盒名称与参数完全匹配的数据集过期日期。 默认为请求中的沙盒名称 `x-sandbox-name` 标题。 使用 `sandboxName=*` 以包含所有沙箱的数据集过期日期。 | `sandboxName=dev1` |
| `datasetId` | 匹配应用于特定数据集的过期日期。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | 匹配在24小时窗口中创建的过期日期，从指定时间开始。<br><br>请注意，日期没有时间(例如 `2021-12-07`)表示当天开始的日期时间。 因此， `createdDate=2021-12-07` 是指2021年12月7日创建的任何 `00:00:00` 至 `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 匹配在指定时间或之后创建的过期日期。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 匹配在指定时间或之前创建的过期日期。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 赞 `createdDate` / `createdFromDate` / `createdToDate`，但与数据集过期的更新时间（而不是创建时间）匹配。<br><br>每次编辑时都会考虑更新过期日期，包括创建、取消或执行该日期的时间。 | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 在指定的间隔内随时取消的匹配过期日期。 即使以后重新打开过期时间（通过为同一数据集设置新的到期），也是如此。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 匹配在指定间隔内完成的过期时间。 | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 在指定的间隔内，匹配将要执行或已执行的过期日期。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style=&quot;table-layout:auto&quot;}
