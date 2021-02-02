---
keywords: Experience Platform；主页；热门主题；批处理摄取；批处理；摄取；开发人员指南；api指南；上传；摄取Parke；摄取json;
solution: Experience Platform
title: 批量摄取开发人员指南
topic: developer guide
description: 本文档全面介绍了如何使用批量摄取API。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '2698'
ht-degree: 5%

---


# 批量摄取开发人员指南

本文档全面介绍了如何使用[批处理摄取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。

本文档的附录提供了用于摄取](#data-transformation-for-batch-ingestion)的[格式化数据的信息，包括示例CSV和JSON数据文件。

## 入门指南

数据摄取提供一个RESTful API，通过它可以针对支持的对象类型执行基本的CRUD操作。

以下各节提供您需要了解或掌握的其他信息，以便成功调用Batch Ingestion API。

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

- [批量摄取](./overview.md):允许您将数据作为批处理文件引入Adobe Experience Platform。
- [[!DNL Experience Data Model (XDM)] 系统](../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../sandboxes/home.md)。

包含有效负荷(POST、PUT、PATCH)的请求可能需要额外的`Content-Type`头。 在呼叫参数中提供特定于每个呼叫的已接受值。

## 类型

在摄取数据时，了解[!DNL Experience Data Model](XDM)模式的工作方式很重要。 有关XDM字段类型如何映射到不同格式的详细信息，请阅读[模式注册表开发人员指南](../../xdm/api/getting-started.md)。

收录数据时具有一定的灵活性——如果某个类型与目标模式中的内容不匹配，则数据将转换为表示的目标类型。 如果不能，它将使具有`TypeCompatibilityException`的批处理失败。

例如，JSON和CSV都没有日期或日期时间类型。 因此，这些值使用ISO 8061格式化字符串](https://www.iso.org/iso-8601-date-and-time-format.html)(“2018-07-10T15:05:59.000-08:00”)或以毫秒为单位格式化的Unix时间(153126)来表示3959000)，并在摄取时转换为目标XDM类型。[

下表显示了在摄取数据时支持的转换。

| 入站（行）与目标（列） | 字符串 | 字节 | 短 | 整数 | 长 | 双精度 | 日期 | 日期——时间 | 对象 | 地图 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 字符串 | X | X | X | X | X | X | X | X |  |  |
| 字节 | X | X | X | X | X | X |  |  |  |  |
| 短 | X | X | X | X | X | X |  |  |  |  |
| 整数 | X | X | X | X | X | X |  |  |  |  |
| 长 | X | X | X | X | X | X | X | X |  |  |
| 双精度 | X | X | X | X | X | X |  |  |  |  |
| 日期 |  |  |  |  |  |  | X |  |  |  |
| 日期——时间 |  |  |  |  |  |  |  | X |  |  |
| 对象 |  |  |  |  |  |  |  |  | X | X |
| 地图 |  |  |  |  |  |  |  |  | X | X |

>[!NOTE]
>
>布尔值和数组不能转换为其他类型。

## 摄取约束

批处理数据获取存在一些限制：
- 每批文件的最大数量：1500
- 最大批大小：100 GB
- 每行的属性或字段的最大数量：10000
- 每用户每分钟批次的最大数量：138

## 收录JSON文件

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，您需要切换到大文件上传。

### 创建批

首先，您需要创建以JSON为输入格式的批。 创建批时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM模式。

>[!NOTE]
>
>以下示例适用于单行JSON。 要获取多行JSON，需要设置`isMultiLineJson`标志。 有关详细信息，请阅读[批摄取疑难解答指南](./troubleshooting.md)。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |

### 上传文件

现在您已创建了批，可以使用之前的`batchId`将文件上传到该批。 您可以将多个文件上传到批。

>[!NOTE]
>
>有关格式正确的JSON数据文件](#data-transformation-for-batch-ingestion)的[示例，请参阅附录部分。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批的ID。 |
| `{DATASET_ID}` | 批的引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!NOTE]
>
>API支持单部分上传。 确保content-type为application/octet-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |

**响应**

```http
200 OK
```

### 完成批

上载完文件的所有不同部分后，您需要发出数据已完全上载以及批准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批的ID。 |

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 收录镶木地板文件

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，您需要切换到大文件上传。

