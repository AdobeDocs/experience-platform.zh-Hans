---
title: Adobe Analytics ExperienceEvent完整扩展架构字段组
description: 了解Adobe Analytics ExperienceEvent完整扩展架构字段组。
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 5%

---

# [!UICONTROL Adobe Analytics ExperienceEvent Full Extension]架构字段组

[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于捕获Adobe Analytics收集的通用指标。

本文档介绍了Analytics扩展字段组的结构和用例。

>[!NOTE]
>
>由于此字段组中重复元素的大小和数量，本指南中显示的许多字段已折叠以节省空间。 要探究此字段组的完整结构，您可以[在Experience Platform UI](../../ui/explore.md)中查找它，或在[公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)中查看完整的架构。

## 字段组结构

字段组为架构提供单个`_experience`对象，它本身包含单个`analytics`对象。

![Analytics字段组的顶级字段](../../images/field-groups/analytics-full-extension/full-schema.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `customDimensions` | 对象 | 捕获Analytics跟踪的自定义维度。 有关此对象内容的更多信息，请参阅[下面的](#custom-dimensions)子部分。 |
| `endUser` | 对象 | 捕获触发事件的最终用户的Web交互详细信息。 有关此对象内容的更多信息，请参阅[下面的](#end-user)子部分。 |
| `environment` | 对象 | 捕获有关触发事件的浏览器和操作系统的信息。 有关此对象内容的更多信息，请参阅[下面的](#environment)子部分。 |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | 对象 | 字段组提供对象字段，用于捕获最多1000个自定义事件。 有关这些字段的更多信息，请参阅下面[的](#events)子部分。 |
| `session` | 对象 | 捕获有关触发事件的会话的信息。 有关此对象内容的更多信息，请参阅[下面的](#session)子部分。 |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions`捕获Analytics跟踪的自定义[维度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html)。

![customDimension字段](../../images/field-groups/analytics-full-extension/customDimensions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `eVars` | 对象 | 捕获最多250个转化变量的对象([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=zh-CN))。 此对象的属性被设置为`eVar1`到`eVar250`的键值，并且仅接受其数据类型的字符串。 |
| `hierarchies` | 对象 | 捕获最多五个自定义层次结构变量([hiers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html))的对象。 此对象的属性被设置为`hier1`到`hier5`的键值，这些属性本身是具有以下子属性的对象：<ul><li>`delimiter`：用于生成`values`下提供的列表的原始分隔符。</li><li>`values`：层次结构级别名称的分隔列表，以字符串形式表示。</li></ul> |
| `listProps` | 对象 | 捕获最多75个[列表属性](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props)的对象。 此对象的属性被设置为`prop1`到`prop75`的键值，这些属性本身是具有以下子属性的对象：<ul><li>`delimiter`：用于生成`values`下提供的列表的原始分隔符。</li><li>`values`：属性值的分隔列表，以字符串形式表示。</li></ul> |
| `lists` | 对象 | 捕获最多三个[列表](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html)的对象。 此对象的属性被设置为`list1`到`list3`的键值。 每个属性都包含一个`list`数组，其中包含[[!UICONTROL Key Value Pair]](../../data-types/key-value-pair.md)数据类型。 |
| `props` | 对象 | 捕获最多75个[prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html)的对象。 此对象的属性被设置为`prop1`到`prop75`的键值，并且仅接受其数据类型的字符串。 |
| `postalCode` | 字符串 | 客户提供的邮政编码。 |
| `stateProvince` | 字符串 | 客户端提供的州或省位置。 |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser`捕获触发事件的最终用户的Web交互详细信息。

![endUser字段](../../images/field-groups/analytics-full-extension/endUser.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | 与此最终用户的网页、链接和来自第一个体验事件的反向链接相关的信息。 |
| `firstTimestamp` | 整数 | 此最终用户的第一个ExperienceEvent的Unix时间戳。 |

## `environment` {#environment}

`environment`捕获有关触发事件的浏览器和操作系统的信息。

![环境字段](../../images/field-groups/analytics-full-extension/environment.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `browserIDStr` | 字符串 | 所用浏览器的Adobe Analytics标识符（也称为[浏览器类型维度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)）。 |
| `operatingSystemIDStr` | 字符串 | 所用操作系统的Adobe Analytics标识符（也称为[操作系统类型维度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)）。 |

## 自定义事件字段 {#events}

Analytics扩展字段组提供了10个对象字段，每个字段最多可捕获100个[自定义事件量度](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html)，字段组的总数量为1000。

每个顶级事件对象包含其各自范围内的单个事件对象。 例如，`event101to200`包含从`event101`到`event200`的键值事件。

每个偶数对象使用[[!UICONTROL Measure]](../../data-types/measure.md)数据类型，提供唯一标识符和可量化的值。

![自定义事件字段](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session`捕获有关触发事件的会话的信息。

![会话字段](../../images/field-groups/analytics-full-extension/session.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `search` | [[!UICONTROL Search]](../../data-types/search.md) | 捕获与会话条目的Web或移动搜索相关的信息。 |
| `web` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | 捕获有关会话条目的链接点击次数、网页详细信息、反向链接信息和浏览器详细信息的信息。 |
| `depth` | 整数 | 最终用户的当前会话深度（如页码）。 |
| `num` | 整数 | 最终用户的当前会话编号。 |
| `timestamp` | 整数 | 会话条目的Unix时间戳。 |

## 后续步骤

本文档介绍了Analytics扩展字段组的结构和用例。 有关字段组本身的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)。

如果您使用此字段组通过Adobe Experience Platform Web SDK收集Analytics数据，请参阅[配置数据流](../../../datastreams/overview.md)指南，了解如何将数据映射到服务器端的XDM。
