---
title: 数据集过期API端点
description: 数据卫生API中的/ttl端点允许您在Adobe Experience Platform中以编程方式计划数据集过期时间。
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1966'
ht-degree: 2%

---

# 数据集到期端点

数据卫生API中的`/ttl`端点允许您安排Adobe Experience Platform中数据集的过期日期。

数据集到期只是定时延迟的删除操作。 数据集在过渡期间不受保护，因此在达到过期时间之前，可以通过其他方式将其删除。

>[!NOTE]
>
>尽管过期时间指定为特定的即时时间，但在实际删除开始之前，过期后最多可能有24小时的延迟。 开始删除后，可能需要长达7天时间，才会从Experience Platform系统中删除数据集的所有跟踪。

在实际启动数据集删除之前，您可以随时取消过期时间或修改其触发时间。 取消数据集到期后，可以通过设置新到期来重新打开数据集。

开始删除数据集后，其到期作业将标记为`executing`，并且不能进一步更改。 数据集本身最多可以恢复7天，但只能通过Adobe服务请求启动的手动流程进行恢复。 在请求执行时，数据湖、Identity Service和Real-time Customer Profile开始单独的进程，以从各自的服务中删除数据集的内容。 从所有三个服务中删除数据后，到期将被标记为`completed`。

>[!WARNING]
>
>如果数据集设置为过期，则必须手动更改任何可能正在将数据摄取到该数据集的数据流，以便下游工作流不会受到负面影响。

高级数据生命周期管理支持通过数据集到期终结点进行数据集删除，以及通过[工作单终结点](./workorder.md)使用主标识进行ID删除（行级数据）。 您还可以通过Experience Platform UI管理[数据集过期](../ui/dataset-expiration.md)和[记录删除](../ui/record-delete.md)。 有关更多信息，请参阅链接的文档。

>[!NOTE]
>
>数据生命周期不支持批量删除。

## 快速入门

本指南中使用的端点属于数据卫生API。 在继续之前，请查看[API指南](./overview.md)，了解有关CRUD操作所需的标头、错误消息、Postman集合以及如何读取示例API调用的信息。

>[!IMPORTANT]
>
>调用数据卫生API时，必须使用 — H `x-sandbox-name: {SANDBOX_NAME}`标头。

## 列出数据集过期时间 {#list}

