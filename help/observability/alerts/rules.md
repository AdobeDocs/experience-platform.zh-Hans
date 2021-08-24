---
keywords: Experience Platform；主页；热门主题；日期范围
title: 标准警报规则
description: '本文档涵盖由Experience Platform提供的预定义警报规则。 '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 13%

---


# 标准警报规则

Adobe Experience Platform提供了多个可为贵组织启用的预定义警报规则。 下表包含这些Adobe提供的警报规则的详细信息。 有关Experience Platform中警报的更多常规信息，请参阅[警报概述](./overview.md)。

| 规则 | 描述 | 评估频率 | 重复窗口 |
| --- | --- | --- | --- |
| 超出授权阈值 | 当创建的用户档案数超过贵组织权利的80%时，将触发此警报。 | 30秒 | 不适用 |
| 过去24小时内没有摄取活动 | 在过去24小时内未摄取任何新数据时，将触发此警报。 | 1 天 | 1 天 |
| SFTP源未摄取数据 | 当[SFTP源](../../sources/connectors/cloud-storage/sftp.md)未在特定时间段内摄取任何数据时，将触发此警报。 | 1 天 | 1 天 |
| 已超出摄取错误率 | 当数据摄取的错误率超过20%时，将触发此警报。 | 30秒 | 30秒 |
| 信息源消息 | 当使用[区段匹配](../../segmentation/ui/segment-match.md)向用户发送身份共享信息源消息时，此警报。 | 不适用 | 不适用 |
| 已吊销馈送访问权限 | 当其他Platform用户使用[区段匹配](../../segmentation/ui/segment-match.md)取消对身份共享信息源的访问时，将触发此警报。 | 不适用 | 不适用 |
| 已修改馈送 | 当用户使用[区段匹配](../../segmentation/ui/segment-match.md)修改身份共享信息源时，将触发此警报。 | 不适用 | 不适用 |
| 共享信息源 | 当用户在[区段匹配](../../segmentation/ui/segment-match.md)中共享新信息源时，将触发此警报。 | 不适用 | 不适用 |
| 链接请求 | 当用户请求连接以进行合作伙伴共享时，将触发此警报。 | 不适用 | 不适用 |
| 链接操作 | 当用户接受连接以进行合作伙伴共享的请求时，将触发此警报。 | 不适用 | 不适用 |
| 禁用区段定义 | 禁用区段定义时，将触发此警报。 | 不适用 | 不适用 |
| 区段作业延迟 | 当区段作业完成时间超过150分钟时，将触发此警报。 | 30秒 | 3 小时 |
| 源流运行失败 | 从源连接摄取数据时出错时，会触发此警报。 | 不适用 | 不适用 |
| 源流运行成功 | 成功从源连接摄取数据时，将触发此警报。 | 不适用 | 不适用 |

{style=&quot;table-layout:auto&quot;}