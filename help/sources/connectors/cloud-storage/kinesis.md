---
keywords: Experience Platform；主页；热门主题；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis源连接器概述
description: 了解如何使用API或用户界面将Amazon Kinesis连接到Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 连接器

Adobe Experience Platform为AWS等云提供商提供本机连接， [!DNL Google Cloud Platform]和 [!DNL Azure]. 您可以将这些系统中的数据导入 [!DNL Platform].

云存储源可以将您自己的数据引入 [!DNL Platform] 无需下载、设置格式或上传。 摄取的数据可以格式为XDM JSON、XDM Parquet或分隔。 流程的每个步骤都会集成到源工作流中。 [!DNL Platform] 允许您从 [!DNL Amazon Kinesis] 实时。

>[!NOTE]
>
>的比例因子 [!DNL Kinesis] 如果需要摄取大量数据，则必须增加。 目前，您可以从 [!DNL Kinesis] Platform帐户每秒有4000条记录。 要放大并摄取更大量的数据，请联系您的Adobe代表。

## 先决条件

以下部分提供了在创建 [!DNL Kinesis] 源连接。

### 设置访问策略

A [!DNL Kinesis] 流需要以下权限才能创建源连接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

这些权限通过 [!DNL Kinesis] 控制台中，并且在您输入凭据并选择您的数据流后，将会由Platform检查。

以下示例显示创建 [!DNL Kinesis] 源连接。

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

有关控制访问的详细信息 [!DNL Kinesis] 数据流，请参阅以下内容 [[!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### 配置迭代器类型

[!DNL Kinesis] 支持以下迭代器类型，以允许您指定数据的读取顺序：

| 迭代器类型 | 描述 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 从由特定序列号标识的位置开始读取数据。 |
| `AFTER_SEQUENCE_NUMBER` | 在由特定序列号标识的位置之后读取数据。 |
| `AT_TIMESTAMP` | 从由特定时间戳标识的位置开始读取数据。 |
| `TRIM_HORIZON` | 从最早的数据记录开始读取数据。 |
| `LATEST` | 从最近的数据记录开始读取数据。 |

A [!DNL Kinesis] 当前仅支持UI源 `TRIM_HORIZON`，而API同时支持 `TRIM_HORIZON` 和 `LATEST` 作为获取数据的模式。 Platform用于 [!DNL Kinesis] 源 `TRIM_HORIZON`.

有关迭代器类型的更多信息，请参阅以下内容 [[!DNL Kinesis] 文档](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## 连接 [!DNL Amazon Kinesis] to [!DNL Platform]

以下文档提供了有关如何连接的信息 [!DNL Amazon Kinesis] to [!DNL Platform] 使用API或用户界面：

### 使用API

- [使用流量服务API创建Amazon Kinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Amazon Kinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
