---
keywords: Experience Platform；主页；热门主题；摄取数据；故障诊断；FAQ；摄取；批量摄取；批量摄取；
solution: Experience Platform
title: 批量摄取疑难解答指南
topic-legacy: troubleshooting
description: 本文档将帮助回答有关Adobe Experience Platform批量数据摄取API的常见问题。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# 批量摄取疑难解答指南

本文档将帮助回答有关Adobe Experience Platform的常见问题 [!DNL Batch Data Ingestion] API。

## 批量API调用

### 从CompleteBatch API接收HTTP 200 OK后，批次是否会立即处于活动状态？

的 `200 OK` 来自API的响应意味着批处理已被接受处理 — 在批处理转变为最终状态（如“活动”或“失败”）之前，该批处理不会处于活动状态。

### 在CompleteBatch API调用失败后重试该调用是否安全？

是 — 可以安全地重试API调用。 尽管失败，但操作实际上可能成功，并且批次被成功接受。 但是，在API失败时，客户端应具有重试机制，实际上鼓励客户端重试。 如果操作实际成功，则API将返回成功，即使重试后也是如此。

### 何时应使用大文件上传API?

使用大文件上传API的建议文件大小为256 MB或更大。 有关如何使用大文件上传API的更多信息，请参阅 [此处](./api-overview.md#ingest-large-parquet-files).

### 为何大文件完成API调用失败？

如果发现大文件的区块重叠或缺失，则服务器将响应HTTP 400错误请求。 之所以会出现这种情况，是因为可以上传重叠的区块，因为在文件块拼合在一起时，会在文件完成时完成范围验证。

## 摄取支持

### 支持的摄取格式有哪些？

目前，支持Parquet和JSON。 旧版支持CSV — 虽然数据将提升为主控并完成初步检查，但不支持转换、分区或行验证等现代功能。

### 应该在何处指定批量输入格式？

应在有效负荷内的批量创建时指定输入格式。 有关如何指定批量输入格式的示例，请参见下文：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### 为什么上载的数据没有显示在数据集中？

要在数据集中显示数据，必须将批次标记为完成。 必须先上传要摄取的所有文件，然后才能将批标记为完成。 将批标记为完成的示例如下所示：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 如何摄取多行JSON?

要摄取多行JSON，请 `isMultiLineJson` 标记需要在创建批时设置。 示例如下所示：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### JSON行（单行JSON）与多行JSON之间有何区别？

对于JSON行，每行有一个JSON对象。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

对于多行JSON，一个对象可能占用多行，而所有对象都封装在JSON数组中。 例如：

```json
[
    {"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}},
    {"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}},
    {
        "string": "string3",
        "int": 3,
        "array": [
            3,
            6,
            9
        ],
        "dict": {
            "key": "value3",
            "extra_key": "extra_value3"
        }
    }
]
```

默认情况下， [!DNL Batch Data Ingestion] 使用单行JSON。

### 是否支持CSV摄取？

仅平面架构支持CSV摄取。 目前，不支持以CSV格式摄取分层数据。

要获取所有数据摄取功能，需要使用JSON或Parquet格式。

### 对数据执行哪些类型的验证？

对数据执行了三个级别的验证：

- 架构 — 批量摄取可确保摄取数据的架构与数据集的架构匹配。
- 数据类型 — 批量摄取可确保摄取的每个字段的类型与数据集架构中定义的类型相匹配。
- 约束 — 批量摄取可确保在架构定义中正确定义约束，如“必需”、“枚举”和“格式”。

### 如何替换已摄取的批？

已摄取的批处理可以使用批处理重播功能替换。 有关批量重播的详细信息，请参阅 [此处](./api-overview.md#replay-a-batch).

### 如何监控批量摄取？

在发出批次升级信号后，可通过以下请求监控批量摄取进度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

通过此请求，您将收到类似以下内容的响应：

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{ORG_ID}",
        "created":1494349962314,
        "createdClient":"{API_KEY}",
        "createdUser":"{USER_ID}",
        "updatedUser":"{USER_ID}",
        "completed":1494349963467,
        "externalId":"{EXTERNAL_ID}",
        "status":"staging",
        "errors":[],
    }
}
```

## 批处理状态

### 可能的批处理状态是什么？

批处理在其生命周期中可以完成以下状态：

| 状态 | 写入主控的数据 | 描述 |
| ------ | ---------------------- | ----------- |
| 已放弃 |  | 客户端未能在预期时间范围内完成批处理。 |
| 已中止 |  | 客户端已通过 [!DNL Batch Data Ingestion] API，指定批处理的中止操作。 一旦某个批处理处于“已加载”状态，该批处理将无法中止。 |
| 活动/成功 | x | 该批已成功从阶段提升到主控，现在可用于下游使用。 **注意：** “活动”和“成功”可互换使用。 |
| 已存档 |  | 批已存档到冷存储中。 |
| 失败/失败 |  | 由配置错误和/或数据错误导致的终端状态。 系统会记录可操作的错误以及批次，以便客户能够更正并重新提交数据。 **注意：** “失败”和“失败”可互换使用。 |
| 不活动 | x | 批已成功提升，但已还原或已过期。 该批次将不再可用于下游使用，但基础数据将保留主控，直到其被保留、存档或删除为止。 |
| 正在加载 |  | 客户端当前正在为批处理编写数据。 批次为 **not** 随时准备升职，此时此刻。 |
| 已加载 |  | 客户端已完成写入批处理的数据。 批已准备好进行升级。 |
| 保留 |  | 数据已从主控中提取，并在Adobe数据湖中的指定存档中提取。 |
| 暂存 |  | 客户端已成功发出批次提升的信号，并且正在对数据进行暂存以在下游使用。 |
| 正在重试 |  | 客户端已发出批次升级的信号，但由于出现错误，批次正在由批次监控服务重试。 此状态可用于告知客户端在摄取数据时可能存在延迟。 |
| 停止 |  | 客户已发出批号以进行升级，但之后 `n` 重试，则批量促销已停止。 |

### “暂存”对于批次是什么意思？

当某个批处于“暂存”状态时，这表示已成功发出该批的提升信号，并且正在对数据进行暂存以在下游使用。

### 批处理为“正在重试”时，它意味着什么？

当批处理处于“正在重试”状态时，这意味着该批处理的数据摄取由于间歇性问题而被暂时停止。 发生这种情况时，无需客户干预。

### 批处理为“停止”时，这意味着什么？

当批处于“停止”状态时，表示 [!DNL Data Ingestion Services] 在摄取批处理时遇到困难，且已用尽所有重试。

### 如果批次仍处于“正在加载”状态，则表示什么？

当批处理处于“正在加载”状态时，这表示未调用CompleteBatch API来提升批处理。

### 是否有方法可确定批次是否已成功摄取？

批次状态为“活动”后，即表示已成功摄取该批次。 要了解批的状态，请按照详细的步骤操作 [更早](#how-is-batch-ingestion-monitored).

### 批处理失败后会发生什么情况？

批处理失败时，可以在 `errors` 部分。 错误示例如下所示：

```json
    "errors":[
        {
            "code":"106",
            "description":"Dataset file is empty. Please upload file with data.",
            "rows":[]
        },
        {
            "code":"118",
            "description":"CSV file contains empty header row.",
            "rows":[]
        }
    ]
