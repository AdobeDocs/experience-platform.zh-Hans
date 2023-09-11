---
keywords: Experience Platform；主页；热门主题；日期范围
title: 标准警报规则
description: 本文档介绍了Experience Platform提供的预定义警报规则。
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 9120377f5f2048579d7e2a4740cfcbc56d49d61a
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# 标准警报规则

Adobe Experience Platform提供了多个预定义警报规则，您可以为组织启用这些规则。 本文档介绍这些Adobe提供的警报规则的详细信息。 有关Experience Platform中警报的更多常规信息，请参阅 [警报概述](./overview.md).

时间 [在Platform UI中查看警报规则](./ui.md)，您可以单独订阅每个规则。 通过订阅警报时 [I/O事件通知](./subscribe.md)但是，警报规则会整理到不同的订阅包中。 在下表中，每个规则都显示为其对应的I/O事件订阅名称。

## 数据引入

以下警报规则特定于 [数据摄取](../../ingestion/home.md) 和  [源](../../sources/home.md)：

>[!NOTE]
>
>警报当前不支持流源。 您只能订阅批次来源的警报通知。

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 源流运行信息 | 源流运行开始 | 当源连接开始处理数据时，将触发此警报。 |
| 源流运行信息 | 源流运行成功 | 成功从源连接摄取数据时会触发此警报。 |
| 源流运行延迟、失败和错误 | 源流运行失败 | 当从源连接摄取数据时出现错误时，将触发此警报。 |
| 源流运行延迟、失败和错误 | 摄取延迟 | 当批处理摄取流运行需要150分钟以上的时间来处理时，将触发此警报。 |
| 源流运行延迟、失败和错误 | 摄取失败 | 当失败记录与所有记录的比率超过0.5%的阈值时，将触发此警报。 |

{style="table-layout:auto"}

如果您之前订阅了以下警报类型，则不会再收到警报，因为此警报已被弃用：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 源流运行延迟、失败和错误 | 缺乏摄取 | 如果摄取延迟超过7个小时并且没有数据摄取到Platform，则此警报会向您发送消息。 |

{style="table-layout:auto"}

## 身份服务

以下警报规则特定于 [Identity Service](../../identity-service/home.md)：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 身份摄取信息 | Identity服务流运行启动 | 当Identity Service流运行开始处理数据时会触发此警报。 换句话说，摄取的数据正在从数据湖加载到Identity Service中。 |
| 身份摄取信息 | 身份服务流运行成功 | 当数据成功从数据湖加载到Identity Service中时，将触发此警报。 |
| 身份摄取延迟、失败和错误 | Identity服务流运行延迟 | 当Identity Service流运行处理时间超过150分钟时，将触发此警报。 |
| 身份摄取延迟、失败和错误 | 标识服务流运行失败 | 当将数据摄取到Identity Service中时出现错误时，将触发此警报。 |

{style="table-layout:auto"}

## 实时客户配置文件

以下警报规则特定于 [Real-time Customer Profile](../../profile/home.md)：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 配置文件摄取信息 | 配置文件流运行开始 | 当配置文件流运行开始处理数据时，将触发此警报。 |
| 配置文件摄取信息 | 配置文件流运行成功 | 当数据成功从数据湖加载到配置文件时，将触发此警报。 |
| 配置文件摄取延迟、失败和错误 | 配置文件流运行延迟 | 当从数据湖将数据加载到配置文件中需要超过150分钟的处理时间时，将触发此警报。 |
| 配置文件摄取延迟、失败和错误 | 配置文件流运行失败 | 当将数据摄取到配置文件中时出错，则会触发此警报。 |

{style="table-layout:auto"}

## 区段

以下警报规则特定于 [分段服务](../../segmentation/home.md)：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 区段评估作业信息 | 区段作业开始 | 当区段评估作业开始处理数据时，将触发此警报。 |
| 区段评估作业信息 | 区段作业成功 | 当区段评估作业成功完成时，将触发此警报。 |
| 区段评估作业延迟、失败和错误 | 区段作业延迟 | 当区段评估作业完成时间超过150分钟时，将触发此警报。 <br> 将显示以下状态之一： <br> — 触发 — 已满足失败或延迟条件（考虑处于“活动”状态）。 <br> — 不活动 — 条件未满足或未解析（考虑它处于“已解析”状态）。 |
| 区段评估作业延迟、失败和错误 | 区段作业失败 | 当区段评估作业导致错误时，将触发此警报。 |
| 区段评估作业延迟、失败和错误 | 区段定义已禁用 | 当区段定义因内部错误而被禁用时，将触发此警报。 这会自动触发战场，供Adobe工程团队调查此问题。 此警报仅用于提供信息，您无需执行任何操作。 |

{style="table-layout:auto"}

## 目标

以下警报规则特定于 [目标](../../destinations/home.md)：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 目标流运行信息 | 目标流运行开始 | 当目标流运行开始激活区段时，将触发此警报。 |
| 目标流运行信息 | 目标流运行成功 | 成功将区段激活到目标时会触发此警报。 |
| 目标流运行延迟、失败和错误 | 目标流运行延迟 | 当目标流运行需要超过150分钟的时间来激活区段时，将触发此警报。 |
| 目标流运行延迟、失败和错误 | 目标流运行失败 | 在将区段激活到目标时出错时，将触发此警报。 |
| 目标流运行延迟、失败和错误 | 跳过率超过阈值 | 当跳过ID与总ID之比超过阈值时，将触发此警报。 |

{style="table-layout:auto"}

## 查询服务

以下警报规则特定于 [查询服务](../../query-service/home.md)：

| I/O事件订阅 | 警报规则 | 描述 |
| --- | --- | --- |
| 查询服务计划的查询信息 | 查询服务计划的查询启动 | 当计划的查询开始运行时，将触发此警报。 |
| 查询服务计划的查询信息 | 查询服务计划查询成功 | 当计划的查询作业成功完成时，将触发此警报。 |
| 查询服务计划的查询延迟、失败和错误 | 查询服务计划查询失败 | 当计划的查询作业失败时，将触发此警报。 |

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
