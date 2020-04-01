---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 可用指标
topic: developer guide
translation-type: tm+mt
source-git-commit: 947955403a270914437d9172bca458f9c49ccd8f

---


# 列表可用指标

以下是可观察性洞察公开的指标列表，每个指标都包含其关联的平台服务、描述和接受的ID查询参数。

| 洞察指标 | 平台服务 | 描述 | ID查询参数 |
| ---- | ---- | ---- | ---- |
| timeseries.ingestion.dataset.new.count | 数据摄取 | 创建的数据集总数。 | 不适用 |
| timeseries.ingestion.dataset.size | 数据摄取 | 为一个或多个数据集摄取的所有数据的累积大小。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.dailysize | 数据摄取 | 针对一个数据集或所有数据集，以每日使用情况为基准摄取的数据大小。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.batchfailed.count | 数据摄取 | 一个数据集或所有数据集失败的批次数。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.batchsuccess.count | 数据摄取 | 为一个数据集或所有数据集摄取的批次数。 | 数据集ID（可选） |
| timeseries.ingestion.dataset.recordsuccess.count | 数据摄取 | 为一个数据集或所有数据集摄取的记录数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.total.messages.rate | 数据摄取（流） | 一个数据集或所有数据集的消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.valid.messages.rate | 数据摄取（流） | 一个数据集或所有数据集的有效消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.invalid.messages.rate | 数据摄取（流） | 一个数据集或所有数据集的无效消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.type.count | 数据摄取（流） | 一个数据集或所有数据集的无效“类型”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.range.count | 数据摄取（流） | 一个数据集或所有数据集的无效“范围”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.format.count | 数据摄取（流） | 一个数据集或所有数据集的无效“格式”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.pattern.count | 数据摄取（流） | 一个数据集或所有数据集的无效“模式”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.presence.count | 数据摄取（流） | 一个数据集或所有数据集的无效“状态”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.enum.count | 数据摄取（流） | 一个数据集或所有数据集的无效“enum”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.unclassified.count | 数据摄取（流） | 一个数据集或所有数据集的无效“未分类”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.validation.类别.unknown.count | 数据摄取（流） | 一个数据集或所有数据集的无效“未知”消息总数。 | 数据集ID（可选） |
| timeseries.data.collection.inlet.total.messages.received | 数据摄取（流） | 为一个数据入口或所有数据入口接收的消息总数。 | 入口ID（可选） |
| timeseries.data.collection.inlet.total.messages.size.received | 数据摄取（流） | 为一个数据入口或所有数据入口接收的数据的总大小。 | 入口ID（可选） |
| timeseries.data.collection.inlet.success | 数据摄取（流） | 对一个数据入口或所有数据入口的成功HTTP调用总数。 | 入口ID（可选） |
| timeseries.data.collection.inlet.failure | 数据摄取（流） | 对一个数据入口或所有数据入口的失败HTTP调用总数。 | 入口ID（可选） |
| timeseries.用户档案.dataset.recordear.count | 实时客户资料 | 按用户档案、一个数据集或所有数据集从数据湖读取的记录数。 | 数据集ID（可选） |
| timeseries.用户档案.dataset.recordsuccess.count | 实时客户资料 | 按用户档案、一个数据集或所有数据集写入其数据源的记录数。 | 数据集ID（可选） |
| timeseries.用户档案.dataset.recordfailed.count | 实时客户资料 | 按用户档案、一个数据集或所有数据集失败的记录数。 | 数据集ID（可选） |
| timeseries.用户档案.dataset.batchsuccess.count | 实时客户资料 | 为数据集或所有数据集摄取的用户档案批次数。 | 数据集ID（可选） |
| timeseries.用户档案.dataset.batchfailed.count | 实时客户资料 | 一个数据集或所有数据集失败的用户档案批次数。 | 数据集ID（可选） |
| timeseries.identity.dataset.recordsuccess.count | 标识服务 | 由Identity Service为一个数据集或所有数据集写入其数据源的记录数。 | 数据集ID（可选） |
| timeseries.identity.dataset.recordfailed.count | 标识服务 | Identity Service为一个数据集或所有数据集失败的记录数。 | 数据集ID（可选） |
| timeseries.identity.dataset.namepacecode.recordsuccess.count | 标识服务 | 为命名空间成功摄取的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 标识服务 | 身份记录数由命名空间失败。 | 命名空间ID(**必需**) |
| timeseries.identity.dataset.namepacecode.recordkipped.count | 标识服务 | 被命名空间跳过的身份记录数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.uniqueidentity.count | 标识服务 | IMS组织的标识图中存储的唯一标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentity.count | 标识服务 | 存储在命名空间标识图中的唯一标识数。 | 命名空间ID(**必需**) |
| timeseries.identity.graph.imsorg.numidgraphs.count | 标识服务 | IMS组织的标识图中存储的唯一图形标识数。 | 不适用 |
| timeseries.identity.graph.imsorg.graphstrenth.uniqueidentity.count | 标识服务 | 针对特定图形强度（“未知”、“弱”或“强”），存储在IMS组织标识图中的唯一标识数。 | 图形强度(**必需**) |
| timeseries.gdpr.jobs.totaljobs.count | GDPR | 从GDPR创建的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.completedjobs.count | GDPR | GDPR中已完成的作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.gdpr.jobs.errorjobs.count | GDPR | GDPR中的错误作业总数。 | ENV(必&#x200B;**需**) |
| timeseries.queryservice.查询.scheduleonce.count | 查询服务 | 非经常性计划查询总数。 | 不适用 |
| timeseries.queryservice.查询.scheduledrecuring.count | 查询服务 | 重复计划查询的总数。 | 不适用 |
| timeseries.queryservice.查询.batchquery.count | 查询服务 | 执行批查询总数。 | 不适用 |
| timeseries.queryservice.查询.scheduledquery.count | 查询服务 | 已执行的计划查询总数。 | 不适用 |
| timeseries.queryservice.查询.interactivequery.count | 查询服务 | 执行的交互式查询总数。 | 不适用 |
| timeseries.queryservice.查询.batchfrompsqlquery.count | 查询服务 | 来自PSQL的已执行批查询总数。 | 不适用 |