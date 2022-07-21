---
keywords: Experience Platform；故障诊断；护栏；准则；
title: 数据摄取的防护
description: 本文档提供了有关在Adobe Experience Platform中摄取数据的防护的指导
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 4fd26078017ae13e22ebb02f98335094c8e0581b
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# 数据摄取的防护

护栏是指为Adobe Experience Platform中的数据和系统使用、性能优化以及避免错误或意外结果提供指导的阈值。 护栏可以是指您对与授权许可相关的数据和处理的使用情况或使用情况。

本文档提供了有关在Adobe Experience Platform中摄取数据的防护的指导。

## 批量摄取的防护

下表概述了在使用 [批量摄取API](./batch-ingestion/overview.md) 或来源：

| 摄取类型 | 准则 | 注释 |
| --- | --- | --- |
| 使用批量摄取API的数据湖摄取 | <ul><li>使用批量摄取API，您每小时可以摄取多达20 GB的数据到数据湖。</li><li>每批文件的最大数量为1500。</li><li>最大批处理大小为100 GB。</li><li>每行的属性或字段的最大数为10000。</li><li>每用户每分钟的批次数上限为138个。</li></ul> |
| 使用批处理源的数据湖摄取 | <ul><li>使用批量摄取源(例如， [!DNL Azure Blob], [!DNL Amazon S3]和 [!DNL SFTP].</li><li>批处理大小应介于256 MB和100 GB之间。</li><li>每批文件的最大数量为1500。</li></ul> | 请参阅 [源概述](../sources/home.md) 用于数据摄取的源目录。 |
| 批量摄取到配置文件 | <ul><li>您每小时可摄取多达120 GB的数据。</li><li>记录类的最大大小为100 KB（软）。</li><li>ExperienceEvent类的最大大小为10 KB（软）。</li><li>单个记录的最大大小为1 MB。</li></ul> |

## 用于流式引入的防护

下表概述了在使用 [流式引入API](./streaming-ingestion/overview.md) 或流源：

| 摄取类型 | 准则 | 注释 |
| --- | --- | --- |
| 流式摄取 | <ul><li>最大记录大小为1 MB，建议大小为10 KB。</li><li>您可以在一分钟内每秒处理20000个向用户档案发出的请求。</li><li>在15分钟内，您每秒最多可以处理20000个数据湖请求。</li></ul> | 如果您需要提高数据吞吐量，请使用批量摄取API。 |
| 流源 | <ul><li>最大记录大小为1 MB，建议大小为10 KB。</li><li>在创建新的源连接时，流源每秒支持4000到5000个请求。 **注意**:流式数据最多可能需要30分钟才能完全处理到数据湖。</li><li>您每秒可以处理4000到5000个数据湖请求。 **注意**:流式数据最多可能需要30分钟才能完全处理到数据湖。</li></ul> | 流源，如 [!DNL Kafka], [!DNL Azure Event Hubs]和 [!DNL Amazon Kinesis] 不使用 [!DNL Data Collection Core Service] (DCCS)路由，并且可以具有不同的吞吐量限制。 请参阅 [源概述](../sources/home.md) 用于数据摄取的源目录。 |

## 后续步骤

有关Experience Platform中数据和处理护栏的更多信息，请参阅以下文档：

* [实时客户资料数据的防护](../profile/guardrails.md)
* [Identity Service数据的防护](../identity-service/guardrails.md)
