---
title: 数据集过期API端点
description: 数据卫生API中的/ttl端点允许您在Adobe Experience Platform中以编程方式计划数据集过期时间。
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 2%

---

# 数据集到期端点

>[!IMPORTANT]
>
>Adobe Experience Platform中的数据卫生功能目前仅适用于已购买的组织 **AdobeHealth Shield** 或 **Adobe隐私和安全防护**.

此 `/ttl` 数据卫生API中的端点允许您计划Adobe Experience Platform中数据集的过期日期。

数据集过期只是定时延迟的删除操作。 数据集在过渡期间不受保护，因此在达到过期时间之前，可以通过其他方式将其删除。

>[!NOTE]
>
>尽管到期被指定为特定的即时时间，但在实际删除开始之前，到期后最多可能有24小时的延迟。 开始删除后，可能需要长达7天时间，才会从Platform系统中删除数据集的所有跟踪。

在实际启动数据集删除之前，您可以随时取消过期时间或修改其触发时间。 取消数据集到期后，您可以通过设置新到期来重新打开它。

开始删除数据集后，其过期作业将标记为 `executing`，并且不得进一步更改。 数据集本身最多可以恢复7天，但只能通过Adobe服务请求启动的手动过程恢复。 在请求执行时，数据湖、Identity Service和Real-time Customer Profile开始单独的进程，以从各自的服务中删除数据集的内容。 从所有三个服务中删除数据后，到期将标记为 `executed`.