您可以通过发出GET请求来列出贵组织的所有数据集过期日期。 查询参数可用于筛选响应以获取相应的结果。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 可选查询参数的列表，多个参数以`&`个字符分隔。 通用参数包括`limit`和`page`以用于分页。 有关支持的查询参数的完整列表，请参阅[附录部分](#query-params)。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/ttl?updatedToDate=2021-08-01&author=LIKE%20%25Jane%20Doe%25 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将列出生成的数据集过期日期。 以下示例的空间已被截断。

>[!IMPORTANT]
>
>响应中的`ttlId`也称为`{DATASET_EXPIRATION_ID}`。 它们都引用数据集到期的唯一标识符。

```json
{
  "results": [
    {
      "ttlId": "SD-b16c8b48-a15a-45c8-9215-587ea89369bf",
      "datasetId": "629bd9125b31471b2da7645c",
      "datasetName": "Sample Acme dataset",
      "sandboxName": "hygiene-beta",
      "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
      "status": "pending",
      "expiry": "2050-01-01T00:00:00Z",
      "updatedAt": "2023-06-09T16:52:44.136028Z",
      "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| 属性 | 描述 |
| --- | --- |
| `total_count` | 与列表调用的参数匹配的数据集过期计数。 |
| `results` | 包含返回的数据集过期的详细信息。 有关数据集到期属性的更多详细信息，请参阅有关进行[查找调用](#lookup)的响应部分。 |

{style="table-layout:auto"}

## 查找数据集过期 {#lookup}

要查找数据集过期时间，请使用`{DATASET_ID}`或`{DATASET_EXPIRATION_ID}`发出GET请求。

>[!IMPORTANT]
>
>`{DATASET_EXPIRATION_ID}`在响应中称为`ttlId`。 它们都引用数据集到期的唯一标识符。

**API格式**

```http
GET /ttl/{DATASET_ID}?include=history
GET /ttl/{DATASET_EXPIRATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 要查找其过期时间的数据集的ID。 |
| `{DATASET_EXPIRATION_ID}` | 数据集过期的ID。 |

{style="table-layout:auto"}

**请求**

以下请求查找数据集`62759f2ede9e601b63a2ee14`的到期详细信息：

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
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "62759f2ede9e601b63a2ee14",
    "datasetName": "XtVRwq9-38734",
    "sandboxName": "prod",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2024-05-11T15:12:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| 属性 | 描述 |
| --- | --- |
| `ttlId` | 数据集过期的ID。 |
| `datasetId` | 此到期应用于的数据集的ID。 |
| `datasetName` | 此过期应用于的数据集的显示名称。 |
| `sandboxName` | 目标数据集所在的沙盒的名称。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集到期的当前状态。 |
| `expiry` | 计划删除数据集的日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的描述。 |

{style="table-layout:auto"}

### 目录到期标记

使用[目录API](../../catalog/api/getting-started.md)查找数据集详细信息时，如果数据集具有活动过期日期，它将列在`tags.adobe/hygiene/ttl`下。

以下JSON表示从目录中对数据集详细信息的截断响应，其过期值为`32503680000000`。 标记的值将过期时间编码为自Unix纪元开始以来的整数毫秒数。

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

## 创建数据集过期 {#create}

要确保在指定的时间段后从系统中删除数据，请以ISO 8601格式提供数据集ID以及过期日期和时间，从而安排特定数据集的过期时间。

要创建数据集过期，请执行如下所示的POST请求，并在有效负荷中提供下面提到的值。

>[!NOTE]
>
>如果您收到404错误，请确保请求没有其他正斜杠。 尾随斜杠可能会导致POST请求失败。

**API格式**

```http
POST /ttl
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/ttl \
  -H `Authorization: Bearer {ACCESS_TOKEN}`
  -H `x-gw-ims-org-id: {ORG_ID}`
  -H `x-api-key: {API_KEY}`
  -H `Accept: application/json`
  -d {
      "datasetId": "5b020a27e7040801dedbf46e",
      "expiry": "2030-12-31T23:59:59Z"
      "displayName": "Delete Acme Data before 2025",
      "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }
```

| 属性 | 描述 |
| --- | --- |
| `datasetId` | **必需**&#x200B;要为其计划过期的目标数据集的ID。 |
| `expiry` | **必需** ISO 8601格式的日期和时间。 如果字符串没有明确的时区偏移，则假定时区为UTC。 系统内的数据寿命根据提供的失效值设置。<br>注意：<ul><li>如果数据集已存在数据集过期，请求将失败。</li><li>此日期和时间必须至少为将来&#x200B;**24小时**。</li></ul> |
| `displayName` | 数据集过期请求的可选显示名称。 |
| `description` | 到期请求的可选描述。 |

**响应**

成功的响应会返回HTTP 201（已创建）状态和数据集过期的新状态。

```json
{
  "ttlId":       "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
  "datasetId":   "5b020a27e7040801dedbf46e",
  "datasetName": "Acme licensed data",
  "sandboxName": "prod",
  "imsOrg":      "{ORG_ID}",
  "status":      "pending",
  "expiry":      "2030-12-31T23:59:59Z",
  "updatedAt":   "2021-08-19T11:14:16Z",
  "updatedBy":   "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
  "displayName": "Delete Acme Data before 2031",
  "description": "The Acme information in this dataset is licensed for our use through the end of 2030."
}
```

| 属性 | 描述 |
| --- | --- |
| `ttlId` | 数据集过期的ID。 |
| `datasetId` | 此到期应用于的数据集的ID。 |
| `datasetName` | 此过期应用于的数据集的显示名称。 |
| `sandboxName` | 目标数据集所在的沙盒的名称。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集到期的当前状态。 |
| `expiry` | 计划删除数据集的日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的描述。 |

如果数据集已存在数据集过期，则出现400（错误请求）HTTP状态。 如果不存在此类数据集过期（或您无权访问数据集），则失败的响应将返回404 （未找到）HTTP状态。

## 更新数据集过期 {#update}

要更新数据集的过期日期，请使用PUT请求和`ttlId`。 您可以更新`displayName`、`description`和/或`expiry`信息。

>[!NOTE]
>
>如果更改过期日期和时间，则以后必须至少为24小时。 这种强制的延迟为您提供了取消或重新计划到期日的机会，并可避免任何意外的数据丢失。

**API格式**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | 要更改的数据集过期的ID。 注意：这称为响应中的`ttlId`。 |

**请求**

以下请求将数据集过期`SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f`重新安排为2024年底（格林尼治标准时间）。 如果发现现有数据集过期，则会使用新的`expiry`值更新该过期。

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "expiry": "2024-12-31T23:59:59Z",
        "displayName": "Delete Acme Data before 2025",
        "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `expiry` | **必需** ISO 8601格式的日期和时间。 如果字符串没有明确的时区偏移，则假定时区为UTC。 系统内的数据寿命根据提供的失效值设置。 同一数据集的任何以前到期时间戳将由您提供的新到期值替换。 此日期和时间必须至少为将来&#x200B;**24小时**。 |
| `displayName` | 到期请求的显示名称。 |
| `description` | 到期请求的可选描述。 |

{style="table-layout:auto"}

**响应**

如果更新了预先存在的过期时间，则成功响应将返回数据集过期的新状态和HTTP状态200 （正常）。

```json
{
    "ttlId": "SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f",
    "datasetId": "5b020a27e7040801dedbf46e",
    "imsOrg": "A2A5*EF06164773A8A49418C@AdobeOrg",
    "status": "pending",
    "expiry": "2024-12-31T23:59:59Z",
    "updatedAt": "2022-05-09T22:38:40.393115Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024."
}
```

| 属性 | 描述 |
| --- | --- |
| `ttlId` | 数据集过期的ID。 |
| `datasetId` | 此到期应用于的数据集的ID。 |
| `imsOrg` | 您组织的ID。 |
| `status` | 数据集到期的当前状态。 |
| `expiry` | 计划删除数据集的日期和时间。 |
| `updatedAt` | 上次更新过期时间的时间戳。 |
| `updatedBy` | 上次更新过期时间的用户。 |

{style="table-layout:auto"}

如果不存在此类数据集过期，则失败的响应会返回404 （未找到）HTTP状态。

## 取消数据集过期 {#delete}

您可以通过发出DELETE请求来取消数据集过期。

>[!NOTE]
>
>只能取消状态为`pending`的数据集过期。 尝试取消已执行或已取消的到期返回HTTP 404错误。

**API格式**

```http
DELETE /ttl/{EXPIRATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPIRATION_ID}` | 要取消的数据集的`ttlId`过期。 |

{style="table-layout:auto"}

**请求**

以下请求取消了ID为`SD-b16c8b48-a15a-45c8-9215-587ea89369bf`的数据集过期：

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-b16c8b48-a15a-45c8-9215-587ea89369bf \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容），并且过期的`status`属性设置为`cancelled`。

## 附录

### 接受的查询参数 {#query-params}

下表概述了[列出数据集过期时间](#list)时可用的查询参数：

>[!NOTE]
>
>`description`、`displayName`和`datasetName`参数都包含按LIKE值搜索的功能。 这意味着您可以通过搜索字符串“Name1”来查找名为“Name123”、“Name183”、“DisplayName1234”的计划数据集过期时间。

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `author` | 使用`author`查询参数查找最近更新了数据集到期的人员。 如果自创建后未进行任何更新，则将与到期的原始创建者匹配。 此参数与`created_by`字段与搜索字符串对应的过期日期匹配。<br>如果搜索字符串以`LIKE`或`NOT LIKE`开头，则其余部分将被视为SQL搜索模式。 否则，整个搜索字符串将被视为必须完全匹配`created_by`字段的整个内容的文字字符串。 | `author=LIKE %john%`、`author=John Q. Public` |
| `datasetId` | 匹配应用于特定数据集的过期时间。 | `datasetId=62b3925ff20f8e1b990a7434` |
| `datasetName` | 匹配数据集名称包含提供的搜索字符串的过期时间。 匹配项不区分大小写。 | `datasetName=Acme` |
| `description` |   | `description=Handle expiration of Acme information through the end of 2024.` |
| `displayName` | 匹配显示名称包含提供的搜索字符串的过期时间。 匹配项不区分大小写。 | `displayName=License Expiry` |
| `executedDate` / `executedFromDate` / `executedToDate` | 根据确切的执行日期、执行的结束日期或执行的开始日期过滤结果。 它们用于检索与特定日期、特定日期之前或特定日期之后执行操作相关联的数据或记录。 | `executedDate=2023-02-05T19:34:40.383615Z` |
| `expiryDate` | 匹配在指定日期的24小时窗口内发生的过期。 | `2024-01-01` |
| `expiryToDate` / `expiryFromDate` | 匹配在指定间隔内即将执行或已执行的过期日期。 | `expiryFromDate=2099-01-01&expiryToDate=2100-01-01` |
| `limit` | 介于1和100之间的整数，它表示要返回的最大过期次数。 默认为25。 | `limit=50` |
| `orderBy` | `orderBy`查询参数指定API返回结果的排序顺序。 使用它根据一个或多个字段以升序(ASC)或降序(DESC)顺序排列数据。 使用+或 — 前缀分别表示ASC、DESC。 接受以下值： `displayName`、`description`、`datasetName`、`id`、`updatedBy`、`updatedAt`、`expiry`、`status`。 | `-datasetName` |
| `orgId` | 匹配其组织ID与参数的组织ID匹配的数据集过期日期。 此值默认为`x-gw-ims-org-id`标头的值，除非请求提供服务令牌，否则将忽略该值。 | `orgId=885737B25DC460C50A49411B@AdobeOrg` |
| `page` | 一个整数，它指示要返回的过期页。 | `page=3` |
| `sandboxName` | 匹配沙盒名称与参数完全匹配的数据集过期时间。 默认为请求的`x-sandbox-name`标头中的沙盒名称。 使用`sandboxName=*`包含所有沙盒中的数据集过期时间。 | `sandboxName=dev1` |
| `search` | 匹配过期时间，其中指定的字符串与过期ID完全匹配，或者在以下任何字段中为&#x200B;**包含**：<br><ul><li>作者</li><li>显示名称</li><li>描述</li><li>显示名称</li><li>数据集名称</li></ul> | `search=TESTING` |
| `status` | 以逗号分隔的状态列表。 包含后，响应将与当前状态位于所列数据集中的数据集过期日期相匹配。 | `status=pending,cancelled` |
| `ttlId` | 将过期请求与给定ID匹配。 | `ttlID=SD-c8c75921-2416-4be7-9cfd-9ab01de66c5f` |
| `updatedDate` | 匹配在指定日期的24小时窗口内更新的过期时间。 | `2024-01-01` |
| `updatedToDate` / `updatedFromDate` | 匹配在指定时间开始的24小时窗口内更新的过期时间。<br><br>每次编辑时都会将过期视为已更新，包括创建、取消或执行过期的时间。 | `updatedDate=2022-01-01` |

{style="table-layout:auto"}

