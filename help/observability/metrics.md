---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用指标
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---


# 可用指标列表

下表列表了可观察性洞察所揭示的所有指标(按服务分 [!DNL Platform] 类)。 每个度量都包括一个描述和一个接受的ID查询参数。

## [!DNL Data Ingestion]

下表概述了Adobe Experience Platform指标 [!DNL Data Ingestion]。 粗体的 **指标** 是流式摄取指标。

| 洞察指标  | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 创建的数据集总数。 | 不适用 |
| timeseries.ingestion.dataset.size | 为一个或多个数据集摄取的所有数据的累计大小。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.dailysize | 根据每日使用情况摄取的数据大小，用于一个数据集或所有数据集。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.batchfailed.count | 一个数据集或所有数据集失败的批次数。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.batchsuccess.count | 为一个数据集或所有数据集摄取的批次数。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.recordsuccess.count | 为一个数据集或所有数据集摄取的记录数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.total.messages.rate** | 一个数据集或所有数据集的消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.valid.messages.rate** | 一个数据集或所有数据集的有效消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.invalid.messages.rate** | 一个数据集或所有数据集的无效消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.type.count** | 一个数据集或所有数据集的无效“类型”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.range.count** | 一个数据集或所有数据集的无效“范围”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.format.count** | 一个数据集或所有数据集的无效“格式”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.pattern.count** | 一个数据集或所有数据集的无效“模式”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.presence.count** | 一个数据集或所有数据集的无效“存在”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.enum.count** | 一个数据集或所有数据集的无效“枚举”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.unclassified.count** | 一个数据集或所有数据集的无效“未分类”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.unknown.count** | 一个数据集或所有数据集的无效“未知”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID（可选） |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID（可选） |
| **timeseries.data.collection.inlet.success** | 对一个数据入口或所有数据入口成功的HTTP调用总数。 | 入口ID（可选） |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID（可选） |

## [!DNL Identity Service]

下表概述了Adobe Experience Platform指标 [!DNL Identity Service]。

| 洞察指标  | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 为一个数据集或所有数据集写入 [!DNL Identity Service]其数据源的记录数。 | 数据集ID（可选） |
| timeseries.identity.dataset.recordfailed.count | 失败的记录数 [!DNL Identity Service]目依据、一个数据集或所有数据集。 | 数据集ID（可选） |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 为命名空间成功摄取的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 由命名空间失败的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 命名空间跳过的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | IMS组织的标识图中存储的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 存储在标识图中的命名空间的唯一标识数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | IMS组织的标识图中存储的唯一图形标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | IMS组织在标识图中存储的特定标识数，用于特定图形强度（“未知”、“弱”或“强”）。 | 图形强度(**必需**) |

## [!DNL Privacy Service]

下表概述了Adobe Experience Platform指标 [!DNL Privacy Service]。

| 洞察指标  | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 从GDPR创建的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR已完成的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR中的错误作业总数。 | ENV(必&#x200B;**需**) |

## [!DNL Query Service]

下表概述了Adobe Experience Platform指标 [!DNL Query Service]。

| 洞察指标  | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非重复计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.scheduledrecurring.count | 定期计划查询总数。 | 不适用 |
| timeseries.queryservice.query.batchquery.count | 已执行的批查询总数。 | 不适用 |
| timeseries.queryservice.query.scheduledquery.count | 已执行的计划查询总数。 | 不适用 |
| timeseries.queryservice.query.interactivequery.count | 执行的交互式查询总数。 | 不适用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | PSQL中执行的批查询总数。 | 不适用 |

## [!DNL Real-time Customer Profile]

下表概述了相关指标 [!DNL Real-time Customer Profile]。

| 洞察指标  | 描述 | ID查询参数 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 从中读取的记录数 [!DNL Data Lake] 量， [!DNL Profile]依据一个数据集或所有数据集。 | 数据集ID（可选） |
| timeseries.profiles.dataset.recordsuccess.count | 按、一个数据集或所有数据集 [!DNL Profile]写入其数据源的记录数。 | 数据集ID（可选） |
| timeseries.profiles.dataset.recordfailed.count | 失败的记录数 [!DNL Profile]目依据、一个数据集或所有数据集。 | 数据集ID（可选） |
| timeseries.profiles.dataset.batchsuccess.count | 为数据集 [!DNL Profile] 或所有数据集摄取的批次数。 | 数据集ID（可选） |
| timeseries.profiles.dataset.batchfailed.count | 一个数 [!DNL Profile] 据集或所有数据集失败的批次数。 | 数据集ID（可选） |
| platform.ups.ingest.streaming.request.m1_rate | 传入请求率。 | IMS组织 |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 摄取成功率。 | IMS组织 |
| platform.ups.ingest.streaming.records.created.m15_rate | 为数据集摄取的新记录的速率。 | 数据集ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 创建数据集请求的超时时间戳记录的速率。 | 数据集ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 数据集的上次创建记录请求的时间戳。 | 数据集ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 数据集更新请求的超时时间戳记录的速率。 | 数据集ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 数据集的上次更新记录请求的时间戳。 | 数据集ID |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均记录大小。 | IMS组织 |
| platform.ups.ingest.streaming.records.updated.m15_rate | 为数据集摄取的记录请求更新的速率。 | 数据集ID |
