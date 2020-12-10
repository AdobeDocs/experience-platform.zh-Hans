---
product: experience-platform
audience: user
user-guide-title: Adobe Experience Platform 数据提取帮助
breadcrumb-title: Data Ingestion 指南
user-guide-description: 通过批处理或流式获取将数据引入平台。
translation-type: tm+mt
source-git-commit: cfdaf72b7f4bf190877006ccd4cc6a7fd014adc2
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 20%

---


# Adobe Experience Platform Data Ingestion {#ingestion}

- [数据摄取概述](home.md)
- 流摄取 {#streaming}
   - [概述](streaming-ingestion/overview.md)
   - [卡夫卡连接器](streaming-ingestion/kafka.md)
   - [故障诊断](streaming-ingestion/troubleshooting.md)
- 批量摄取{#batch}
   - [概述](batch-ingestion/overview.md)
   - [批处理摄取API](batch-ingestion/api-overview.md)
   - [部分批摄取](batch-ingestion/partial.md)
   - [故障诊断](batch-ingestion/troubleshooting.md)
- 教程 {#tutorials}
   - [将CSV文件映射到XDM](tutorials/map-a-csv-file.md)
   - [使用UI摄取批数据](tutorials/ingest-batch-data.md)
   - [创建经过身份验证的流连接](tutorials/create-authenticated-streaming-connection.md)
   - [创建流连接(API)](tutorials/create-streaming-connection.md)
   - [创建流连接(UI)](tutorials/create-streaming-connection-ui.md)
   - [流记录数据](tutorials/streaming-record-data.md)
   - [流式时间序列数据](tutorials/streaming-time-series-data.md)
   - [流化多条消息](tutorials/streaming-multiple-messages.md)
- 数据摄取质量和监控{#quality}
   - [概述](quality/overview.md)
   - [监控数据获取](quality/monitor-data-ingestion.md)
   - [检索错误诊断](quality/error-diagnostics.md)
   - [检索失败的批](quality/retrieve-failed-batches.md)
   - [流式摄取验证](quality/streaming-validation.md)
   - [订阅数据获取事件](quality/subscribe-events.md)
- [源连接器](source-connectors.md)
- [API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [平台发行说明](https://www.adobe.com/go/platform-release-notes-en)