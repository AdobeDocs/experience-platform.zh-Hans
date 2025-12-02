---
title: Experience Platform中的事件重复处理
description: 了解Adobe Experience Platform如何处理事件重复
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Adobe Experience Platform中的事件重复处理

Adobe Experience Platform是一个高度分布式的系统，旨在最大限度地提高可靠性，同时扩展到不断增加的数据量。

对于实时数据收集，[体验事件](/help/xdm/classes/experienceevent.md)是通过Edge Network从客户端源(如Web SDK或[Mobile SDK](https://developer.adobe.com/client-sdks/home/))收集的，并交付给Experience Platform处理和存储层。 这些层构成诸如Experience Platform、[Real-Time CDP](/help/rtcdp/home.md)、[Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans)和[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hans)之类的解决方案。

为了最大程度地减少体验事件丢失，客户端SDK和内部Experience Platform交付服务需要确认事件已成功收集。

如果未收到该确认，则客户端SDK或内部Experience Platform交付服务会触发重试，并再次发送Experience事件。

这是处理瞬态故障的最佳实践。 其副作用是可能会引入重复事件。

要更好地了解处理瞬态故障的最佳实践，请参阅有关[瞬态故障处理](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults)的文章。

## 事件重复方案 {#scenarios}

事件重复可能会在各种情况下发生，例如但不限于：

* 客户端SDK与[!DNL Edge Network]之间的网络相关问题。 这些问题可能源于Internet服务提供商故障、移动信号丢失或其他网络故障，因为客户和Edge Network之间的连接是通过公共Internet完成的。
* 内部Experience Platform自动缩放事件。 有时，数据可能会因云基础架构的波动而重新平衡。

Adobe Experience Platform数据收集层旨在支持“至少一次”处理。 因此，在少数情况下，可能会发生事件重复。

若要了解有关“至少一次”处理的更多信息，请参阅这篇关于[邮件传递保证](https://docs.confluent.io/kafka/design/delivery-semantics.html)的文章。

## 事件去重选项 {#deduplication}

对于对重复事件敏感的业务方案，Experience Platform在其下游存储系统中使用多种事件重复数据删除方法，如下所述。

* 如果`_id`中已存在具有相同[!DNL Profile store]的事件，则Real-Time CDP配置文件存储区会丢弃事件。 有关更多详细信息，请参阅有关[XDM ExperienceEvent类](/help/xdm/classes/experienceevent.md)的文档。
* Customer Journey Analytics允许用户将指标配置为仅以非重复的方式计入值。 要了解如何执行此操作，请参阅有关[量度去重组件设置](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=zh-Hans)的文档。
* 当需要从计算中删除整个行或忽略特定字段集（因为行中只有部分数据是重复信息）时，Experience Platform查询服务支持重复数据删除。 有关详细信息，请参阅有关查询服务[中重复数据删除](/help/query-service/key-concepts/deduplication.md)的文档。

>[!NOTE]
>
>如果您遇到上述用例以外的事件重复问题，请联系您的Adobe代表并提供有关用例的详细信息。
