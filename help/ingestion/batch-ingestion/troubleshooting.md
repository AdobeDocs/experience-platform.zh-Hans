---
keywords: Experience Platform；主页；热门主题；摄取的数据；故障排除；faq；摄取；批量摄取；批量摄取；
solution: Experience Platform
title: 批量摄取疑难解答指南
description: 本文档将有助于解答有关Adobe Experience Platform批量数据摄取API的常见问题。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---

# 批量摄取疑难解答指南

此文档可帮助回答有关Adobe Experience Platform [!DNL Batch Data Ingestion] API的常见问题。

## 批处理API调用

### 从CompleteBatch API收到HTTP 200 OK后，批是否立即处于活动状态？

来自API的`200 OK`响应意味着该批次已被接受处理 — 在它转换为最终状态（如“活动”或“失败”）之前，它将处于非活动状态。

### 在CompleteBatch API调用失败后重试是否安全？

是 — 重试API调用是安全的。 尽管失败，但操作可能实际成功，并且已成功接受批次。 但是，当API失败时，客户端应具有重试机制，事实上，建议重试。 如果操作实际成功，则即使重试后，API也将返回成功结果。

### 何时应使用大文件上传API？

建议使用大文件上传API的文件大小为256 MB或更大。 有关如何使用大文件上传API的详细信息，可在[此处](./api-overview.md#ingest-large-parquet-files)找到。

### 为什么大文件完成API调用失败？

如果发现大文件的块重叠或缺失，服务器将使用HTTP 400错误请求进行响应。 出现这种情况的原因是，在文件完成时，当文件块拼合在一起时，可能会上载重叠的块，因为会完成范围验证。

## 摄取支持

### 支持的引入格式有哪些？

目前，Parquet和JSON都受支持。 CSV在旧版的基础上受支持 — 虽然数据将提升为主视图并进行初步检查，但不支持任何新功能，例如转换、分区或行验证。

### 应在何处指定批量输入格式？

应在批量创建时在有效负荷内指定输入格式。 下面显示了如何指定批量输入格式的示例：

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

### 为何上传的数据未出现在数据集中？

为了让数据显示在数据集中，必须将批次标记为完成。 在将批次标记为完成之前，必须上传您要摄取的所有文件。 下面显示了将批次标记为完成的示例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 如何摄取多行JSON？

要摄取多行JSON，需要在创建批次时设置`isMultiLineJson`标志。 下面显示了这方面的示例：

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

### JSON行（单行JSON）和多行JSON之间有何区别？

对于JSON行，每行有一个JSON对象。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

对于多行JSON，一个对象可以占用多行，而所有对象都封装在JSON数组中。 例如：

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

默认情况下，[!DNL Batch Data Ingestion]使用单行JSON。

### 是否支持CSV引入？

仅平面架构支持CSV摄取。 当前，不支持在CSV中引入层次结构数据。

要获取所有数据摄取功能，需要使用JSON或Parquet格式。

### 对数据执行什么类型的验证？

对数据执行三个级别的验证：

- 架构 — 批量摄取可确保摄取数据的架构与数据集的架构匹配。
- 数据类型 — 批量摄取可确保每个摄取的字段的类型与数据集架构中定义的类型匹配。
- 约束 — 批量摄取确保架构定义中正确定义了约束，如“Required”、“enum”和“format”。

### 如何替换已摄取的批次？

已摄取的批次可以通过使用批量重放功能进行替换。 可在[此处](./api-overview.md#replay-a-batch)找到有关批次重播的详细信息。

### 如何监控批量摄取？

在发出批量升级的信号后，可通过以下请求监控批量摄取进度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

对于此请求，您将获得类似于以下内容的响应：

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

## 批次状态

### 可能的批处理状态是什么？

批次在其生命周期中可以经历以下状态：

| 状态 | 数据写入母版 | 描述 |
| ------ | ---------------------- | ----------- |
| 已放弃 | | 客户端未能在预期时间范围内完成批处理。 |
| 已中止 | | 客户端已通过[!DNL Batch Data Ingestion] API显式调用指定批次的中止操作。 当批次处于“已加载”状态时，无法中止该批次。 |
| 活动/成功 | x | 已成功将批次从暂存提升到母版，现在可用于下游使用。 **注意：**&#x200B;活动和成功可互换使用。 |
| 已存档 | | 该批次已存档到冷存储中。 |
| 失败/失败 | | 因配置错误和/或数据错误导致的终端状态。 将记录可操作错误以及批处理，以使客户端能够更正并重新提交数据。 **注意：**&#x200B;失败和失败可互换使用。 |
| 非活动 | x | 已成功提升批次，但已还原或已过期。 该批次将无法再用于下游使用，但基础数据将保留在主数据中，直到它被保留、存档或以其他方式删除。 |
| 正在加载 | | 客户端当前正在写入批次数据。 此时批次&#x200B;**未**&#x200B;准备好进行提升。 |
| 已加载 | | 客户端已完成为批次写入数据。 该批次已准备好进行升级。 |
| 已保留 | | 数据已从Master中获取，并存放在Adobe数据湖中的指定存档中。 |
| 暂存 | | 客户端已成功发出要提升的批次信号，并且正在将数据暂存到下游以供使用。 |
| 正在重试 | | 客户端已发出升级批次的信号，但由于错误，批次正由批量监控服务重试。 此状态可用于告诉客户端摄取数据时可能存在延迟。 |
| 已搁置 | | 客户端已发出升级批次的信号，但在批次监视服务重试`n`次后，批次升级已停止。 |

### “暂存”对于批处理是什么意思？

当批次处于“暂存”状态时，这意味着已成功发出升级信号，并且正在将数据暂存到下游以供使用。

### 当批次为“正在重试”时，这意味着什么？

当批次处于“正在重试”状态时，这意味着由于间歇性问题，批次的数据摄取已暂时停止。 发生这种情况时，无需客户干预。

### 当批处理“已停止”时，这意味着什么？

当批次处于“已停止”状态时，这意味着[!DNL Data Ingestion Services]在摄取批次时遇到困难，并且所有重试都已耗尽。

### 如果批次仍处于“正在加载”状态，这意味着什么？

当批次处于“正在加载”状态时，这意味着尚未调用CompleteBatch API来提升该批次。

### 是否可以通过某种方式了解是否已成功摄取批次？

是，当批状态为“有效”时，即表示已成功引入批。 要了解批次的状态，请按照[early](#how-is-batch-ingestion-monitored)中详述的步骤操作。

### 批次失败后会发生什么情况？ {#what-if-a-batch-fails}

当批次失败时，进程将停止并返回`Failure`状态。 可以在有效负荷的`errors`部分中识别失败的原因。 错误示例如下所示：

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

### 应如何删除批次？

应使用下面提供的任一方法删除批次，而不是直接从[!DNL Catalog]中删除：

1. 如果批次正在进行，则应中止该批次。
2. 如果成功掌握了批次，则应还原批次。

### 提供了哪些批次级别的量度？

以下批次级别量度适用于处于活动/成功状态的批次：

| 量度 | 描述 |
| ------ | ----------- |
| inputByteSize | 要处理[!DNL Data Ingestion Services]的暂存字节总数。 |
| inputRecordSize | 要处理[!DNL Data Ingestion Services]的暂存行总数。 |
| outputByteSize | [!DNL Data Ingestion Services]输出到[!DNL Data Lake]的总字节数。 |
| outputRecordSize | [!DNL Data Ingestion Services]输出到[!DNL Data Lake]的总行数。 |
| partitionCount | 写入到[!DNL Data Lake]中的分区总数。 |

### 为什么某些批次中没有可用的量度？

量度可能在您的批次中不可用可能有两个原因：

1. 该批次从未成功变为“活动/成功”状态。
2. 批次使用旧版促销路径（如CSV摄取）进行促销。

### 不同的状态代码表示什么？

| 状态代码 | 描述 |
| ----------- | ----------- |
| 106 | 数据集文件为空。 |
| 118 | CSV文件包含一个空标头行。 |
| 200 | 该批次已被接受处理，并将转换为最终状态，如“活动”或“失败”。 提交后，可以使用`GetBatch`终结点监视批处理。 |
| 400 | 错误请求。 如果批次中存在缺失或重叠的块，则返回。 |

`[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files`
