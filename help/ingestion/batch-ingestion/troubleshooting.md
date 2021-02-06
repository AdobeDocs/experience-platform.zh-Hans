---
keywords: Experience Platform；主页；热门主题；摄取的数据；疑难解答；常见问题解答；摄取；批处理摄取；批处理摄取；
solution: Experience Platform
title: 批量摄取疑难解答指南
topic: troubleshooting
description: '本文档将帮助回答有关Adobe Experience Platform批量数据摄取API的常见问题。 '
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---


# 批量摄取疑难解答指南

本文档将帮助回答有关Adobe Experience Platform[!DNL Batch Data Ingestion] API的常见问题。

## 批处理API调用

### 从CompleteBatch API接收HTTP 200 OK后，批是否立即处于活动状态？

来自API的`200 OK`响应意味着批处理已被接受——在它过渡到其最终状态（如“活动”或“失败”）之前，它不处于活动状态。

### CompleteBatch API调用失败后，是否可以重试该调用？

是——可以安全地重试API调用。 尽管失败，操作仍可能实际成功，批也可能成功接受。 但是，在API失败时，客户端应具有重试机制，实际上，会鼓励客户端重试。 如果操作实际成功，则API将返回成功，即使重试后也是如此。

### 何时应使用大文件上传API?

使用“大文件上传API”的建议文件大小为256 MB或更大。 有关如何使用大文件上传API的更多信息，请在[此处](./api-overview.md#ingest-large-parquet-files)找到。

### 为什么大文件完整API调用失败？

如果发现大文件的块重叠或缺失，则服务器会使用HTTP 400错误请求做出响应。 之所以会出现这种情况，是因为可以上传重叠的块，因为在文件完成时，当文件块拼接在一起时，会执行范围验证。

## 摄取支持

### 支持哪些收录格式？

目前，支持Parke和JSON。 旧版支持CSV —— 虽然数据将提升为主控，并将进行初步检查，但不支持转换、分区或行验证等现代功能。

### 应在何处指定批处理输入格式？

应在有效负荷内的批量创建时指定输入格式。 有关如何指定批处理输入格式的示例如下所示：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
    }'
```

### 为什么上传的数据不显示在数据集中？

要使数据显示在数据集中，必须将批标记为完成。 必须先上传要收录的所有文件，然后才能将批标记为完成。 将批标记为完成的示例如下所示：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 多行JSON如何摄取？

要获取多行JSON，需要在创建批时设置`isMultiLineJson`标志。 以下是此示例：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json",
                "isMultiLineJson": true
           }
      }'
```

### JSON行（单行JSON）与多行JSON之间有何差异？

对于JSON行，每行有一个JSON对象。 例如：

```json
{"string":"string1","int":1,"array":[1,2,3],"dict": {"key": "value1"}}
{"string":"string2","int":2,"array":[2,4,6],"dict": {"key": "value2"}}
{"string":"string3","int":3,"array":[3,6,9],"dict": {"key": "value3", "extra_key": "extra_value3"}}
```

对于多行JSON，一个对象可以占用多行，而所有对象都打包在JSON数组中。 例如：

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

### 是否支持CSV摄取？

CSV摄取仅支持简单模式。 目前，不支持以CSV格式接收分层数据。

要获取所有数据获取功能，需要使用JSON或Parke格式。

### 对数据执行哪些类型的验证？

对数据执行的验证有三个级别：

- 模式-批处理摄取确保所摄取数据的模式与数据集的模式相匹配。
- 数据类型——批处理摄取确保摄取的每个字段的类型与数据集模式中定义的类型相匹配。
- 约束——批处理摄取确保约束（如“必需”、“枚举”和“格式”）在模式定义中正确定义。

### 如何替换已摄取的批？

