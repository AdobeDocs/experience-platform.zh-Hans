---
keywords: Experience Platform；主页；热门主题；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis源连接器概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Amazon Kinesis连接到Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 连接器

Adobe Experience Platform为云提供程序(如AWS、[!DNL Google Cloud Platform]和[!DNL Azure])提供本机连接。 您可以将数据从这些系统导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、设置格式或上载。 摄取的数据可以格式为XDM JSON、XDM Parquet或分隔。 流程的每个步骤都会集成到源工作流中。 [!DNL Platform] 允许您实时导入 [!DNL Amazon Kinesis] 数据。

## 先决条件

以下部分提供了在创建[!DNL Kinesis]源连接之前需要先设置的先决条件的详细信息。

### 设置访问策略

[!DNL Kinesis]流需要以下权限才能创建源连接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

这些权限通过[!DNL Kinesis]控制台进行排列，并在您输入凭据并选择数据流后由Platform检查。

以下示例显示创建[!DNL Kinesis]源连接所需的最低访问权限。

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
| `kinesis:GetRecords` | 从特定偏移或共享ID获取记录所需的操作。 |
| `kinesis:DescribeStream` | 一种操作，可返回与包括共享映射在内的流相关的信息，生成共享ID时需要该共享映射。 |
| `kinesis:ListStreams` | 列出可从UI中选择的可用流时需要执行的操作。 |

有关控制[!DNL Kinesis]数据流访问的更多信息，请参阅以下[[!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 配置迭代器类型

[!DNL Kinesis] 支持以下迭代器类型，以允许您指定数据的读取顺序：

| 迭代器类型 | 描述 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 从由特定序列号标识的位置开始读取数据。 |
| `AFTER_SEQUENCE_NUMBER` | 在由特定序列号标识的位置之后读取数据。 |
| `AT_TIMESTAMP` | 从由特定时间戳标识的位置开始读取数据。 |
| `TRIM_HORIZON` | 从最早的数据记录开始读取数据。 |
| `LATEST` | 从最近的数据记录开始读取数据。 |

[!DNL Kinesis] UI源当前仅支持`TRIM_HORIZON`，而API同时支持`TRIM_HORIZON`和`LATEST`作为获取数据的模式。 Platform用于[!DNL Kinesis]源的默认迭代器值为`TRIM_HORIZON`。

有关迭代器类型的更多信息，请参阅以下[[!DNL Kinesis] document](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 将[!DNL Amazon Kinesis]连接到[!DNL Platform]

以下文档提供了有关如何使用API或用户界面将[!DNL Amazon Kinesis]连接到[!DNL Platform]的信息：

### 使用API

- [使用流量服务API创建Amazon Kinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Amazon Kinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
