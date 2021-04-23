---
keywords: Experience Platform；主页；热门主题；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Amazon Kinesis Source Connector概述
topic-legacy: overview
description: 了解如何使用API或用户界面将Amazon Kinesis连接到Adobe Experience Platform。
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# [!DNL Amazon Kinesis] 连接器

Adobe Experience Platform为AWS、[!DNL Google Cloud Platform]和[!DNL Azure]等云提供商提供本机连接。 您可以将这些系统中的数据导入[!DNL Platform]。

云存储源可以将您自己的数据导入[!DNL Platform]，而无需下载、格式化或上传。 收录的数据可以格式化为XDM JSON、XDM Perface或分隔。 流程的每个步骤都集成到源工作流中。 [!DNL Platform] 让您能够实时导入 [!DNL Amazon Kinesis] 数据。

## IP地址允许列表

在使用源连接器之前，必须向允许列表添加IP地址列表。 如果无法将您的区域特定IP地址添加到允许列表，在使用源时可能会导致错误或性能不佳。 有关详细信息，请参阅[ IP地址允许列表](../../ip-address-allow-list.md)页。

## 先决条件

以下部分提供了在创建[!DNL Kinesis]源连接之前所需的入门项目设置的详细信息。

### 设置访问策略

[!DNL Kinesis]流需要以下权限才能创建源连接：

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

这些权限通过[!DNL Kinesis]控制台进行排列，在您输入凭据并选择数据流后，平台会对其进行检查。

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
| `kinesis:DescribeStream` | 返回有关包括共享映射的流的信息的操作，生成共享ID时需要该映射。 |
| `kinesis:ListStreams` | 列表可从UI中选择的可用流所需的操作。 |

有关控制[!DNL Kinesis]数据流访问的详细信息，请参阅以下[[!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

### 配置迭代器类型

[!DNL Kinesis] 支持以下迭代器类型，以便指定数据的读取顺序：

| 迭代器类型 | 描述 |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | 从由特定序列号标识的位置开始读取数据。 |
| `AFTER_SEQUENCE_NUMBER` | 在由特定序列号标识的位置之后读取数据。 |
| `AT_TIMESTAMP` | 从由特定时间戳标识的位置开始读取数据。 |
| `TRIM_HORIZON` | 从最旧的数据记录开始读取数据。 |
| `LATEST` | 从最近的数据记录开始读取数据。 |

[!DNL Kinesis] UI源当前仅支持`TRIM_HORIZON`，而API支持`TRIM_HORIZON`和`LATEST`作为获取数据的模式。 平台用于[!DNL Kinesis]源的默认迭代器值为`TRIM_HORIZON`。

有关迭代器类型的详细信息，请参阅以下[[!DNL Kinesis] 文档](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax)。

## 将[!DNL Amazon Kinesis]连接到[!DNL Platform]

以下文档提供了如何使用API或用户界面将[!DNL Amazon Kinesis]连接到[!DNL Platform]的信息：

### 使用API

- [使用Flow Service API创建Amazon Kinesis源连接](../../tutorials/api/create/cloud-storage/kinesis.md)
- [使用Flow Service API收集流数据](../../tutorials/api/collect/streaming.md)

### 使用UI

- [在UI中创建Amazon Kinesis源连接](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [在UI中为云存储连接配置数据流](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