>[!WARNING]
>
>如果数据集设置为过期，则必须手动更改任何可能正在将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看 [概述](./overview.md) 有关相关文档的链接，请参阅本文档中的示例API调用指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 列出数据集过期时间 {#list}

您可以通过发出GET请求来列出贵组织的所有数据集过期日期。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 可选查询参数列表，多个参数由以下字符分隔 `&` 个字符。 常见参数包括 `size` 和 `page` 用于分页。 有关支持的查询参数的完整列表，请参阅 [附录部分](#query-params). |

{style="table-layout:auto"}

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

成功的响应将列出生成的数据集过期时间。 以下示例的空格已被截断。

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
| `totalRecords` | 与列表调用的参数匹配的数据集过期次数。 |
| `ttlDetails` | 包含返回的数据集过期时间的详细信息。 有关数据集到期属性的更多详细信息，请参阅响应部分以发出 [查找调用](#lookup). |

{style="table-layout:auto"}

## 查找数据集过期 {#lookup}

您可以通过GET请求查找数据集到期情况。

**API格式**

```http
GET /ttl/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找其过期时间的数据集的ID。 |

{style="table-layout:auto"}

**请求**

以下请求查找数据集的到期详细信息 `62759f2ede9e601b63a2ee14`：

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl/62759f2ede9e601b63a2ee14 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回数据集到期的详细信息。

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
| `datasetId` | 此到期应用于的数据集的ID。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集到期的当前状态。 |
| `expiry` | 计划删除数据集的日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的描述。 |

{style="table-layout:auto"}

### 目录到期标记

使用时 [目录API](../../catalog/api/getting-started.md) 要查找数据集详细信息，如果数据集具有有效到期日期，则它将在下面列出 `tags.adobe/hygiene/ttl`.

以下JSON表示对目录中数据集详细信息的响应被截断，其过期值为 `32503680000000`. 标记的值将过期时间编码为自Unix纪元开始以来的整数毫秒数。

```json
{
  "63212313c308d51b997858ba": {
    "name": "Test Dataset",
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

## 创建或更新数据集过期 {#create-or-update}

您可以通过PUT请求创建或更新数据集的到期日期。

**API格式**

```http
PUT /ttl/{DATASET_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要为其安排过期时间的数据集的ID。 |

**请求**

以下请求计划一个数据集 `5b020a27e7040801dedbf46e` ，以在2022年底（格林尼治标准时间）删除。 如果未找到数据集的现有过期时间，则会创建新的过期时间。 如果数据集已有待处理过期，则会使用新的更新该过期 `expiry` 值。

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
| `expiry` | 有关何时删除数据集的ISO 8601时间戳。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的可选描述。 |

{style="table-layout:auto"}

**响应**

成功响应将返回数据集到期的详细信息，如果更新了预先存在的到期，则返回HTTP状态200 （正常），如果不存在预先存在的到期，则返回201 （创建）。

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
| `datasetId` | 此到期应用于的数据集的ID。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集到期的当前状态。 |
| `expiry` | 计划删除数据集的日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |

{style="table-layout:auto"}

## 取消数据集过期 {#delete}

您可以通过发出DELETE请求来取消数据集过期。

>[!NOTE]
>
>仅限状态为“ ”的数据集过期时间 `pending` 可以取消。 尝试取消已执行或已取消的到期返回HTTP 404错误。

**API格式**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPIRATION_ID}` | 此 `workorderId` 要取消的数据集过期时间。 |

{style="table-layout:auto"}

**请求**

以下请求取消了ID为的数据集过期 `SD5cfd7a11b25543a9bcd9ef647db3d8df`：

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD5cfd7a11b25543a9bcd9ef647db3d8df \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容），并且过期时间 `status` 属性设置为 `cancelled`.

## 检索数据集的到期状态历史记录

您可以使用查询参数查找特定数据集的到期状态历史记录 `include=history` 在查找请求中。 结果包括关于数据集到期的创建、已应用的任何更新及其取消或执行（如果适用）的信息。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找其过期历史记录的数据集的ID。 |

{style="table-layout:auto"}

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

成功的响应将返回数据集到期的详细信息，其中 `history` 数组，提供详细信息 `status`， `expiry`， `updatedAt`、和 `updatedBy` 其每个记录的更新的属性。

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
| `datasetId` | 此到期应用于的数据集的ID。 |
| `datasetName` | 此过期时间适用的数据集的显示名称。 |
| `sandboxName` | 目标数据集所在的沙盒的名称。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的描述。 |
| `imsOrg` | 您组织的ID。 |
| `history` | 以对象数组形式列出到期更新的历史记录，每个对象包含 `status`， `expiry`， `updatedAt`、和 `updatedBy` 更新时到期的属性。 |

{style="table-layout:auto"}

## 附录

### 接受的查询参数 {#query-params}

下表概述了以下情况下可用的查询参数： [列出数据集过期时间](#list)：

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `size` | 介于1和100之间的整数，表示要返回的最大过期次数。 默认为25。 | `size=50` |
| `page` | 一个整数，指示要返回的过期页。 | `page=3` |
| `orgId` | 匹配组织ID与参数的组织ID匹配的数据集过期日期。 此值默认为 `x-gw-ims-org-id` 标头，并且将被忽略，除非请求提供服务令牌。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `status` | 以逗号分隔的状态列表。 如果包含，则响应将匹配数据集过期时间，而数据集过期时间的当前状态属于列出的状态之一。 | `status=pending,cancelled` |
| `author` | 匹配过期时间 `created_by` 是搜索字符串的匹配项。 如果搜索字符串的开头为 `LIKE` 或 `NOT LIKE`，则余数将被视为SQL搜索模式。 否则，整个搜索字符串将被视为必须完全匹配 `created_by` 字段。 | `author=LIKE %john%` |
| `sandboxName` | 匹配沙盒名称与参数完全匹配的数据集过期时间。 在请求的 `x-sandbox-name` 标头。 使用 `sandboxName=*` 以包含来自所有沙盒的数据集过期时间。 | `sandboxName=dev1` |
| `datasetId` | 匹配应用于特定数据集的过期时间。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `createdDate` | 匹配在指定时间开始的24小时窗口内创建的过期时间。<br><br>请注意，没有时间的日期(例如 `2021-12-07`)表示当天开始的日期时间。 因此， `createdDate=2021-12-07` 指在2021年12月7日创建的从 `00:00:00` 到 `23:59:59.999999999` (UTC)。 | `createdDate=2021-12-07` |
| `createdFromDate` | 匹配在指定时间或之后创建的过期时间。 | `createdFromDate=2021-12-07T00:00:00Z` |
| `createdToDate` | 匹配在指定时间或之前创建的过期时间。 | `createdToDate=2021-12-07T23:59:59.999999999Z` |
| `updatedDate` / `updatedToDate` / `updatedFromDate` | 点赞 `createdDate` / `createdFromDate` / `createdToDate`，但匹配数据集到期的更新时间，而不是创建时间。<br><br>每次编辑时都会考虑更新过期，包括创建、取消或执行过期的时间。 | `updatedDate=2022-01-01` |
| `cancelledDate` / `cancelledToDate` / `cancelledFromDate` | 匹配在指定间隔内任何时间取消的过期日期。 即使稍后重新打开了过期时间（通过为同一数据集设置新过期时间），这也适用。 | `updatedDate=2022-01-01` |
| `completedDate` / `completedToDate` / `completedFromDate` | 匹配在指定间隔内完成的过期时间。 | `completedToDate=2021-11-11-06:00` |
| `expiryDate` / `expiryToDate` / `expiryFromDate` | 匹配在指定间隔内即将执行或已执行的过期时间。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |

{style="table-layout:auto"}
