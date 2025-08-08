---
title: 数据集过期API端点
description: 数据卫生API中的/ttl端点允许您在Adobe Experience Platform中以编程方式计划数据集过期时间。
role: Developer
exl-id: fbabc2df-a79e-488c-b06b-cd72d6b9743b
source-git-commit: ca6d7d257085da65b3f08376f0bd32e51e293533
workflow-type: tm+mt
source-wordcount: '2331'
ht-degree: 1%

---

# 数据集到期端点

使用数据卫生API中的`/ttl`端点安排何时删除Adobe Experience Platform中的数据集。

数据集到期是延迟的删除操作。 数据集在过渡期间不受保护，并可能在计划到期之前通过其他方式删除。

>[!NOTE]
>
>尽管过期时间指定为特定的即时时间，但在实际删除开始之前，过期后最多可能有24小时的延迟。 开始删除后，可能需要长达7天时间，才会从Experience Platform系统中删除数据集的所有跟踪。

在开始删除之前，您可以取消过期或更改其计划时间。 要重新打开已取消的过期时间，请设置一个新的过期时间。

删除开始后，到期作业将标记为`executing`，无法再修改。 数据集最多可以恢复7天，但只能通过手动Adobe服务请求进行。 在删除期间，数据湖、Identity Service和实时客户档案分别删除了数据集内容。 删除完成后，过期时间将标记为`completed`。

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

您可以通过向`/ttl`端点发出GET请求，列出为组织配置的所有数据集过期日期。

使用查询参数筛选结果，以仅返回符合您标准的过期日期。 每个结果都包括每个数据集到期的状态和配置详细信息。

**API格式**

