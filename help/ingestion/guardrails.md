---
keywords: Experience Platform；故障诊断；护栏；指南；
title: 数据引入的护栏
description: 本文档提供了有关Adobe Experience Platform中数据摄取防护的指南
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 008537dffff4cc428de9070964446f4e7ebf039f
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# 数据引入的护栏

护栏是阈值，可为数据和系统使用、性能优化以及避免Adobe Experience Platform中的错误或意外结果提供指导。 护栏可指您对与许可权利相关的数据和处理的使用或使用。

本文档提供了有关Adobe Experience Platform中数据摄取防护的指南。

## 批量摄取的护栏

下表概述了在使用时应考虑的护栏 [批量摄取API](./batch-ingestion/overview.md) 或源：

| 摄取类型 | 准则 | 注释 |
| --- | --- | --- |
| 使用批量摄取API进行数据湖摄取 | <ul><li>您可以使用批量摄取API，每小时向Data Lake摄取多达20 GB的数据。</li><li>每批次的最大文件数为1500。</li><li>最大批次大小为100 GB。</li><li>每行的属性或字段的最大数量为10000。</li><li>每个用户每分钟的最大批次数为138。</li></ul> |
| 使用批处理源摄取数据湖 | <ul><li>您可以使用批量摄取源（例如）每小时向数据湖摄取多达200 GB的数据 [!DNL Azure Blob]， [!DNL Amazon S3]、和 [!DNL SFTP].</li><li>批次大小应介于256 MB和100 GB之间。</li><li>每批次的最大文件数为1500。</li></ul> | 请参阅 [源概述](../sources/home.md) 对于可用于数据摄取的源目录。 |
| 将批量摄取到配置文件 | <ul><li>记录类的最大大小为100 KB (soft)。</li><li>ExperienceEvent类的最大大小为10 KB (soft)。</li><li>单个记录的最大大小为1 MB。</li></ul> |
| 每天摄取的配置文件或ExperienceEvent批次数 | **每天摄取的Profile或ExperienceEvent批次的最大数量为90。** 这意味着每天摄取的Profile和ExperienceEvent批次总数不能超过90。 摄取其他批次将影响系统性能。 | 这是一个软限制。 可以超出软限制，但是，软限制提供了系统性能推荐准则。 |

## 流式摄取的护栏

阅读 [流式摄取概述](./streaming-ingestion/overview.md) 以了解有关流式摄取的护栏的信息。

## 流源的护栏

下表概述了使用流源时要考虑的防护：

| 摄取类型 | 准则 | 注释 |
| --- | --- | --- |
| 流源 | <ul><li>最大记录大小为1 MB，建议的大小为10 KB。</li><li>在创建新的源连接时，流源支持每秒钟有4000到5000个请求。 **注意**：流式处理数据完全到数据湖最多可能需要30分钟。</li><li>您可以每秒处理4000到5000个到数据湖的请求。 **注意**：流式处理数据完全到数据湖最多可能需要30分钟。</li></ul> | 流源，如 [!DNL Kafka]， [!DNL Azure Event Hubs]、和 [!DNL Amazon Kinesis] 请勿使用 [!DNL Data Collection Core Service] (DCCS)路由，可以具有不同的吞吐量限制。 请参阅 [源概述](../sources/home.md) 对于可用于数据摄取的源目录。 |

## 后续步骤

有关Experience Platform中数据和处理护栏的更多信息，请参阅以下文档：

* [Real-time Customer Profile数据的护栏](../profile/guardrails.md)
* [Identity Service数据的护栏](../identity-service/guardrails.md)
