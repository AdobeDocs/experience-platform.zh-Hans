---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用指标
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a988c990d3d4df706a44cdbc82f77bef20c2ea1

---


# 列表可用指标

下表列表了由Opencibility Insights（可观性分析）公开的所有指标，这些指标按平台服务分类。 每个度量都包括一个描述和一个接受的ID查询参数。

## 数据摄取

下表概述了Adobe Experience Platform数据摄取的指标。 粗体量 **度是流** 式摄取量度。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 创建的数据集总数。 | 不适用 |
| timeseries.ingestion.dataset.size | 为一个或多个数据集摄取的所有数据的累积大小。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.dailysize | 针对一个数据集或所有数据集，以每日使用情况为基准摄取的数据大小。 | 数据集ID（可选） |
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
| **timeseries.data.collection.validation.类别.presence.count** | 一个数据集或所有数据集的无效“状态”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.enum.count** | 一个数据集或所有数据集的无效“enum”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.unclassified.count** | 一个数据集或所有数据集的无效“未分类”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.validation.类别.unknown.count** | 一个数据集或所有数据集的无效“未知”消息总数。 | 数据集ID（可选） |
| **timeseries.data.collection.inlet.total.messages.received** | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID（可选） |
| **timeseries.data.collection.inlet.total.messages.size.received** | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID（可选） |
| **timeseries.data.collection.inlet.success** | 对一个数据入口或所有数据入口的成功HTTP调用总数。 | 入口ID（可选） |
| **timeseries.data.collection.inlet.failure** | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID（可选） |

## 标识服务

下表概述了Adobe Experience Platform Identity Service的指标。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 由Identity Service为一个数据集或所有数据集写入其数据源的记录数。 | 数据集ID（可选） |
| timeseries.identity.dataset.recordfailed.count | Identity Service为一个数据集或所有数据集失败的记录数。 | 数据集ID（可选） |
| timeseries.identity.dataset.namespacecode.recordsuccess.count | 为命名空间成功摄取的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 身份记录数由命名空间失败。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 被命名空间跳过的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | IMS组织的标识图中存储的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 存储在命名空间标识图中的唯一标识数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | IMS组织的标识图中存储的唯一图形标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 针对特定图形强度（“未知”、“弱”或“强”），存储在IMS组织标识图中的唯一标识数。 | 图形强度(**必需**) |

## 隐私服务

下表概述了Adobe Experience Platform隐私服务的指标。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- | ---- |
| timeseries.gdpr.jobs.totaljobs.count | 从GDPR创建的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR中已完成的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR中的错误作业总数。 | ENV(必&#x200B;**需**) |

## 查询服务

下表概述了Adobe Experience Platform查询服务的指标。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- | ---- |
| timeseries.queryservice.query.scheduleonce.count | 非经常性计划查询总数。 | 不适用 |
| timeseries.queryservice.query.scheduledrecurring.count | 重复计划查询的总数。 | 不适用 |
| timeseries.queryservice.query.batchquery.count | 执行批查询总数。 | 不适用 |
| timeseries.queryservice.query.scheduledquery.count | 已执行的计划查询总数。 | 不适用 |
| timeseries.queryservice.query.interactivequery.count | 执行的交互式查询总数。 | 不适用 |
| timeseries.queryservice.query.batchfrompsqlquery.count | 来自PSQL的已执行批查询总数。 | 不适用 |

## 实时客户资料

下表概述了实时客户用户档案的指标。

| 洞察指标 | 描述 | ID查询参数 |
| ---- | ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 按用户档案、一个数据集或所有数据集从数据湖读取的记录数。 | 数据集ID（可选） |
| timeseries.profiles.dataset.recordsuccess.count | 按用户档案、一个数据集或所有数据集写入其数据源的记录数。 | 数据集ID（可选） |
| timeseries.profiles.dataset.recordfailed.count | 按用户档案、一个数据集或所有数据集失败的记录数。 | 数据集ID（可选） |
| timeseries.profiles.dataset.batchsuccess.count | 为数据集或所有数据集摄取的用户档案批次数。 | 数据集ID（可选） |
| timeseries.profiles.dataset.batchfailed.count | 一个数据集或所有数据集失败的用户档案批次数。 | 数据集ID（可选） |
| platform.ups.ingest.streaming.request.m1_rate | 传入请求率。 | IMS组织 |
| platform.ups.ingest.streaming.access.put.success.m1_rate | 摄取成功率。 | IMS组织 |
| platform.ups.ingest.streaming.records.created.m15_rate | 为数据集摄取的新记录的速率。 | 数据集ID |
| platform.ups.ingest.streaming.request.error.created.outOfOrder.m1_rate | 为数据集创建请求而加盖时间戳的无序记录的速率。 | 数据集ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.created.timestamp | 数据集的上次创建记录请求的时间戳。 | 数据集ID |
| platform.ups.ingest.streaming.request.error.updated.outOfOrder.m1_rate | 数据集的更新请求的超出订单时间戳记录的速率。 | 数据集ID |
| platform.ups.profile-commons.ingest.streaming.dataSet.record.updated.timestamp | 数据集的上次更新记录请求的时间戳。 | 数据集ID |
| platform.ups.ingest.streaming.record.size.m1_rate | 平均记录大小。 | IMS组织 |
| platform.ups.ingest.streaming.records.updated.m15_rate | 为数据集摄取的记录请求更新的速率。 | 数据集ID |
