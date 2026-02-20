---
title: 外部受众API端点
description: 了解如何使用外部受众API从Adobe Experience Platform创建、更新、激活和删除外部受众。
exl-id: eaa83933-d301-48cb-8a4d-dfeba059bae1
source-git-commit: de18b8292f07c143d63d26a45ca541e50b2ed2f3
workflow-type: tm+mt
source-wordcount: '2528'
ht-degree: 4%

---

# 外部受众端点

外部受众允许您将外部源中的配置文件数据上传到Adobe Experience Platform。 您可以使用分段服务API中的`/external-audience`端点将外部受众摄取到Experience Platform、查看详细信息和更新外部受众，以及删除外部受众。

## 护栏

从3月版本开始，在使用外部受众端点时，将强制实施以下防护：

| 护栏 | 限制 | 限制类型 | 描述 |
| --------- | ----- | ---------- | ----------- |
| 每天运行的受众引入次数 | 100 | 系统强制的护栏 | 每天允许的最大受众摄取运行次数。 此限制为每个&#x200B;**沙盒**&#x200B;级别。 |
| 每个受众的摄取数 | 10 | 系统强制的护栏 | 可对指定受众执行的引入次数。 |
| 外部受众规模 | 10 GB | 性能护栏 | 建议外部受众的总大小为10 GB。 |

## 快速入门

>[!IMPORTANT]
>
>本指南中的端点使用`/core/ais`作为前缀，而不是`/core/ups`。

要使用Experience Platform API，您必须已完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将为Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关在[!DNL Experience Platform]中使用沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

## 创建外部受众 {#create-audience}

您可以通过向`/external-audience/`端点发出POST请求来创建外部受众。

**API格式**

```http
POST /external-audience/
```

**请求**

+++ 创建外部受众的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `name` | 字符串 | 外部受众的名称。 |
| `description` | 字符串 | 外部受众的可选描述。 |
| `customAudienceId` | 字符串 | 外部受众的可选标识符。 |
| `fields` | 对象数组 | 字段及其数据类型的列表。 数组中必须至少包含1个字段，且最多包含41个字段。 其中一个字段&#x200B;**必须**&#x200B;是标识字段，并且包含`identityNs`。 创建字段列表时，可以添加以下项目： <ul><li>`name`： **必需**&#x200B;作为外部受众规范一部分的字段的名称。</li><li>`type`： **必需**&#x200B;进入字段的数据类型。 支持的值包括`string`、`number`、`long`、`integer`、`date` (`2025-05-13`)、`datetime` (`2025-05-23T20:19:00+00:00`)和`boolean`。</li><li>`identityNs`： **身份字段必需**&#x200B;身份字段使用的命名空间。 支持的值包括所有有效的命名空间，如`ECID`或`email`。</li><li>`labels`： *可选*&#x200B;字段的访问控制标签数组。 有关可用访问控制标签的详细信息，请参阅[数据使用标签术语表](/help/data-governance/labels/reference.md)。 </li></ul> |
| `sourceSpec` | 对象 | 包含外部受众所在信息的对象。 使用此对象时，您&#x200B;**必须**&#x200B;包括以下信息： <ul><li>`path`： **必需**：外部受众或源中包含外部受众的文件夹的位置。 文件路径&#x200B;**不能**&#x200B;包含任何空格。 例如，如果您的路径为`activation/sample-source/Example CSV File.csv`，则将路径设置为`activation/sample-source/ExampleCSVFile.csv`。 您可以在数据流部分的&#x200B;**Source数据**&#x200B;列中查找到源的路径。</li><li>`type`： **必需**&#x200B;您要从源检索的对象类型。 此值可以是`file`或`folder`。</li><li>`sourceType`： *可选*&#x200B;您要从中检索的源类型。 当前，唯一支持的值为`Cloud Storage`。</li><li>`cloudType`： **必需**&#x200B;云存储的类型，基于源类型。 支持的值包括`S3`、`DLZ`、`GCS`、`Azure`和`SFTP`。</li><li>`baseConnectionId`：基本连接的ID，由源提供程序提供。 如果使用&#x200B;**、**&#x200B;或`cloudType`的`S3`值，则此值为`GCS`必需`SFTP`。 否则，您&#x200B;**不**&#x200B;需要包含此参数。 有关详细信息，请阅读[源连接器概述](../../sources/home.md)。</li></ul> |
| `ttlInDays` | 整数 | 外部受众的数据过期时间（天）。 此值可以设置为1到90。 默认情况下，数据到期设置为30天。 |
| `audienceType` | 字符串 | 外部受众的受众类型。 当前仅支持`people`。 |
| `originName` | 字符串 | **必需**&#x200B;受众的来源。 它指明了受众的来源。 对于外部受众，您应使用`CUSTOM_UPLOAD`。 |
| `namespace` | 字符串 | 受众的命名空间。 默认情况下，此值设置为`CustomerAudienceUpload`。 |
| `labels` | 字符串数组 | 应用于外部受众的访问控制标签。 有关可用访问控制标签的详细信息，请参阅[数据使用标签术语表](/help/data-governance/labels/reference.md)。 |
| `tags` | 字符串数组 | 要应用于外部受众的标记。 添加标记数组时，**必须**&#x200B;使用`tagId`。 有关标记的详细信息，请参阅[管理标记指南](/help/administrative-tags/ui/managing-tags.md)。 |

