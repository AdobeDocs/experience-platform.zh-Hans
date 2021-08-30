---
keywords: Experience Platform；主页；热门主题；日期范围
title: 标准警报规则
description: '本文档涵盖由Experience Platform提供的预定义警报规则。 '
source-git-commit: de8d8d92622abc75f2d09f4bb771dbe4268d0b38
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 12%

---


# 标准警报规则

Adobe Experience Platform提供了多个可为贵组织启用的预定义警报规则。 下表包含这些Adobe提供的警报规则的详细信息。 有关Experience Platform中警报的更多常规信息，请参阅[警报概述](./overview.md)。

| 规则 | 描述 | 评估频率 | 重复窗口 |
| --- | --- | --- | --- |
| 源流运行成功 | 成功从源连接摄取数据时，将触发此警报。 | 不适用 | 不适用 |
| 源流运行失败 | 从源连接摄取数据时出错时，会触发此警报。 | 不适用 | 不适用 |
| 区段作业延迟 | 当区段作业完成时间超过150分钟时，将触发此警报。 | 30秒 | 3 小时 |
| 禁用区段定义 | 禁用区段定义时，将触发此警报。 | 不适用 | 不适用 |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
