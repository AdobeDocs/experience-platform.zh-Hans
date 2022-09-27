---
title: Adobe Experience Platform发行说明2022年9月
description: 2022年9月版Adobe Experience Platform发行说明。
source-git-commit: 5335c77b4636d10064e8786525c9f8f893371b9b
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 7%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 9 月 28 日**

Adobe Experience Platform 现有功能的更新包括：

- [体验数据模型(XDM)](#xdm)
- [Identity Service](#identity-service)
- [源](#sources)

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| UI支持枚举和建议值 | 除了启用数据验证的枚举之外，您现在还可以 [添加或删除建议值](../../xdm/ui/fields/enum.md) 标准或自定义字符串字段，以便Platform用户在创建区段时可以从中选择一个易记值列表。 |

**新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL AJO分类字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 与之交互的特定元素的属性，该元素会触发建议事件。 |
| 字段组 | [[!UICONTROL MediaAnalytics互动详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 跟踪一段时间内的媒体交互。 |
| 字段组 | [[!UICONTROL 媒体详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 跟踪媒体详细信息。 |
| 字段组 | [[!UICONTROL AdobeCJM ExperienceEvent — 曲面]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | 描述Adobe Journey Optimizer中体验事件的曲面。 |

{style=&quot;table-layout:auto&quot;}

**更新了XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 行为 | [[!UICONTROL 时间系列]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>为 `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>删除了 `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 字段组 | （多个） | [更新了多个字段描述](https://github.com/adobe/xdm/pull/1628/files) 跨Journey Orchestration组件。 |
| 字段组 | （多个） | [更新了多个Adobe Workfront组件的标题](https://github.com/adobe/xdm/pull/1634/files) 以保持一致性。 |
| 字段组 | [[!UICONTROL AJO分类字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 已将多个字段的命名空间更新为 `xdm`. |
| 字段组 | [[!UICONTROL Journey Orchestration步骤事件常用字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 添加了新字段， `isReadSegmentTriggerStartEvent`. |
| 字段组 | [[!UICONTROL 预测天气]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 更改了 `xdm:uvIndex` 字段，并将 `xdm` 命名空间。 |
| 字段组 | [[!UICONTROL 媒体详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 和 `xdm:implementationDetails` 已从字段组中删除。 |
| 数据类型 | （多个） | [更新了多个媒体属性名称](https://github.com/adobe/xdm/pull/1626/files) 跨多个数据类型以保持一致性。 |
| 数据类型 | [[!UICONTROL 实施详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 添加了颤动的已知名称。 |
| 数据类型 | [[!UICONTROL 目标点详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 数据类型现在可以接受与目标点关联的元数据键值对列表。 |
| 数据类型 | [[!UICONTROL 建议行动]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 已更名为 [!UICONTROL 建议行动]. |
| 数据类型 | [[!UICONTROL 建议事件类型]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 已重命名为 [!UICONTROL 建议行动]. |
| （多个） | （多个） | 实验性质 [稳定在所有B2B组件上](https://github.com/adobe/xdm/pull/1617/files). |
| （多个） | （多个） | Adobe Journey Optimizer实体 [稳定](https://github.com/adobe/xdm/pull/1625/files). |
| （多个） | （多个） | 某些实验组件中特定字段的命名空间已 [更新了一致性](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## Identity Service {#identity-service}

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持删除数据集 | 现在，在通过 [目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、用户界面或数据卫生。 阅读 [删除UI中的数据集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以了解更多信息。 |

要了解有关Identity Service的更多信息，请阅读 [Identity Service概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| Audience Manager区段人口对实时客户资料的影响 | 首次使用Audience Manager源将Audience Manager区段发送到Platform时，大量Audience Manager区段人口的摄取会直接影响用户档案总数。 这意味着选择所有区段可能会导致用户档案计数超过您的许可证使用权限。 有关更多信息，请阅读 [Audience Manager源概述](../../sources/connectors/adobe-applications/audience-manager.md). 有关许可证使用情况的信息，请阅读 [使用许可证使用功能板](../../dashboards/guides/license-usage.md). |

要进一步了解来源，请阅读 [源概述](../../sources/home.md).