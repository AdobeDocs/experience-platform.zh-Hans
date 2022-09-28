---
title: Adobe Experience Platform发行说明2022年9月
description: 2022年9月版Adobe Experience Platform发行说明。
source-git-commit: 3d7a04c0ec6cf6a9bed90c9c22db2e8b56bfa01f
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 9 月 28 日**

Adobe Experience Platform的新增功能：

- [数据卫生](#data-hygiene)
- [[!UICONTROL 隐私控制台]](#privacy-console)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [审核日志](#audit-logs)
- [数据收集](#data-collection)
- [体验数据模型(XDM)](#xdm)
- [Identity Service](#identity-service)
- [源](#sources)

## 数据卫生 {#data-hygiene}

Adobe Experience Platform提供了一组功能强大的工具来管理大型、复杂的数据操作，以编排客户体验。 随着数据逐渐被摄取到系统中，管理数据存储变得越来越重要，这样数据就可以按预期使用，错误数据需要更正时会更新，组织策略认为有必要时会删除。

Adobe Experience Platform的数据卫生功能允许您通过计划自动数据集过期时间以及按身份以编程方式删除消费者数据来清除数据。

>[!NOTE]
>
>消费者删除功能仅适用于已购买Adobe医疗保健盾或隐私盾的组织。

请参阅以下文档，以开始使用数据卫生：

- [数据卫生概述](../../hygiene/home.md):了解有关Platform数据卫生功能的基础知识。
- [[!UICONTROL 数据卫生] UI指南](../../hygiene/ui/overview.md):了解如何在Platform用户界面中计划数据集过期和消费者删除请求。
- [数据卫生API指南](../../hygiene/api/overview.md):您可以在UI中执行的所有数据卫生活动也可以采用编程方式

## [!UICONTROL 隐私控制台] {#privacy-console}

的 [!UICONTROL 隐私控制台] Experience PlatformUI中的选项卡提供了一个功能板视图，其中提供了与隐私相关的功能(例如 [来自Privacy Service的数据主体请求], [数据卫生工作单]和 [审核日志]. 该控制台还提供了一些产品内用例指南，以帮助您完成常见的隐私工作流程。

请参阅 [隐私控制台概述](../../landing/governance-privacy-security/privacy-console.md) 以了解有关该功能的更多信息。

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服务使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的功能。 这允许营销分析人员使用业务级别配置来设置特定于公司需求的模型，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| --- | --- |
| 保存草稿实例 | 这项新功能使营销分析人员能够在配置期间将模型配置另存为草稿实例，并继续编辑草稿，直到完成后再进行培训和评分。 当用户在配置工作流中有多个字段需要定义，但无法一次完成时，或者当一个或多个数据集统计信息（如列完整性）需要时间才能使用时，此功能非常有用，包括但不限于以下情况：用户在配置工作流中有多个字段需要定义，无法一次完成； 阅读 [Attribution AI用户指南](../../intelligent-services/attribution-ai/user-guide.md) 以了解更多。 |
| 治理政策 | 在用户通过配置工作流提交以创建实例后，新策略实施服务会检查是否存在任何违反数据使用策略的情况，并在弹出窗口中显示详细信息。 它可确保数据操作和营销操作符合在Adobe Experience Platform上配置的数据使用策略。 |

有关Attribution AI的更多信息，请参阅 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md). 有关数据管理策略的信息，请阅读 [策略概述](../../data-governance/policies/overview.md).

### 客户人工智能

Real-time Customer Data Platform中提供的Customer AI用于生成自定义倾向得分，例如大规模单个用户档案的流失率和转化。

| 功能 | 描述 |
| --- | --- |
| 保存草稿实例 | 这项新功能使营销分析人员能够在配置期间将模型配置另存为草稿实例，并继续编辑草稿，直到完成后再进行培训和评分。 当用户在配置工作流中有多个字段需要定义，但无法一次完成时，或者当一个或多个数据集统计信息（如列完整性）需要时间才能使用时，此功能非常有用，包括但不限于以下情况：用户在配置工作流中有多个字段需要定义，无法一次完成； 阅读 [Customer AI用户指南](../../intelligent-services/customer-ai/user-guide/configure.md) 以了解更多。 |
| 治理政策 | 在用户通过配置工作流提交以创建实例后，新策略实施服务会检查是否存在任何违反数据使用策略的情况，并在弹出窗口中显示详细信息。 它可确保数据操作和营销操作符合在Adobe Experience Platform上配置的数据使用策略。 |

有关Customer AI的更多信息，请阅读 [Customer AI概述](../../intelligent-services/customer-ai/overview.md). 有关数据管理策略的信息，请阅读 [策略概述](../../data-governance/policies/overview.md).

## 审核日志 {#audit-logs}

Experience Platform允许您审核用户活动以获取各种服务和功能。 审核日志提供有关谁执行了操作以及何时执行的信息。

**更新功能**

| 功能 | 名称 | 描述 |
| --- | --- | --- |
| 已添加资源 | <ul><li>Attribution AI实例</li><li>Customer AI实例</li><li>数据流</li></ul> | 活动发生时，会自动记录审核日志资源。 如果启用了该功能，则无需手动启用日志收集。 |

{style=&quot;table-layout:auto&quot;}

有关平台中由审核日志跟踪的不同特定于资源的事件类型的更多信息，请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## 数据收集

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| Platform UI中的左侧导航集成 | 以前专用于数据收集UI的所有功能（包括标记、事件转发和数据流）现在也可通过Experience Platform中的左侧导航（位于类别下）使用 **[!UICONTROL 数据收集]**. 使用Platform中的数据收集功能时，无需在UI之间切换。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

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