### 创建批

首先，您需要创建一个批，输入格式为Parke。 创建批时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM模式。

**请求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "parquet"
           }
      }'
```

| 参数 | 描述 |
| --------- | ------------ |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批的用户的ID。 |

### 上传文件

现在您已创建了批，可以使用之前的`batchId`将文件上传到该批。 您可以将多个文件上传到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批的ID。 |
| `{DATASET_ID}` | 批的引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保content-type为application/octet-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |

**响应**

```http
200 OK
```

### 完成批

上载完文件的所有不同部分后，您需要发出数据已完全上载以及批准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=complete
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要发出信号的批的ID已准备就绪，可以完成。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 摄取大型镶木文件

>[!NOTE]
>
>本节详细介绍如何上传大于256 MB的文件。 大文件以块形式上传，然后通过API信号进行拼接。

### 创建批

首先，您需要创建一个批，输入格式为Parke。 创建批时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM模式。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "parquet"
           }
      }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批的用户的ID。 |

### 初始化大文件

创建批后，您需要先初始化大文件，然后再将块上传到该批。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{FILE_NAME}` | 要初始化的文件的名称。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=INITIALIZE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
201 Created
```

### 上传大文件块

现在已创建文件，所有后续区块都可以通过重复的PATCH请求上传，每个区域对应一个请求。

**API格式**

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批的ID。 |
| `{DATASET_ID}` | 批的引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保content-type为application/octet-stream。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'Content-Range: bytes {CONTENT_RANGE}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONTENT_RANGE}` | 在整数中，为请求范围的开始和结束。 |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |


**响应**

```http
200 OK
```

### 完整大文件

现在您已创建了批，可以使用之前的`batchId`将文件上传到该批。 您可以将多个文件上传到批。

**API格式**

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要发出完成信号的批的ID。 |
| `{DATASET_ID}` | 批的引用数据集的ID。 |
| `{FILE_NAME}` | 要指示完成的文件的名称。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
201 Created
```

### 完成批

上载完文件的所有不同部分后，您需要发出数据已完全上载以及批准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要发出信号的批次的ID已完成。 |


**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 收录CSV文件

要摄取CSV文件，您需要创建支持CSV的类、模式和数据集。 有关如何创建必要类和模式的详细信息，请按照[ad-hoc模式创建教程](../../xdm/api/ad-hoc.md)中提供的说明操作。

>[!NOTE]
>
>以下步骤适用于小文件（256 MB或更小）。 如果遇到网关超时或请求正文大小错误，您需要切换到大文件上传。

### 创建数据集

按照以上说明创建必要的类和模式后，您需要创建可支持CSV的数据集。

**API格式**

```http
POST /catalog/dataSets
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "{DATASET_NAME}",
      "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed+json;version=1"
      },
      "fileDescription": {
          "format": "parquet",
          "delimiters": [","], 
          "quotes": ["\""],
          "escapes": ["\\"],
          "header": true,
          "charset": "UTF-8"
      }      
  }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TENANT_ID}` | 此ID用于确保您创建的资源命名正确且包含在IMS组织中。 |
| `{SCHEMA_ID}` | 您创建的模式的ID。 |

JSON主体的“fileDescription”部分不同部分的说明如下：

```json
{
    "fileDescription": {
        "format": "parquet",
        "delimiters": [","],
        "quotes": ["\""],
        "escapes": ["\\"],
        "header": true,
        "charset": "UTF-8"
    }
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `format` | 已掌握文件的格式，而不是输入文件的格式。 |
| `delimiters` | 用作分隔符的字符。 |
| `quotes` | 用于引号的字符。 |
| `escapes` | 用作转义字符的字符。 |
| `header` | 上传的文件&#x200B;**必须**&#x200B;包含标头。 由于模式验证已完成，因此必须将其设置为true。 此外，标题&#x200B;**不**&#x200B;可能包含任何空格——如果标题中有任何空格，请改为用下划线替换它们。 |
| `charset` | 可选字段。 其他支持的字符集包括“US-ASCII”和“ISO-8869-1”。 如果留空，则默认采用UTF-8。 |

引用的数据集必须上面列出文件描述块，并且必须指向注册表中的有效模式。 否则，文件将不会被掌握到Parke中。

### 创建批

接下来，您需要创建以CSV为输入格式的批。 创建批时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的模式。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
            "datasetId": "{DATASET_ID}",
            "inputFormat": {
                "format": "csv"
            }
      }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批的用户的ID。 |

