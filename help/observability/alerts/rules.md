---
keywords: Experience Platform；主页；热门主题；日期范围
title: 标准警报规则
description: 本文档涵盖由Experience Platform提供的预定义警报规则。
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: f707a6338ad72578328b363792010fa50ea9ce88
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 标准警报规则

Adobe Experience Platform提供了多个可为贵组织启用的预定义警报规则。 本文档介绍这些Adobe提供的警报规则的详细信息。 有关Experience Platform中警报的更多常规信息，请参阅 [警报概述](./overview.md).

When [在平台UI中查看警报规则](./ui.md)，则可以单独订阅每个规则。 通过订阅警报时 [I/O事件通知](./subscribe.md)但是，警报规则会组织到不同的订阅包中。 在下表中，每个规则都显示其相应的I/O事件订阅名称。

## 数据引入

以下警报规则专用于 [数据摄取](../../ingestion/home.md) 和  [来源](../../sources/home.md):

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 源流运行信息 | 源流运行开始 | 当源连接开始处理数据时，将触发此警报。 |
| 源流运行信息 | 源流运行成功 | 成功从源连接摄取数据时，将触发此警报。 |
| 源流运行延迟、失败和错误 | 源流运行失败 | 从源连接摄取数据时出错时，会触发此警报。 |
| 源流运行延迟、失败和错误 | 摄取延迟 | 当批量摄取流程运行超过150分钟时，将触发此警报。 |
| 源流运行延迟、失败和错误 | 摄取失败 | 当失败记录与所有记录的比率超过0.5%的阈值时，将触发此警报。 |

{style=&quot;table-layout:auto&quot;}

如果您之前订阅了以下警报类型，则由于此警报已被弃用，因此您将不再收到警报：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 源流运行延迟、失败和错误 | 缺少摄取 | 如果摄取延迟超过七小时且未将数据摄取到平台，则此警报会向您发送消息。 |

{style=&quot;table-layout:auto&quot;}

## Identity Service

以下警报规则专用于 [Identity Service](../../identity-service/home.md):

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 身份摄取信息 | Identity服务流运行开始 | 当Identity服务流程运行开始处理数据时，将触发此警报。 换言之，将摄取的数据从数据湖加载到Identity Service中。 |
| 身份摄取信息 | Identity服务流运行成功 | 成功将数据从数据湖加载到Identity服务后，将触发此警报。 |
| 身份摄取延迟、失败和错误 | Identity服务流运行延迟 | 当处理Identity服务流程运行超过150分钟时，将触发此警报。 |
| 身份摄取延迟、失败和错误 | Identity服务流运行失败 | 将数据摄取到Identity服务时出错时，会触发此警报。 |

{style=&quot;table-layout:auto&quot;}

## 实时客户个人资料

以下警报规则专用于 [实时客户资料](../../profile/home.md):

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 配置文件摄取信息 | 配置文件流运行开始 | 当用户档案流程运行开始处理数据时，将触发此警报。 |
| 配置文件摄取信息 | 配置文件流运行成功 | 当数据成功从数据湖加载到用户档案时，将触发此警报。 |
| 配置文件摄取延迟、失败和错误 | 配置文件流运行延迟 | 当将数据从数据湖加载到用户档案需要超过150分钟才能处理时，会触发此警报。 |
| 配置文件摄取延迟、失败和错误 | 配置文件流运行失败 | 将数据摄取到用户档案时出错时，会触发此警报。 |

{style=&quot;table-layout:auto&quot;}

## 区段

以下警报规则专用于 [Segmentation Service](../../segmentation/home.md):

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 区段评估作业信息 | 区段作业开始 | 当区段评估作业开始处理数据时，将触发此警报。 |
| 区段评估作业信息 | 区段作业成功 | 成功完成区段评估作业时，将触发此警报。 |
| 区段评估作业延迟、失败和错误 | 区段作业延迟 | 当区段评估作业完成时间超过150分钟时，将触发此警报。 |
| 区段评估作业延迟、失败和错误 | 区段作业失败 | 当区段评估作业导致错误时，将触发此警报。 |
| 区段评估作业延迟、失败和错误 | 禁用区段定义 | 当区段定义因内部错误而被禁用时，将触发此警报。 这会自动触发一个供Adobe工程团队调查此问题的战争室。 此警报仅供参考，无需您采取任何操作。 |

{style=&quot;table-layout:auto&quot;}

## 目标

以下警报规则专用于 [目标](../../destinations/home.md):

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 目标流运行信息 | 目标流运行开始 | 当目标流运行开始激活区段时，将触发此警报。 |
| 目标流运行信息 | 目标流运行成功 | 成功将区段激活到目标时，将触发此警报。 |
| 目标流运行延迟、失败和错误 | 目标流运行延迟 | 当目标流运行时间超过150分钟才能激活区段时，将触发此警报。 |
| 目标流运行延迟、失败和错误 | 目标流运行失败 | 在将区段激活到目标时出错时，会触发此警报。 |
| 目标流运行延迟、失败和错误 | 跳页率超过阈值 | 当跳过的ID与总ID的比率超过阈值时，将触发此警报。 |

{style=&quot;table-layout:auto&quot;}

## 查询服务

以下警报规则专用于 [查询服务](../../query-service/home.md):

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 查询服务临时信息 | 查询服务临时成功 | 当临时架构作业成功完成时，将触发此警报。 |
| 查询服务临时延迟、失败和错误 | 查询服务临时失败 | 当临时架构作业失败时，将触发此警报。 |
| 查询服务计划查询信息 | 查询服务计划查询开始 | 当计划查询开始运行时，将触发此警报。 |
| 查询服务计划查询信息 | 查询服务计划查询成功 | 成功完成计划查询作业时，将触发此警报。 |
| 查询服务计划查询延迟、失败和错误 | 查询服务计划查询失败 | 当计划查询作业失败时，将触发此警报。 |

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
