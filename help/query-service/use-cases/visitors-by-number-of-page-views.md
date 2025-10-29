---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；experienceevent查询；experienceevent查询；体验事件查询；
title: 按访客页面查看次数列出访客
description: 了解如何编写查询，这些查询使用体验事件检索按页面查看次数组织的访客列表。
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# 按访客页面查看次数列出访客

本文档提供了一个示例，说明检索按页面查看次数组织的访客列表所需的SQL。 使用Adobe Experience Platform查询服务，您可以编写使用[!DNL Experience Events]来捕获各种用例的查询。 体验事件由体验数据模型(XDM) ExperienceEvent类表示，该类捕获用户与网站或服务交互时系统的不可变和非聚合快照。 体验事件甚至可用于时域分析。 请参阅[后续步骤部分](#next-steps)以了解更多涉及[!DNL Experience Events]的用例以生成访客报告。

有关XDM和[!DNL Experience Events]的更多信息，请参阅[[!DNL XDM System] 概述](../../xdm/home.md)。 通过将查询服务与[!DNL Experience Events]相结合，您可以有效地跟踪用户之间的行为趋势。 以下文档提供了涉及[!DNL Experience Events]的查询示例。

## 目标

以下示例创建一个报表，其中列出查看页面次数最多的用户的10个ID。

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

查询结果显示在下表中。

```console
               id                  | pageViews
|-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## 后续步骤 {#next-steps}

通过阅读本文档，您可以更好地了解如何将查询服务与[!DNL Experience Events]结合使用，以列出查看页面次数最多的用户。

请参阅以下用例，了解其他基于访客的用例：

- [列出访客以前的会话。](./list-visitor-sessions.md)
- [查看访客的汇总报表。](./roll-up-report-of-a-visitor.md)
- [按日期创建事件趋势报表。](./trended-report-of-events.md)