+++

**响应**

成功的响应会返回HTTP状态202以及新创建的外部受众的详细信息。

+++ 创建外部受众时的示例响应。

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `operationId` | 字符串 | 操作的ID。 您随后可以使用此ID检索受众创建的状态。 |
| `operationDetails` | 对象 | 一个对象，其中包含您为创建外部受众而提交的请求的详细信息。 |
| `name` | 字符串 | 外部受众的名称。 |
| `description` | 字符串 | 外部受众的描述。 |
| `fields` | 对象数组 | 字段及其数据类型的列表。 此数组确定外部受众中所需的字段。 |
| `sourceSpec` | 对象 | 包含外部受众所在信息的对象。 |
| `ttlInDays` | 整数 | 外部受众的数据过期时间（天）。 此值可以设置为1到90。 默认情况下，数据到期设置为30天。 |
| `audienceType` | 字符串 | 外部受众的受众类型。 |
| `originName` | 字符串 | **必需**&#x200B;受众的来源。 它指明了受众的来源。 |
| `namespace` | 字符串 | 受众的命名空间。 |
| `labels` | 字符串数组 | 应用于外部受众的访问控制标签。 有关可用访问控制标签的详细信息，请参阅[数据使用标签术语表](/help/data-governance/labels/reference.md)。 |


+++

## 检索受众创建状态 {#retrieve-status}

您可以通过向`/external-audiences/operations`端点发出GET请求并提供从创建外部受众响应中收到的操作的ID，来检索外部受众提交状态。

