---
audience: user
user-guide-title: Adobe Experience Platform 数据引入帮助
breadcrumb-title: Data Ingestion 指南
user-guide-description: 通过批次引入或流式处理引入将您的数据引入 Experience Platform。
feature: Data Ingestion
role: Developer
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 21%

---


# Adobe Experience Platform数据摄取 {#ingestion}

- [数据引入概述](home.md)
- 流式摄取 {#streaming}
   - [概述](streaming-ingestion/overview.md)
   - [Kafka连接器](streaming-ingestion/kafka.md)
   - [故障排除](streaming-ingestion/troubleshooting.md)
- 批量摄取{#batch}
   - [批量摄取API快速入门](batch-ingestion/getting-started.md)
   - [API概述](batch-ingestion/overview.md)
   - [API开发人员指南](batch-ingestion/api-overview.md)
   - [部分批次摄取](batch-ingestion/partial.md)
   - [故障排除](batch-ingestion/troubleshooting.md)
- 教程 {#tutorials}
   - 将CSV文件映射到XDM {#map-csv}
      - [概述](./tutorials/map-csv/overview.md)
      - [将CSV文件映射到现有架构](./tutorials/map-csv/existing-schema.md)
      - [使用人工智能生成的推荐映射CSV文件](./tutorials/map-csv/recommendations.md)
   - [使用UI引入批量数据](tutorials/ingest-batch-data.md)
   - [创建经过身份验证的流连接](tutorials/create-authenticated-streaming-connection.md)
   - [创建流连接(API)](tutorials/create-streaming-connection.md)
   - [创建流连接(UI)](tutorials/create-streaming-connection-ui.md)
   - [流记录数据](tutorials/streaming-record-data.md)
   - [流式处理时间序列数据](tutorials/streaming-time-series-data.md)
   - [流式传输多条消息](tutorials/streaming-multiple-messages.md)
- 数据质量和监控{#quality}
   - [概述](quality/overview.md)
   - [监测数据摄取](quality/monitor-data-ingestion.md)
   - [检索错误诊断](quality/error-diagnostics.md)
   - [检索失败的批次](quality/retrieve-failed-batches.md)
   - [流式摄取验证](quality/streaming-validation.md)
- [数据摄取的护栏](guardrails.md)
- [Source连接器](source-connectors.md)
- [批次摄取API引用](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [流式引入API引用](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience Platform 发行说明](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/release-notes/latest)
