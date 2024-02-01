---
title: Experience Platform中的事件重复处理
description: 了解Adobe Experience Platform如何处理事件重复
source-git-commit: 89cdb0832009bcee31b4339f021bc5a0ce254752
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Adobe Experience Platform中的事件重复处理

Adobe Experience Platform是一个高度分布式的系统，旨在最大限度地提高可靠性，同时扩展到不断增加的数据量。

对于实时数据收集， [体验事件](../xdm/classes/experienceevent.md) 是通过 [边缘网络](../edge/home.md#edge-network)，来自客户端源，如 [Web SDK](../edge/home.md) 或 [移动SDK](https://developer.adobe.com/client-sdks/home/)，并传送到Experience Platform处理和存储层。 这些层构成解决方案，例如Experience Platform、 [Real-Time CDP](../rtcdp/home.md)， [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans)、和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html).

为了最大程度地减少Experience Event丢失，客户端SDK和内部Experience Platform交付服务需要确认事件已成功收集。

如果未收到该确认，则客户端SDK或内部Platform交付服务将触发重试，并再次发送Experience事件。

这是处理瞬态故障的最佳实践。 其副作用是可能会引入重复事件。

要更好地了解处理瞬态故障的最佳实践，请参阅此文章，其主题为 [瞬态故障处理](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## 事件重复方案 {#scenarios}

事件重复可能会在各种情况下发生，例如但不限于：

* 客户端SDK与 [!DNL Edge Network]. 这些问题可能源自互联网服务提供商故障、移动信号丢失或其他网络故障，因为客户与边缘网络之间的连接是通过公共Internet完成的。
* 内部Experience Platform自动缩放事件。 有时，数据可能会因云基础架构的波动而重新平衡。

Adobe Experience Platform数据收集层旨在支持“至少一次”处理。 因此，在少数情况下，可能会发生事件重复。

要了解有关“至少一次”处理的更多信息，请参阅此文章位于 [报文传送保证](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## 事件去重选项 {#deduplication}

对于对重复事件敏感的业务情形，Experience Platform在其下游存储系统中使用多种事件重复数据删除方法，如下所述。

* 如果某个事件具有相同的属性，则Real-Time CDP配置文件存储区会丢弃事件 `_id` 已存在于 [!DNL Profile Store]. 请参阅相关文档 [XDM ExperienceEvent类](../xdm/classes/experienceevent.md) 以了解更多详细信息。
* Customer Journey Analytics允许用户将指标配置为仅以非重复的方式计入值。 要了解如何执行此操作，请参阅关于以下内容的文档： [量度去重组件设置](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=zh-Hans).
* 当需要从计算中删除整行数据或由于行中只有部分数据是重复信息而忽略特定字段集时，Experience Platform查询服务支持重复数据删除。 请参阅相关的文档 [查询服务中的重复数据删除](../query-service/key-concepts/deduplication.md) 以了解更多信息。

>[!NOTE]
>
>如果您遇到上述用例以外的事件重复问题，请联系您的Adobe代表并提供有关用例的详细信息。