**API格式**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{OPERATION_ID}` | 要检索的操作的`id`值。 |

**请求**

+++ 检索外部受众操作状态的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200以及外部受众任务状态的详细信息。

+++ 检索外部受众的任务状态时的示例响应。

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `operationId` | 字符串 | 正在检索的操作的ID。 |
| `status` | 字符串 | 操作的状态。 此值可以是以下值之一： `SUCCESS`、`FAILED`、`PROCESSING`。 |
| `operationDetails` | 对象 | 包含受众详细信息的对象。 |
| `audienceId` | 字符串 | 操作正在提交的外部受众的ID。 |
| `createdBy` | 字符串 | 创建外部受众的用户的ID。 |
| `createdAt` | 长纪元时间戳 | 提交创建外部受众的请求时的时间戳（以秒为单位）。 |
| `updatedBy` | 字符串 | 上次更新受众的用户的ID。 |
| `updatedAt` | 长纪元时间戳 | 上次更新受众的时间戳（以秒为单位）。 |

+++

## 更新外部受众 {#update-audience}

>[!NOTE]
>
>若要使用以下端点，您需要具有外部受众的`audienceId`。 通过成功调用`audienceId`终结点，您可以获取`GET /external-audiences/operations/{OPERATION_ID}`。

您可以通过向`/external-audience`端点发出PATCH请求并在请求路径中提供受众的ID来更新外部受众的字段。

使用此端点时，您可以更新以下字段：

- 受众描述
- 字段级访问控制标签
- 受众级别的访问控制标签
- 受众的数据过期时间

使用此终结点&#x200B;**更新字段将替换**&#x200B;您请求的字段内容。

**API格式**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**请求**

+++ 更新外部受众描述的示例请求。

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `description` | 字符串 | 更新了外部受众的描述。 |

此外，您还可以更新以下参数：

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `labels` | 数组 | 一个数组，其中包含受众的更新访问标签列表。 有关可用访问控制标签的详细信息，请参阅[数据使用标签术语表](/help/data-governance/labels/reference.md)。 |
| `fields` | 对象数组 | 一个数组，其中包含外部受众的字段及其关联标签。 仅更新PATCH请求中列出的字段。 有关可用访问控制标签的详细信息，请参阅[数据使用标签术语表](/help/data-governance/labels/reference.md)。 |
| `ttlInDays` | 整数 | 外部受众的数据过期时间（天）。 此值可以设置为1到90。 |

+++

**响应**

成功的响应返回HTTP状态200以及已更新外部受众的详细信息。

+++ 更新外部受众的描述时的示例响应。

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## 开始受众引入 {#start-audience-ingestion}

>[!IMPORTANT]
>
>如果以前的受众引入已在进行中，则您&#x200B;**无法**&#x200B;为外部受众开始新的引入。

>[!NOTE]
>
>若要使用以下端点，您需要具有外部受众的`audienceId`。 通过成功调用`audienceId`终结点，您可以获取`GET /external-audiences/operations/{OPERATION_ID}`。

您可以在提供受众ID的同时，通过向以下端点发出POST请求来开始受众摄取。

**API格式**

```http
POST /external-audience/{AUDIENCE_ID}/runs
```

**请求**

以下请求会触发外部受众的摄取运行。

+++ 开始受众摄取的示例请求。

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Epoch时间戳 | **必需**&#x200B;指定开始时间的范围，以确定将处理哪些文件。 这意味着所选文件将在指定时间&#x200B;**后**&#x200B;成为文件。 |
| `dataFilterEndTime` | Epoch时间戳 | 指定流运行的结束时间以选择要处理的文件的范围。 这意味着所选文件将在指定时间&#x200B;**之前**&#x200B;的文件。 |

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关摄取运行的详细信息。

+++ 开始受众摄取时的示例响应。

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `audienceName` | 字符串 | 您正在为其开始引入运行的受众的名称。 |
| `audienceId` | 字符串 | 受众的ID。 |
| `runId` | 字符串 | 您启动的引入运行的ID。 |
| `differentialIngestion` | 布尔值 | 一个字段，可根据自上次引入或完全受众引入后的差异确定引入是部分引入还是完全引入。 |
| `dataFilterStartTime` | Epoch时间戳 | 指定流运行的开始时间，以选择已处理的文件的范围。 |
| `dataFilterEndTime` | Epoch时间戳 | 指定流运行的结束时间，以选择已处理的文件的范围。 |
| `createdAt` | 长纪元时间戳 | 提交创建外部受众的请求时的时间戳（以秒为单位）。 |
| `createdBy` | 字符串 | 创建外部受众的用户的ID。 |

+++

## 检索特定受众摄取状态 {#retrieve-ingestion-status}

>[!NOTE]
>
>若要使用以下端点，您需要同时具有外部受众的`audienceId`和引入运行ID的`runId`。 您可从对`audienceId`端点的成功调用中获取`GET /external-audiences/operations/{OPERATION_ID}`，并从先前对`runId`端点的成功调用中获取`POST /external-audience/{AUDIENCE_ID}/runs`。

您可以在提供受众和运行ID的同时，通过向以下端点发出GET请求来检索受众摄取状态。

**API格式**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**请求**

以下请求检索外部受众的摄取状态。

+++ 检索外部受众摄取状态的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200以及外部受众摄取的详细信息。

+++ 检索外部受众摄取时的示例响应。

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `audienceName` | 字符串 | 受众的名称。 |
| `audienceId` | 字符串 | 受众的ID。 |
| `runId` | 字符串 | 摄取运行的ID。 |
| `status` | 字符串 | 摄取运行的状态。 可能的状态包括`SUCCESS`和`FAILED`。 |
| `differentialIngestion` | 布尔值 | 一个字段，可根据自上次引入或完全受众引入后的差异确定引入是部分引入还是完全引入。 |
| `dataFilterStartTime` | Epoch时间戳 | 指定流运行的开始时间，以选择已处理的文件的范围。 |
| `dataFilterEndTime` | Epoch时间戳 | 指定流运行的结束时间，以选择已处理的文件的范围。 |
| `createdAt` | 长纪元时间戳 | 提交创建外部受众的请求时的时间戳（以秒为单位）。 |
| `createdBy` | 字符串 | 创建外部受众的用户的ID。 |
| `details` | 对象数组 | 包含摄取运行详细信息的对象。 <ul><li>`stage`：引入运行的阶段。 这可以是`DATASET_INGEST`或`PROFILE_STORE_INGEST`，它们表示数据湖摄取和配置文件摄取。</li><li>`status`：阶段中的摄取状态。 可能的状态包括`SUCCESS`和`FAILED`。</li><li>`flowRunId`：阶段的摄取流运行的ID。</li></ul> |

+++

## 列出受众摄取运行 {#list-ingestion-runs}

>[!NOTE]
>
>若要使用以下端点，您需要具有外部受众的`audienceId`。 通过成功调用`audienceId`终结点，您可以获取`GET /external-audiences/operations/{OPERATION_ID}`。

您可以在提供受众ID的同时向以下端点发出GET请求，以检索所选外部受众的所有摄取运行。 可以包含多个参数，以&amp;符号(`&`)分隔。

**API格式**

<!-- The following endpoint supports several query parameters to help filter your results. While these parameters are optional, their use is strongly recommended to help focus your results. -->

```http
GET /external-audience/{AUDIENCE_ID}/runs
```

<!-- **Query parameters**

+++ A list of available query parameters. 

| Parameter | Description | Example |
| --------- | ----------- | ------- |
| `limit` | The maximum number of items returned in the response. This value can range from 1 to 40. By default, the limit is set to 20. | `limit=30` |
| `sortBy` | The order in which the returned items are sorted. You can sort by either `name` or by `createdAt`. Additionally, you can add a `-` sign to sort by **descending** order instead of **ascending** order. By default, the items are sorted by `createdAt` in descending order. | `sortBy=name` |
| `property` | A filter to determine which audience ingestion runs are displayed. You can filter on the following properties: <ul><li>`name`: Lets you filter by the audience name. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li><li>`createdAt`: Lets you filter by the ingestion time. If using this property, you can compare by using `>=` or `<=`.</li><li>`status`: Lets you filter by the ingestion run's status. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li></ul>  | `property=createdAt<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++ -->

