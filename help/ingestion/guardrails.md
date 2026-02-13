---
keywords: Experience Platform；故障排除；护栏；指南；
title: 数据引入的护栏
description: 了解Adobe Experience Platform中的数据摄取防护。
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: b5b975308d28ae82ea4d811652681215bc2cfbdb
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# 数据引入的护栏

>[!IMPORTANT]
>
>批量摄取和流式摄取的护栏通常在组织级别而非沙盒级别计算。 这意味着每个沙盒的数据使用情况绑定到与整个组织对应的许可证使用情况权利总数。 此外，开发沙盒中的数据使用限制为总配置文件的10%。 有关许可证使用授权的更多信息，请阅读[数据管理最佳实践指南](../landing/license-usage-and-guardrails/data-management-best-practices.md)。

护栏是阈值，可为数据和系统使用、性能优化以及避免Adobe Experience Platform中的错误或意外结果提供指导。 护栏可指您对与许可权利相关的数据和处理的使用或使用。

>[!IMPORTANT]
>
>除了此护栏页面外，还检查销售订单中的许可证授权和相应的[产品描述](https://helpx.adobe.com/cn/legal/product-descriptions.html)中的实际使用限制。

本文档提供了有关Adobe Experience Platform中数据摄取防护的指南。

## 批量摄取的护栏

下表概述了使用[批处理摄取API](./batch-ingestion/overview.md)或源时应考虑的护栏：

| 摄取类型 | 准则 | 注释 |
| --- | --- | --- |
| 使用批量摄取API进行数据湖摄取 | <ul><li>您可以使用批量摄取API，每小时向Data Lake摄取多达20 GB的数据。</li><li>每批次的最大文件数为1500。</li><li>最大批次大小为100 GB。</li><li>每行的属性或字段的最大数量为10000。</li><li>每个用户每分钟的最大批次数为2000。</li></ul> | |
| 使用批处理源摄取数据湖 | <ul><li>您可以使用批量摄取源（如[!DNL Azure Blob]、[!DNL Amazon S3]和[!DNL SFTP]）每小时最多可摄取200 GB的数据到数据湖。</li><li>批次大小应介于256 MB和100 GB之间。 这同时适用于未压缩数据和压缩数据。 在数据湖中解压缩压缩数据时，将应用这些限制。</li><li>每批次的最大文件数为1500。</li><li>文件或文件夹的最小大小为1字节。 无法摄取0字节大小的文件或文件夹。</li></ul> | 请阅读[源概述](../sources/home.md)，了解可用于数据摄取的源目录。 |
| 将批量摄取到配置文件 | <ul><li>记录类的最大大小为100 KB (hard)。</li><li>ExperienceEvent类的最大大小为10 KB (hard)。</li></ul> | |
| 每天摄取的配置文件或ExperienceEvent批次数 | **每个沙盒每天摄取的Profile或ExperienceEvent批次的最大数量为90。**&#x200B;这意味着每天摄取的Profile和ExperienceEvent批次总数不能超过90。 摄取其他批次将影响系统性能。 | 这是一个软限制。 可以超出软限制，但是，软限制提供了系统性能推荐准则。 此外，此护栏是基于&#x200B;**每个沙盒**，而不是基于每个组织。 |
| 加密的数据摄取 | 单个加密文件的最大支持大小为1 GB。 例如，虽然您可以在单个数据流运行中摄取2 GB或更多GB的数据，但数据流运行中的任何单个文件都不能超过1 GB。 | 摄取加密数据的过程可能需要比常规数据摄取更长的时间。 有关详细信息，请阅读[加密数据摄取API指南](../sources/tutorials/api/encrypt-data.md)。 |
| 更新插入批次摄取 | 摄取upsert批次的速度最多可为常规批次的10倍，因此，您应&#x200B;**将您的upsert批次保留在200万条记录以下**，以确保高效的运行时并避免阻止在沙盒中处理其他批次。 | 虽然您毫无疑问可以摄取超过200万条记录的批次，但摄取时间会由于小沙盒的限制而显着延长。 |

{style="table-layout:auto"}

## 流式摄取的护栏

有关流式摄取的护栏的信息，请阅读[流式摄取概述](./streaming-ingestion/overview.md)。

## 流源的护栏

下表概述了使用流源时要考虑的防护：

| 摄取类型 | 准则 | 注释 |
| --- | --- | --- |
| 流源 | <ul><li>最大记录大小为1 MB，建议的大小为10 KB。</li><li>在摄取到数据湖时，流媒体源支持每秒钟在4000到5000个请求之间。 除了现有的源连接外，这还适用于新创建的源连接。 **注意**：流式处理数据最多可能需要60分钟才能完全处理到数据湖。</li><li>当将数据摄取到用户档案或流式分段时，流式源支持每秒最多1500个请求。</li></ul> | 流源（如[!DNL Kafka]、[!DNL Azure Event Hubs]和[!DNL Amazon Kinesis]）不使用[!DNL Data Collection Core Service] (DCCS)路由，因此可能有不同的吞吐量限制。 有关可用于数据摄取的源的目录，请参阅[源概述](../sources/home.md)。 |

{style="table-layout:auto"}

## 后续步骤

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [各种Experience Platform服务的端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=zh-Hans#end-to-end-latency-diagrams)。
* [Real-Time Customer Data Platform (B2C Edition - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime和Ultimate包)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
