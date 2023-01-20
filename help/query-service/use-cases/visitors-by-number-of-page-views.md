---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；体验事件查询；体验事件查询；体验事件查询；
title: 按访客的页面查看次数列出访客
description: 了解如何编写使用体验事件的查询，以检索按页面查看次数组织的访客列表。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 按访客的页面查看次数列出访客

本文档提供了检索按页面查看次数组织的访客列表所需的SQL示例。 通过Adobe Experience Platform查询服务，您可以编写使用 [!DNL Experience Events] 来捕获各种用例。 体验事件由体验数据模型(XDM)ExperienceEvent类表示，该类可在用户与网站或服务交互时捕获系统的不可更改和非聚合快照。 体验事件甚至可用于时域分析。 请参阅 [“下一步”部分](#next-steps) 对于涉及 [!DNL Experience Events] 以生成访客报表。

有关XDM和 [!DNL Experience Events] 可在 [[!DNL XDM System] 概述](../../xdm/home.md). 通过将查询服务与 [!DNL Experience Events]，则可以有效地跟踪用户中的行为趋势。 以下文档提供了涉及 [!DNL Experience Events].

## 目标

以下示例创建一个报表，其中列出了查看次数最多页面的用户的10个ID。

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
-----------------------------------+-----------
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

通过阅读本文档，您可以更好地了解如何在 [!DNL Experience Events] 列出查看次数最多的页面的用户。

请参阅以下用例，了解其他基于访客的用例：

- [列出访客以前的会话。](./list-visitor-sessions.md)
- [查看访客的汇总报表。](./roll-up-report-of-a-visitor.md)
- [按天创建事件的趋势报表。](./trended-report-of-events.md)