已摄取的批可以使用“批重播”功能替换。 有关“批重播”的详细信息，请在[此处](./api-overview.md#replay-a-batch)找到。

### 如何监控批量摄取？

一旦向批发出批次升级信号，便可通过以下请求监控批次获取进度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

通过此请求，您将收到类似以下内容的响应：

```http
200 OK
```

```json
{
    "{BATCH_ID}":{
        "imsOrg":"{IMS_ORG}",
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

### 哪些可能的批处理状态？

批处理在其生命周期中可以经历以下状态：

| 状态 | 写入主控的数据 | 描述 |
| ------ | ---------------------- | ----------- |
| 已放弃 |  | 客户端未能在预期时间范围内完成批处理。 |
| 已中止 |  | 客户端已通过[!DNL Batch Data Ingestion] API显式调用指定批次的中止操作。 一旦批处理处于“已加载”状态，则该批处理将无法中止。 |
| 活动／成功 | x | 批已成功从阶段提升到主控，现在可用于下游消耗。 **注意：“** 活动”和“成功”可互换使用。 |
| 已存档 |  | 批已存档为冷存储。 |
| 失败／失败 |  | 由错误配置和／或错误数据导致的终端状态。 将记录可操作的错误以及批，以使客户端能够更正并重新提交数据。 **注意：“** 失败”和“失败”可互换使用。 |
| 非活动 | x | 批已成功提升，但已还原或已过期。 批处理将不再可用于下游消耗，但基础数据将保持主控，直到其被保留、存档或删除。 |
| 正在加载 |  | 客户端当前正在为批处理编写数据。 此时，批处于&#x200B;**未**&#x200B;状态，可以升级。 |
| 已加载 |  | 客户端已完成为批处理写入数据。 批已准备好升级。 |
| 保留 |  | 数据已从主控中取出，并存放在Adobe数据湖的指定存档中。 |
| 暂存 |  | 客户端已成功发出批升级信号，数据正在暂存以在下游消耗。 |
| 正在重试 |  | 客户端已发出批次升级的信号，但由于出错，批次正在由批次监视服务重试。 此状态可用于告知客户端在摄取数据时可能存在延迟。 |
| 停止 |  | 客户端已发出批次升级的信号，但在批次监控服务`n`重试后，批次升级已停止。 |

### “暂存”对于批意味着什么？

当批处于“暂存”时，这意味着已成功发出批的升级信号，并且数据正在暂存以供下游消耗。

### 批“正在重试”时，它表示什么？

当批处于“重试”状态时，这意味着由于间歇性问题，该批的数据摄取已暂时停止。 当发生这种情况时，无需客户干预。

### 当批“停止”时，它意味着什么？

当批处于“停止”状态时，这意味着[!DNL Data Ingestion Services]在接收该批时遇到困难，并且所有重试都已用尽。

### 如果批仍“正在加载”，它意味着什么？

当批处于“正在加载”中时，这意味着尚未调用CompleteBatch API来提升批。

### 是否有方法可确定批次是否成功摄取？

一旦批状态为“活动”，批便被成功摄取。 要了解批的状态，请按照详细的[早期](#how-is-batch-ingestion-monitored)步骤操作。

### 批处理失败后会发生什么情况？

当批处理失败时，其失败的原因可以在有效负荷的`errors`部分中确定。 错误示例如下：

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

更正错误后，可以重新上传批。

## 批支持

### 如何删除批？

应使用以下任一方法删除批，而不是直接从[!DNL Catalog]删除：

1. 如果批处理正在进行，则应中止该批处理。
2. 如果批已成功掌握，则应还原该批。

### 提供哪些批处理级别指标？

在“活动／成功”状态中，批可使用以下批级度量：

| 量度 | 描述 |
| ------ | ----------- |
| inputByteSize | [!DNL Data Ingestion Services]要处理的分段字节总数。 |
| inputRecordSize | 为[!DNL Data Ingestion Services]要处理的暂存行总数。 |
| outputByteSize | [!DNL Data Ingestion Services]输出到[!DNL Data Lake]的字节总数。 |
| outputRecordSize | 由[!DNL Data Ingestion Services]输出到[!DNL Data Lake]的行总数。 |
| partitionCount | 写入[!DNL Data Lake]的分区总数。 |

### 为什么某些批量不提供指标？

量度可能无法在您的批中使用有两个原因：

1. 批从未成功进入活动／成功状态。
2. 批已使用旧版提升路径（如CSV摄取）进行提升。

### 不同的状态代码意味着什么？

| 状态代码 | 描述 |
| ----------- | ----------- |
| 106 | 数据集文件为空。 |
| 118 | CSV文件包含空标题行。 |
| 200 | 批已接受处理，并将过渡到最终状态，如“活动”或“失败”。 提交后，可以使用`GetBatch`端点监视批处理。 |
| 400 | 错误请求. 如果批处理中缺少块或重叠块，则返回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