**请求**

以下请求检索为外部受众运行的所有摄取。

+++ 获取受众摄取运行列表的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含指定外部受众的摄取运行列表。

+++ 检索受众摄取列表时运行的示例响应。

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}"
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}"
        }
    ]
}
```

<!-- ,
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
    
| `_page` | Object | An object that contains the pagination information about the list of results. |
     -->

| 属性 | 类型 | 描述 |
| -------- | ---- | ----------- |
| `runs` | 对象 | 一个对象，其中包含属于该受众的摄取运行列表。 有关此对象的详细信息，请参阅[检索摄取状态部分](#retrieve-ingestion-status)。 |

+++

## 延长外部受众的数据过期时间 {#extend-data-expiration}

>[!NOTE]
>
>若要使用以下端点，您需要具有外部受众的`audienceId`。 通过成功调用`audienceId`终结点，您可以获取`GET /external-audiences/operations/{OPERATION_ID}`。

您可以在提供受众ID的同时向以下端点发出POST请求，以延长外部受众的数据过期时间。

数据过期时间会延长到摄取期间设置的原始持续时间。 如果未指定持续时间，则应用30天的默认扩展。 延长数据过期时间后，系统将使用上次成功摄取的数据重新摄取受众。

**API格式**

```http
/ais/external-audience/extend-ttl/{AUDIENCE_ID}
```

**请求**

以下请求扩展指定外部受众的数据过期时间。

+++ 延长外部受众数据到期时间的示例请求。

```shell
curl -x POST https://platform.adobe.io/data/core/ais/external-audience/extend-ttl/60ccea95-1435-4180-97a5-58af4aa285ab \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200以及受众的详细信息。

+++ 延长数据过期时间的示例响应。

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "name": "Sample external audience"
}
```

+++

## 删除外部受众 {#delete-audience}

>[!NOTE]
>
>若要使用以下端点，您需要具有外部受众的`audienceId`。 通过成功调用`audienceId`终结点，您可以获取`GET /external-audiences/operations/{OPERATION_ID}`。

您可以在提供受众ID的同时，通过向以下端点发出DELETE请求来删除外部受众。

**API格式**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**请求**

以下请求删除指定的外部受众。

+++ 删除外部受众的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回带有空响应正文的HTTP状态204。

## 后续步骤 {#next-steps}

阅读本指南后，您现在可以更好地了解如何使用Experience Platform API创建、管理和删除外部受众。 要了解如何通过Experience Platform UI使用外部受众，请阅读[受众门户文档](../ui/audience-portal.md)。

## 附录 {#appendix}

以下部分列出了使用外部受众API时可用的错误代码。

| 平台错误代码 | 状态代码 | 消息 | 描述 |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | 由于验证请求时出现错误，因此发生了错误请求。 |
| 100911-400 | 400 | `BAD_REQUEST` | 提供了无效的令牌。 |
| 100920-401 | 401 | `UNAUTHORIZED` | 缺少标头。 |
| 100921-401 | 401 | `UNAUTHORIZED` | 提供了无效的`imsOrgId`。 |
| 100922-401 | 401 | `UNAUTHORIZED` | 您无权使用外部受众API。 |
| 100940-404 | 404 | `NOT_FOUND` | 未找到所请求的受众。 |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | 受众已存在。 |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | 请求结构有效，但由于逻辑或语义错误而无法处理。 |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | 在系统中处理请求时出现问题。 |
| 100970-502 | 502 | `BAD_GATEWAY` | 存在下游依赖关系问题。 |