```

更正错误后，可以重新上传批次。

## 批量支持

### 如何删除批次？

而不是直接从 [!DNL Catalog]，则应使用以下任一方法删除批次：

1. 如果批处理正在进行中，则应中止该批处理。
2. 如果成功掌握了批，则应恢复该批。

### 提供了哪些批量度？

以下批量度可用于处于“活动/成功”状态的批量：

| 量度 | 描述 |
| ------ | ----------- |
| inputByteSize | 的暂存字节数 [!DNL Data Ingestion Services] 处理。 |
| inputRecordSize | 的暂存行总数 [!DNL Data Ingestion Services] 处理。 |
| outputByteSize | 输出的字节总数 [!DNL Data Ingestion Services] to [!DNL Data Lake]. |
| outputRecordSize | 输出的总行数 [!DNL Data Ingestion Services] to [!DNL Data Lake]. |
| partitionCount | 写入的分区总数 [!DNL Data Lake]. |

### 为什么某些量度在批量中不可用？

量度在您的批量中可能不可用的原因有两个：

1. 批次从未成功设置为“活动/成功”状态。
2. 批次是使用旧版促销路径（如CSV摄取）进行促销的。

### 不同的状态代码表示什么？

| 状态代码 | 描述 |
| ----------- | ----------- |
| 106 | 数据集文件为空。 |
| 118 | CSV文件包含空标题行。 |
| 200 | 批已接受处理，并将过渡到最终状态，如“活动”或“失败”。 提交后，即可使用 `GetBatch` 端点。 |
| 400 | 错误请求. 如果批次中缺少块或重叠块，则返回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