```http
GET /ttl?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETERS}` | 可选查询参数的列表，多个参数以`&`个字符分隔。 通用参数包括`limit`和`page`以用于分页。 有关支持的查询参数的完整列表，请参阅[附录部分](#query-params)支持的查询参数的完整列表。 最常用的参数包括下面以及附录。 |
| `author` | 按最近更新或创建数据集到期的用户进行筛选。 支持类似SQL的模式（例如，`LIKE %john%`）。 |
| `datasetId` | 按特定数据集ID筛选过期日期。 |
| `datasetName` | 数据集名称匹配的不区分大小写的过滤器。 |
| `status` | 按逗号分隔的状态列表筛选： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiryDate` | 筛选具有特定过期日期的过期日期。 |
| `limit` | 指定要返回的结果的最大数目（1-100，默认值： 25）。 |
| `page` | 使用从零开始的索引（默认页面大小：50，最大值：100）对结果进行分页。 |

{style="table-layout:auto"}

**请求**

以下请求可检索在2021年8月1日之前更新并由名称与“Jane Doe”匹配的用户最后更新的所有数据集过期日期。

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
      "ttlId": "SD-c9f113f2-d751-44bc-bc20-9d5ca0b6ae15",
      "datasetId": "3e9f815ae1194c65b2a4c5ea",
      "datasetName": "Acme_Profile_Engagements",
      "sandboxName": "acme-beta",
      "displayName": "Engagement Data Retention Policy",
      "description": "Scheduled expiry for Acme marketing data",
      "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
      "status": "pending",
      "expiry": "2027-01-12T17:15:31.000Z",
      "updatedAt": "2026-12-15T12:40:20.000Z",
      "updatedBy": "t.lannister@acme.com <t.lannister@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
    }
  ],
  "current_page": 0,
  "total_pages": 1,
  "total_count": 1
}
```

| 属性 | 描述 |
| --- | --- |
| `results` | 数据集过期配置数组。 |
| `ttlId` | 数据集到期配置的唯一标识符。 |
| `datasetId` | 与此配置关联的数据集的唯一标识符。 |
| `datasetName` | 数据集的名称。 |
| `sandboxName` | 配置此数据集到期的沙盒。 |
| `displayName` | 易于用户识别的到期配置名称。 |
| `description` | 到期配置的描述。 |
| `imsOrg` | 您的独特组织标识符。 |
| `status` | 到期的当前状态。 `pending`、`executing`、`cancelled`、`completed`之一。 |
| `expiry` | 计划的到期日期和时间（ISO 8601格式）。 |
| `updatedAt` | 此配置的上次更新时间戳。 |
| `updatedBy` | 上次更新配置的用户或服务的标识符和电子邮件。 |
| `current_page` | 当前结果页的索引（从零开始）。 |
| `total_pages` | 可用的结果页总数。 |
| `total_count` | 返回的数据集过期配置记录总数。 |

{style="table-layout:auto"}

## 查找数据集过期 {#lookup}

通过发出GET请求，使用数据集到期ID或数据集ID作为path参数，检索特定数据集到期配置的详细信息。

>[!IMPORTANT]
>
>您可以在路径中提供数据集过期ID（例如，`SD-xxxxxx-xxxx`）或数据集ID。 响应中的`ttlId`是数据集到期的唯一标识符。

**API格式**

```http
GET /ttl/{ID}
GET /ttl/{ID}?include=history
```

| 参数 | 描述 |
| --- | --- |
| `{ID}` | 数据集到期配置的唯一标识符。 您可以提供数据集过期ID或数据集ID。 |
| `include` | （可选）如果设置为`history`，则响应将包含具有配置更改事件的`history`数组。 |

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
    "displayName": "Delete Acme Data before 2025",
    "description": "The Acme information in this dataset is licensed for our use through the end of 2024.",
    "imsOrg": "885737B25DC460C50A49411B@AdobeOrg",
    "status": "pending",
    "expiry": "2035-09-25T00:00:00Z",
    "updatedAt": "2025-05-01T19:00:55.000Z",
    "updatedBy": "Jane Doe <jdoe@adobe.com> 77A51F696282E48C0A494 012@64d18d6361fae88d49412d.e",
}
```

| 属性 | 描述 |
| --- | --- |
| `ttlId` | 数据集到期配置的唯一标识符。 |
| `datasetId` | 数据集的唯一标识符。 |
| `datasetName` | 数据集的名称。 |
| `sandboxName` | 配置数据集到期的沙盒。 |
| `displayName` | 易于用户识别的数据集过期配置名称。 |
| `description` | 数据集到期配置的描述。 |
| `imsOrg` | 您与此配置关联的唯一组织标识符。 |
| `status` | 数据集到期配置的当前状态。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 数据集的计划到期时间戳（ISO 8601格式）。 |
| `updatedAt` | 最近更新的时间戳。 |
| `updatedBy` | 上次更新数据集过期时间的用户或服务的标识符和电子邮件。 |

{style="table-layout:auto"}

### 目录到期标记

使用[目录API](../../catalog/api/getting-started.md)查找数据集详细信息时，如果数据集具有活动过期日期，它将列在`tags.adobe/hygiene/ttl`下。

以下JSON显示过期值为`32503680000000`的数据集的截断目录API响应。 标记将过期编码为自Unix纪元以来的毫秒数。

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

创建新的数据集过期配置，以定义数据集将过期并符合删除条件的时间。\
提供数据集ID、到期日期或日期时间（以ISO 8601格式）、显示名称和（可选）描述。

>[!NOTE]
>
>有效期值可以是日期(YYYY-MM-DD)或日期和时间(YYYY-MM-DDTHH:MM:SSZ)。 如果只提供日期，则系统使用当天的午夜UTC (00:00:00Z)。 到期时间在将来必须至少为24小时。

要创建数据集过期，请发送POST请求，如下所示。

>[!TIP]
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
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "datasetId": "3e9f815ae1194c65b2a4c5ea",
        "expiry": "2030-12-31",
        "displayName": "Expiry rule for Acme customers",
        "description": "Set expiration for Acme customer dataset"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `datasetId` | **必填。**&#x200B;要应用过期的数据集的唯一标识符。 |
| `expiry` | **必填。** ISO 8601格式的到期日期和时间。 这会定义系统中数据的生命周期。 如果只提供日期，则默认为UTC午夜(00:00:00Z)。 过期&#x200B;**在未来**&#x200B;必须至少为24小时。 <br>**注释**：<ul><li>如果数据集已存在数据集过期，请求将失败。</li></ul> |
| `displayName` | **必填。**&#x200B;数据集到期配置的可读名称。 |
| `description` | 数据集到期配置的可选描述。 |

**响应**

成功的响应会返回HTTP 201（已创建）状态和新的数据集到期配置。

```json
{
  "ttlId": "SD-2aaf113e-3f17-4321-bf29-a2c51152b042",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Expiry rule for Acme customers",
  "description": "Set expiration for Acme customer dataset",
  "imsOrg": "{ORG_ID}",
  "status": "pending",
  "expiry": "2030-12-31T00:00:00Z",
  "updatedAt": "2025-01-02T10:35:45.000Z",
  "updatedBy": "s.stark@acme.com <s.stark@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| 属性 | 描述 |
| --- | --- |
| `ttlId` | 已创建数据集到期配置的唯一标识符。 |
| `datasetId` | 数据集的唯一标识符。 |
| `datasetName` | 数据集的名称。 |
| `sandboxName` | 配置此数据集到期的沙盒。 |
| `displayName` | 数据集到期配置的显示名称。 |
| `description` | 数据集到期配置的描述。 |
| `imsOrg` | 您与此配置关联的唯一组织标识符。 |
| `status` | 数据集到期配置的当前状态。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 数据集的计划到期时间戳。 |
| `updatedAt` | 最近更新的时间戳。 |
| `updatedBy` | 上次更新数据集过期配置的用户或服务的标识符和电子邮件。 |

如果数据集已存在数据集过期，则出现400（错误请求）HTTP状态。 如果不存在此类数据集或您无权访问该数据集，则会出现404（未找到）HTTP状态。

## 更新数据集过期配置 {#update}

要更新现有数据集到期配置，请向`/ttl/DATASET_EXPIRATION_ID`发出PUT请求。 您只能更新配置的`displayName`、`description`和`expiry`字段。 仅当过期状态为`pending`时才允许更新。

>[!NOTE]
>
>`expiry`字段接受日期(YYYY-MM-DD)或日期和时间(YYYY-MM-DDTHH:MM:SSZ)。 如果只提供日期，则系统使用当天的午夜UTC (00:00:00Z)。 过期&#x200B;**在未来**&#x200B;必须至少为24小时。

**API格式**

```http
PUT /ttl/{DATASET_EXPIRATION_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_EXPIRATION_ID}` | 数据集到期配置的唯一标识符。 **注意**：这称为响应中的`ttlId`。 |

**请求**

以下请求更新数据集过期`SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45`的过期、显示名称和描述：

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "displayName": "Customer Dataset Expiry Rule",
        "description": "Updated description for Acme customer dataset",
        "expiry": "2031-06-15"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `displayName` | （可选）适用于数据集到期配置的可读新名称。 |
| `description` | （可选）数据集到期配置的新描述。 |
| `expiry` | （可选）ISO 8601格式的新到期日期或日期和时间。 如果只提供日期，则默认为UTC午夜。 到期时间必须在未来&#x200B;**至少24小时**。 |

>[!NOTE]
>
>请求中必须提供这些字段中的至少一个字段。

**响应**

成功的响应返回HTTP状态200 （正常）以及更新的数据集到期配置。

```json
{
  "ttlId": "SD-c1f902aa-57cb-412e-bb2b-c70b8e1a5f45",
  "datasetId": "3e9f815ae1194c65b2a4c5ea",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Updated description for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "pending",
  "expiry": "2031-06-15T00:00:00Z",
  "updatedAt": "2031-05-01T14:11:12.000Z",
  "updatedBy": "b.tarth@acme.com <b.tarth@acme.com> 3E9F815AE1194C65B2A4C5EA@acme.com"
}
```

| 属性 | 描述 |
| --- | --- |
| `ttlId` | 已更新数据集到期配置的唯一标识符。 |
| `datasetId` | 数据集的唯一标识符。 |
| `datasetName` | 数据集的名称。 |
| `sandboxName` | 配置此数据集到期的沙盒。 |
| `displayName` | 数据集到期配置的显示名称。 |
| `description` | 数据集到期配置的描述。 |
| `imsOrg` | 与此配置关联的组织ID。 |
| `status` | 数据集到期配置的当前状态。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 数据集的计划到期时间戳。 |
| `updatedAt` | 最近更新的时间戳。 |
| `updatedBy` | 上次更新数据集过期配置的用户或服务的标识符和电子邮件。 |

{style="table-layout:auto"}

如果不存在此类数据集过期，则失败的响应会返回404 （未找到）HTTP状态。

## 取消数据集过期 {#delete}

通过向`/ttl/{ID}`发出DELETE请求，取消挂起的数据集过期配置。

>[!NOTE]
>
>只能取消处于`pending`状态的数据集过期日期。 尝试取消已经是`executing`、`completed`或`cancelled`的过期操作会返回HTTP 400（错误请求）。

**API格式**

```http
DELETE /ttl/{ID}
```

| 参数 | 描述 |
| --- | --- |
| `{ID}` | 数据集到期配置的唯一标识符。 您可以提供数据集过期ID或数据集ID。 |

{style="table-layout:auto"}

**请求**

以下请求取消了ID为`SD-d4a7d918-283b-41fd-bfe1-4e730a613d21`的数据集过期：

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/hygiene/ttl/SD-d4a7d918-283b-41fd-bfe1-4e730a613d21 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200 （正常）以及已取消的数据集过期配置。 不是过期的`status`属性设置为`cancelled`。

```json
{
  "ttlId": "SD-d4a7d918-283b-41fd-bfe1-4e730a613d21",
  "datasetId": "5a9e2c68d3b24f03b55a91ce",
  "datasetName": "Acme_Customer_Data",
  "sandboxName": "acme-prod",
  "displayName": "Customer Dataset Expiry Rule",
  "description": "Cancelled expiry configuration for Acme customer dataset",
  "imsOrg": "C9D8E7F6A5B41234567890AB@AcmeOrg",
  "status": "cancelled",
  "expiry": "2032-02-28T00:00:00Z",
  "updatedAt": "2032-01-15T08:27:31.000Z",
  "updatedBy": "s.clegane@acme.com <s.clegane@acme.com> 5A9E2C68D3B24F03B55A91CE@acme.com"
}
```

| 属性 | 描述 |
|---|---|
| `ttlId` | 已删除数据集到期配置的唯一标识符。 |
| `datasetId` | 数据集的唯一标识符。 |
| `datasetName` | 数据集的名称。 |
| `sandboxName` | 配置此数据集到期的沙盒。 |
| `displayName` | 数据集到期配置的显示名称。 |
| `description` | 数据集到期配置的描述。 |
| `imsOrg` | 您与此配置关联的唯一组织标识符。 |
| `status` | 数据集到期配置的当前状态。<br>其中之一： `pending`、`executing`、`cancelled`、`completed`。 |
| `expiry` | 数据集的计划到期时间戳。 |
| `updatedAt` | 最近更新的时间戳。 |
| `updatedBy` | 上次更新数据集过期配置的用户或服务的标识符和电子邮件。 |

**示例400 （错误请求）响应**

尝试取消具有`executing`、`completed`或`cancelled`过期配置的数据集时出现400错误。

```json
{
  "type": "http://ns.adobe.com/aep/errors/HYGN-3102-400",
  "title": "The requested dataset already has an existing expiration. Additional detail: A TTL already exists for datasetId=686e9ca25ef7462aefe72c93",
  "status": 400,
  "report": {
    "tenantInfo": {
      "sandboxName": "prod",
      "sandboxId": "not-applicable",
      "imsOrgId": "{IMS_ORG_ID}"
    },
    "additionalContext": {
      "Invoking Client ID": "acp_privacy_hygiene"
    }
  },
  "error-chain": [
    {
      "serviceId": "HYGN",
      "errorCode": "HYGN-3102-400",
      "invokingServiceId": "acp_privacy_hygiene",
      "unixTimeStampMs": 1754408150394
    }
  ]
}
```

>[!NOTE]
>
>尝试取消已经是`completed`或`cancelled`的数据集过期时出现404错误。

## 附录

### 接受的查询参数 {#query-params}

下表概述了[列出数据集过期时间](#list)时可用的查询参数：

>[!NOTE]
>
>`description`、`displayName`和`datasetName`参数都包含按LIKE值搜索的功能。 这意味着您可以通过搜索字符串“Name1”来查找名为“Name123”、“Name183”、“DisplayName1234”的计划数据集过期时间。

| 参数 | 描述 | 示例 |
| --- | --- | --- |
| `author` | 使用`author`查询参数查找最近更新了数据集到期的人员。 如果自创建后未进行任何更新，则将与到期的原始创建者匹配。 此参数与`created_by`字段与搜索字符串对应的过期日期匹配。<br>如果搜索字符串以`LIKE`或`NOT LIKE`开头，则其余部分将被视为SQL搜索模式。 否则，整个搜索字符串将被视为必须完全匹配`created_by`字段的整个内容的文字字符串。 | `author=LIKE %john%`, `author=John Q. Public` |
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

