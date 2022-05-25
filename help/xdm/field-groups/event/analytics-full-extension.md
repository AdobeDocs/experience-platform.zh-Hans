---
title: Adobe Analytics ExperienceEvent完整扩展架构字段组
description: 本文档概述了Adobe Analytics ExperienceEvent完整扩展架构字段组。
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 7%

---

# [!UICONTROL Adobe Analytics ExperienceEvent完整扩展] 架构字段组

[!UICONTROL Adobe Analytics ExperienceEvent完整扩展] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)，可捕获由Adobe Analytics收集的常用量度。

本文档介绍Analytics扩展字段组的结构和用例。

>[!NOTE]
>
>由于此字段组中重复元素的大小和数量，本指南中显示的许多字段都已折叠以节省空间。 要浏览此字段组的完整结构，您可以 [在平台UI中查找 ](../../ui/explore.md) 或在 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## 字段组结构

字段组提供了 `_experience` 对象，该模式本身包含单个 `analytics` 对象。

![Analytics字段组的顶级字段](../../images/field-groups/analytics-full-extension/full-schema.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `customDimensions` | 对象 | 捕获由Analytics跟踪的自定义维度。 请参阅 [下文](#custom-dimensions) 以了解有关此对象内容的详细信息。 |
| `endUser` | 对象 | 为触发事件的最终用户捕获Web交互详细信息。 请参阅 [下文](#end-user) 以了解有关此对象内容的详细信息。 |
| `environment` | 对象 | 捕获有关触发事件的浏览器和操作系统的信息。 请参阅 [下文](#environment) 以了解有关此对象内容的详细信息。 |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | 对象 | 字段组提供对象字段以捕获最多1000个自定义事件。 请参阅 [下文](#events) 以了解有关这些字段的详细信息。 |
| `session` | 对象 | 捕获有关触发事件的会话的信息。 请参阅 [下文](#session) 以了解有关此对象内容的详细信息。 |

{style=&quot;table-layout:auto&quot;}

## `customDimensions` {#custom-dimensions}

`customDimensions` 捕获自定义 [维度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html?lang=zh-Hans) Analytics跟踪的区段。

![customDimensions字段](../../images/field-groups/analytics-full-extension/customDimensions.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `eVars` | 对象 | 捕获最多250个转化变量([eVar](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html?lang=zh-CN))。 此对象的属性已进行键控 `eVar1` to `eVar250` 且仅接受其数据类型的字符串。 |
| `hierarchies` | 对象 | 捕获最多五个自定义层次结构变量([海标](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html))。 此对象的属性已进行键控 `hier1` to `hier5`，这些对象本身具有以下子属性：<ul><li>`delimiter`:用于生成下提供的列表的原始分隔符 `values`.</li><li>`values`:层次结构级别名称的分隔列表，以字符串形式表示。</li></ul> |
| `listProps` | 对象 | 捕获最多75个对象 [列表属性](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). 此对象的属性已进行键控 `prop1` to `prop75`，这些对象本身具有以下子属性：<ul><li>`delimiter`:用于生成下提供的列表的原始分隔符 `values`.</li><li>`values`:prop的分隔值列表，以字符串形式表示。</li></ul> |
| `lists` | 对象 | 捕获最多三个的对象 [列表](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). 此对象的属性已进行键控 `list1` to `list3`. 这些属性中的每个属性都包含一个 `list` 阵列 [[!UICONTROL 键值对]](../../data-types/key-value-pair.md) 数据类型。 |
| `props` | 对象 | 捕获最多75个对象 [prop](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). 此对象的属性已进行键控 `prop1` to `prop75` 且仅接受其数据类型的字符串。 |
| `postalCode` | 字符串 | 客户提供的邮政编码。 |
| `stateProvince` | 字符串 | 客户端提供的州或省的位置。 |

{style=&quot;table-layout:auto&quot;}

## `endUser` {#end-user}

`endUser` 捕获触发事件的最终用户的web交互详细信息。

![endUser字段](../../images/field-groups/analytics-full-extension/endUser.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web信息]](../../data-types/web-information.md) | 与此最终用户首次体验事件中的网页、链接和反向链接相关的信息。 |
| `firstTimestamp` | 整数 | 此最终用户的第一个ExperienceEvent的Unix时间戳。 |

## `environment` {#environment}

`environment` 捕获有关触发事件的浏览器和操作系统的信息。

![环境字段](../../images/field-groups/analytics-full-extension/environment.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `browserIDStr` | 字符串 | 使用的浏览器的Adobe Analytics标识符(也称为 [浏览器类型维度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html))。 |
| `operatingSystemIDStr` | 字符串 | 使用的操作系统的Adobe Analytics标识符(也称为 [操作系统类型维度](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html))。 |

## 自定义事件字段 {#events}

Analytics扩展字段组提供了十个对象字段，这些字段最多可捕获100个 [自定义事件量度](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) 每个字段组合计为1000。

每个顶级事件对象都包含其各自范围内的单个事件对象。 例如， `event101to200` 包含键入自 `event101` to `event200`.

每个偶数对象都使用 [[!UICONTROL 测量]](../../data-types/measure.md) 数据类型，提供唯一标识符和可计量值。

![自定义事件字段](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` 捕获有关触发事件的会话的信息。

![会话字段](../../images/field-groups/analytics-full-extension/session.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `search` | [[!UICONTROL  搜索]](../../data-types/search.md) | 捕获与Web或移动搜索有关的会话条目信息。 |
| `web` | [[!UICONTROL Web信息]](../../data-types/web-information.md) | 捕获有关会话条目的链接点击量、网页详细信息、反向链接信息和浏览器详细信息的信息。 |
| `depth` | 整数 | 最终用户的当前会话深度（如页码）。 |
| `num` | 整数 | 最终用户的当前会话编号。 |
| `timestamp` | 整数 | 会话条目的Unix时间戳。 |

## 后续步骤

本文档介绍了Analytics扩展字段组的结构和用例。 有关字段组本身的详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

如果您使用此字段组通过Adobe Experience Platform Web SDK收集Analytics数据，请参阅 [配置数据流](../../../edge/datastreams/overview.md) 了解如何将数据映射到服务器端的XDM。