### 上传文件

现在您已创建了批，可以使用之前的`batchId`将文件上传到该批。 您可以将多个文件上传到批。

>[!NOTE]
>
>有关格式正确的CSV数据文件](#data-transformation-for-batch-ingestion)的[示例，请参阅附录部分。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批的ID。 |
| `{DATASET_ID}` | 批的引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保content-type为application/octet-stream。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.csv \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.csv"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |


**响应**

```http
200 OK
```

### 完成批

上载完文件的所有不同部分后，您需要发出数据已完全上载以及批处理已准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 取消批

批处理时，仍可取消批处理。 但是，一旦批完成（如成功或失败状态），将无法取消该批。

**API格式**

```http
POST /batches/{BATCH_ID}?action=ABORT
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要取消的批的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=ABORT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 删除批处理{#delete-a-batch}

通过对要删除的批的ID执行以下POST请求(将`action=REVERT`查询参数与参数一起执行)，可以删除该批。 批被标记为“非活动”，因此符合垃圾收集条件。 将异步收集批，此时该批将标记为“已删除”。

**API格式**

```http
POST /batches/{BATCH_ID}?action=REVERT
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要删除的批的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=REVERT \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**响应**

```http
200 OK
```

## 重放批

如果要替换已摄取的批，可以使用“批重播”进行替换——此操作等效于删除旧批并改为摄取新批。

### 创建批

首先，您需要创建以JSON为输入格式的批。 创建批时，您需要提供数据集ID。 您还需要确保作为批处理的一部分上传的所有文件都符合链接到提供数据集的XDM模式。 此外，您还需要在重放部分提供旧批作为引用。 在以下示例中，您将重新播放ID为`batchIdA`和`batchIdB`的批。

**API格式**

```http
POST /batches
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
             "format": "json"
           },
            "replay": {
                "predecessors": ["${batchIdA}","${batchIdB}"],
                "reason": "replace"
             }
      }'
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{DATASET_ID}` | 引用数据集的ID。 |

**响应**

```http
201 Created
```

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "replay": {
        "predecessors": [
            "batchIdA", "batchIdB"
        ],
        "reason": "replace"
    },
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 新创建批的ID。 |
| `{DATASET_ID}` | 引用数据集的ID。 |
| `{USER_ID}` | 创建批的用户的ID。 |


### 上传文件

现在您已创建了批，可以使用之前的`batchId`将文件上传到该批。 您可以将多个文件上传到批。

**API格式**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要上传到的批的ID。 |
| `{DATASET_ID}` | 批的引用数据集的ID。 |
| `{FILE_NAME}` | 要上传的文件的名称。 此文件路径是文件在Adobe端保存的位置。 |

**请求**

>[!CAUTION]
>
>此API支持单部分上传。 确保content-type为application/octet-stream。 请勿使用curl -F选项，因为它默认为与API不兼容的多部件请求。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/octet-stream' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

| 参数 | 描述 |
| --------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 您尝试上传的文件的完整路径和名称。 此文件路径是本地文件路径，如`Users/sample-user/Downloads/sample.json`。 |

**响应**

```http
200 OK
```

### 完成批

上载完文件的所有不同部分后，您需要发出数据已完全上载以及批准备好升级的信号。

**API格式**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 要完成的批的ID。 |

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```http
200 OK
```

## 附录

### 用于批量摄取的数据转换

要将数据文件引入[!DNL Experience Platform]中，文件的分层结构必须符合与要上传的数据集关联的[体验数据模型(XDM)](../../xdm/home.md)模式。

有关如何映射CSV文件以符合XDM模式的信息，请参阅[示例转换](../../etl/transformations.md)文档，以及格式正确的JSON数据文件示例。 文档中提供的示例文件可在以下位置找到：

- [CRM_用户档案.csv](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.csv)
- [CRM_用户档案.json](https://github.com/adobe/experience-platform-etl-reference/blob/master/example_files/CRM_profiles.json)