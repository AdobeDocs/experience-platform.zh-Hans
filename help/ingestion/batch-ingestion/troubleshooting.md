---
keywords: Experience Platform；主页；热门主题；摄取的数据；疑难解答；常见问题；摄取；批处理摄取；批处理摄取；
solution: Experience Platform
title: 批量摄取疑难解答指南
topic-legacy: troubleshooting
description: 本文档将帮助回答有关Adobe Experience Platform Batch Data Ingestion API的常见问题。
exl-id: 0a750d7e-a4ee-4a79-a697-b4b732478b2b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 1%

---

# 批量摄取疑难解答指南

本文档将帮助回答有关Adobe Experience Platform [!DNL Batch Data Ingestion] API的常见问题。

## 批处理API调用

### 在从CompleteBatch API接收HTTP 200 OK后，批是否立即处于活动状态？

来自API的`200 OK`响应表示批已接受处理 — 在它过渡到其最终状态（如“活动”或“失败”）之前，它不处于活动状态。

### 在CompleteBatch API调用失败后重试是否安全？

是 — 可以安全地重试API调用。 尽管失败，操作仍有可能实际成功，批也成功接受。 但是，在API失败时，客户端应具有重试机制，并且实际上鼓励客户端重试。 如果操作实际成功，则API将返回成功，即使重试后也是如此。

### 何时应使用大文件上传API?

使用“大文件上传API”时建议的文件大小为256 MB或更大。 有关如何使用大文件上传API的详细信息，请在[此处](./api-overview.md#ingest-large-parquet-files)找到。

### 为什么大文件完成API调用失败？

如果发现大文件的块重叠或丢失，服务器会使用HTTP 400错误请求做出响应。 之所以会出现这种情况，是因为上载重叠的块是可能的，因为在文件块拼接在一起时，范围验证会在文件完成时完成。

## 摄取支持

### 支持哪些收录格式？

目前，支持Parke和JSON。 旧版支持CSV — 而将将数据提升为主控检查并完成初步检查，不支持转换、分区或行验证等现代功能。

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

### 为什么上载的数据不显示在数据集中？

要使数据显示在数据集中，必须将批标记为完成。 您要收录的所有文件都必须在将批标记为完成之前上传。 将批标记为完成的示例如下所示：

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 多行JSON如何摄取？

要收录多行JSON，需要在创建批时设置`isMultiLineJson`标志。 下面可以看到此示例：

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

### 对数据执行了哪些类型的验证？

对数据执行的验证有三个级别：

- 模式 — 批处理摄取可确保所摄取数据的模式与数据集的模式相匹配。
- 数据类型 — 批处理摄取确保摄取的每个字段的类型与数据集模式中定义的类型相匹配。
- 约束 — 批处理摄取可确保约束（如“必需”、“枚举”和“格式”）在模式定义中正确定义。

### 如何替换已摄取的批？

已摄取的批可以使用“批重放”功能替换。 有关批重播的详细信息，请在[此处](./api-overview.md#replay-a-batch)找到。

### 如何监视批量摄取？

一旦向批发出批次升级信号，便可以通过以下请求监控批次摄取进度：

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

通过此请求，您将得到类似以下内容的响应：

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

### 什么是可能的批处理状态？

批处理在其生命周期中可以执行以下状态：

| 状态 | 写入主控的数据 | 描述 |
| ------ | ---------------------- | ----------- |
| 已放弃 |  | 客户端未能在预期时间范围内完成批处理。 |
| 中止 |  | 客户端已通过[!DNL Batch Data Ingestion] API显式调用指定批的中止操作。 一旦某个批处于“已加载”状态，该批就无法中止。 |
| 活动/成功 | x | 批已成功从阶段提升到主控，现在可用于下游消耗。 **注意：“** 活动”和“成功”可互换使用。 |
| 已存档 |  | 批已存档为冷存储。 |
| 失败/失败 |  | 由错误配置和/或错误数据导致的终端状态。 将记录一个可操作的错误以及该批，以使客户端能够更正并重新提交数据。 **注意：“** 失败”和“失败”可互换使用。 |
| 非活动 | x | 批已成功提升，但已还原或已过期。 该批将不再可用于下游消耗，但基础数据将保持主控，直到其被保留、存档或以其他方式删除。 |
| 正在加载 |  | 客户端当前正在为批处理编写数据。 此时，批&#x200B;**未**&#x200B;准备升级。 |
| 已加载 |  | 客户端已完成为批处理写入数据。 批已准备好进行升级。 |
| 保留 |  | 数据已从主控中取出，并存放在Adobe Data Lake中指定的存档中。 |
| 暂存 |  | 客户端已成功发出批升级的信号，数据正在暂存以在下游消耗。 |
| 正在重试 |  | 客户端已向批发出提升的信号，但由于出错，批正在由批监视服务重试。 此状态可用于告诉客户端在获取数据时可能存在延迟。 |
| 停止 |  | 客户端已发出批升级的信号，但在批监视服务`n`重试后，批升级已停止。 |

### “暂存”对批意味着什么？

当批处于“暂存”中时，它表示已成功发出该批的升级信号，并且正在将数据暂存以在下游消耗。

### 当批为“重试”时，它表示什么？

当批处于“重试”状态时，这意味着由于间歇性问题，该批的数据摄取已暂时停止。 当发生这种情况时，不需要客户干预。

### 当批为“停止”时，这意味着什么？

当批处于“停止”状态时，这意味着[!DNL Data Ingestion Services]在摄取该批时遇到困难，且所有重试已用尽。

### 如果批仍为“正在加载”，它意味着什么？

当批处于“正在加载”中时，这意味着尚未调用CompleteBatch API来提升该批。

### 是否有方法可确定批是否已成功摄取？

批状态为“活动”后，批便被成功摄取。 要了解批的状态，请按照详细步骤[之前的](#how-is-batch-ingestion-monitored)执行。

### 批处理失败后会出现什么情况？

当批处理失败时，可以在负载的`errors`部分中确定其失败的原因。 错误示例如下：

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

应使用以下任一方法删除批，而不是直接从[!DNL Catalog]中删除：

1. 如果批处理中，则应中止该批处理。
2. 如果批已成功掌握，应还原该批。

### 提供哪些批量度？

在“活动/成功”状态中，批可使用以下批级量度：

| 量度 | 描述 |
| ------ | ----------- |
| inputByteSize | 要处理的[!DNL Data Ingestion Services]所暂存的字节总数。 |
| inputRecordSize | 要处理的[!DNL Data Ingestion Services]的已暂存行总数。 |
| outputByteSize | 由[!DNL Data Ingestion Services]输出到[!DNL Data Lake]的字节总数。 |
| outputRecordSize | 由[!DNL Data Ingestion Services]输出到[!DNL Data Lake]的行总数。 |
| partitionCount | 写入[!DNL Data Lake]的分区总数。 |

### 为什么某些批中不提供量度？

量度在您的批中可能不可用有两个原因：

1. 批从未成功进入活动/成功状态。
2. 批已使用旧版提升路径（如CSV摄取）进行提升。

### 不同的状态代码意味着什么？

| 状态代码 | 描述 |
| ----------- | ----------- |
| 106 | 数据集文件为空。 |
| 118 | CSV文件包含空标题行。 |
| 200 | 批已接受处理，并将过渡到最终状态，如“活动”或“失败”。 提交后，可以使用`GetBatch`端点监视批。 |
| 400 | 错误请求. 如果批处理中缺少块或重叠块，则返回。 |

[large-file-upload]: batch_data_ingestion_developer_guide.md#how-to-ingest-large-parquet-files
