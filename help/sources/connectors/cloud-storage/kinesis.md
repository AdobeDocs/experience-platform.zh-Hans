---
title: Amazon Kinesis Source连接器概述
description: 了解如何使用API或用户界面将Amazon Kinesis连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# [!DNL Amazon Kinesis]源

>[!IMPORTANT]
>
>- [!DNL Amazon Kinesis]源在源目录中可供已购买Real-Time CDP Ultimate的用户使用。
>
>- 在Amazon Web Services (AWS)上运行Adobe Experience Platform时，您现在可以使用[!DNL Amazon Kinesis]源。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。


Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将来自这些系统的数据导入[!DNL Experience Platform]。

云存储源可以将您自己的数据导入[!DNL Experience Platform]，而无需下载、格式化或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 [!DNL Experience Platform]允许您从[!DNL Amazon Kinesis]实时引入数据。

>[!NOTE]
>
>如果需要摄取大量数据，必须增加[!DNL Kinesis]的缩放因子。 目前，您可以从[!DNL Kinesis]帐户向Experience Platform引入的最大数据量为每秒4000条记录。 要扩展并摄取更大数量的数据，请联系您的Adobe代表。

## 先决条件

以下部分提供了在创建[!DNL Kinesis]源连接之前所需的先决条件设置的详细信息。

### 设置访问策略

[!DNL Kinesis]流需要以下权限才能创建源连接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

这些权限通过[!DNL Kinesis]控制台进行排列，并在输入凭据并选择数据流后由Experience Platform检查。

以下示例显示了创建[!DNL Kinesis]源连接所需的最低访问权限。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `kinesis:GetShardIterator` | 遍历记录所需的操作。 |
| `kinesis:GetRecords` | 从特定偏移或分片ID获取记录所需的操作。 |
| `kinesis:DescribeStream` | 一个操作，用于返回有关流的信息，包括生成分片ID所需的分片映射。 |
| `kinesis:ListStreams` | 列出可从UI中选择的可用流时需要执行的操作。 |

有关控制[!DNL Kinesis]数据流的访问权限的详细信息，请参阅以下[[!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 配置迭代器类型

[!DNL Kinesis]支持以下迭代器类型，允许您指定读取数据的顺序：

| 迭代器类型 | 描述 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 从由特定序列号标识的位置开始读取数据。 |
| `AFTER_SEQUENCE_NUMBER` | 从特定序列号标识的位置之后开始读取数据。 |
| `AT_TIMESTAMP` | 从由特定时间戳标识的位置开始读取数据。 |
| `TRIM_HORIZON` | 从最早的数据记录开始读取数据。 |
| `LATEST` | 从最近的数据记录开始读取数据。 |

[!DNL Kinesis] UI源当前仅支持`TRIM_HORIZON`，而API同时支持`TRIM_HORIZON`和`LATEST`作为获取数据的模式。 Experience Platform用于[!DNL Kinesis]源的默认迭代器值为`TRIM_HORIZON`。

有关迭代器类型的详细信息，请参阅以下[[!DNL Kinesis] 文档](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 将[!DNL Amazon Kinesis]连接到[!DNL Experience Platform]

>[!NOTE]
>
>创建或更新流数据流后，需要短暂暂停数据摄取5分钟，以防出现任何潜在的数据丢失或数据丢失情况。

以下文档提供了有关如何使用API或用户界面将[!DNL Amazon Kinesis]连接到[!DNL Experience Platform]的信息：

### 使用API

- [使用流服务API创建Amazon Kinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Amazon Kinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
