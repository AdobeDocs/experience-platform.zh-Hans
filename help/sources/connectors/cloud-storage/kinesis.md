---
title: Amazon Kinesis源连接器概述
description: 了解如何使用API或用户界面将Amazon Kinesis连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] 源

>[!IMPORTANT]
>
>此 [!DNL Amazon Kinesis] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

Adobe Experience Platform为云提供商(如AWS)提供本机连接， [!DNL Google Cloud Platform]、和 [!DNL Azure]. 您可以将来自这些系统的数据导入 [!DNL Platform].

云存储源可以将您自己的数据导入 [!DNL Platform] 无需下载、格式化或上传。 引入的数据可以格式化为XDM JSON、XDM Parquet或分隔。 该过程的每个步骤都集成到源工作流中。 [!DNL Platform] 允许您从以下位置引入数据 [!DNL Amazon Kinesis] 实时。

>[!NOTE]
>
>的缩放因子 [!DNL Kinesis] 如果您需要摄取大量数据，则必须增加。 目前，您可以从 [!DNL Kinesis] account到Platform的记录数是每秒4000条。 要扩展并摄取更大数量的数据，请联系您的Adobe代表。

## 先决条件

以下部分提供了在创建之前所需的先决条件设置的详细信息 [!DNL Kinesis] 源连接。

### 设置访问策略

A [!DNL Kinesis] 流需要以下权限才能创建源连接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

这些权限是通过 [!DNL Kinesis] 控制台，并在输入凭据并选择数据流后由Platform检查。

下面的示例显示了创建所需的最低访问权限 [!DNL Kinesis] 源连接。

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

有关控制对的访问权限的更多信息 [!DNL Kinesis] 数据流，请参阅以下内容 [[!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### 配置迭代器类型

[!DNL Kinesis] 支持以下迭代器类型，以便您指定读取数据的顺序：

| 迭代器类型 | 描述 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 从由特定序列号标识的位置开始读取数据。 |
| `AFTER_SEQUENCE_NUMBER` | 从特定序列号标识的位置之后开始读取数据。 |
| `AT_TIMESTAMP` | 从由特定时间戳标识的位置开始读取数据。 |
| `TRIM_HORIZON` | 从最早的数据记录开始读取数据。 |
| `LATEST` | 从最近的数据记录开始读取数据。 |

A [!DNL Kinesis] UI源当前仅支持 `TRIM_HORIZON`，而API同时支持这两者 `TRIM_HORIZON` 和 `LATEST` 作为获取数据的模式。 Platform使用的默认迭代器值 [!DNL Kinesis] 源是 `TRIM_HORIZON`.

有关迭代器类型的详细信息，请参阅以下内容 [[!DNL Kinesis] 文档](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## 连接 [!DNL Amazon Kinesis] 到 [!DNL Platform]

以下文档提供了有关如何连接的信息 [!DNL Amazon Kinesis] 到 [!DNL Platform] 使用API或用户界面：

### 使用API

- [使用流服务API创建Amazon Kinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用流服务API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Amazon Kinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
