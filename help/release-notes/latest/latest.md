---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
source-git-commit: bbc9df59f91b6de12e902a71f7b9d054735cad7b
workflow-type: tm+mt
source-wordcount: '3079'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 9 月 28 日**

Adobe Experience Platform的新增功能：

- [基于属性的访问控制](#abac)
- [数据卫生](#data-hygiene)
- [[!UICONTROL 隐私控制台]](#privacy-console)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [审核日志](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [数据收集](#data-collection)
- [目标](#destinations)
- [体验数据模型(XDM)](#xdm)
- [Identity Service](#identity-service)
- [查询服务](#query-service)
- [源](#sources)

## 基于属性的访问控制 {#abac}

>[!IMPORTANT]
>
>从2022年10月起，将启用基于属性的访问控制。 如果您希望成为早期收养者，请联系您的Adobe代表。

基于属性的访问控制是Adobe Experience Platform的一项功能，它为具有隐私意识的品牌提供了更大的灵活性来管理用户访问权限。 可以将单个对象（如架构字段和区段）分配给用户角色。 此功能允许您为组织中的特定Platform用户授予或撤消对单个对象的访问权限。

通过基于属性的访问控制，贵组织的管理员可以控制用户对所有平台工作流和资源中敏感个人数据(SPD)、个人身份信息(PII)和其他自定义类型数据的访问。 管理员可以定义用户角色，这些用户角色只能访问与这些字段对应的特定字段和数据。

| 功能 | 描述 |
| --- | --- |
| 基于属性的访问控制 | 基于属性的访问控制允许您为体验数据模型(XDM)架构字段和区段设置标签，以定义组织或数据使用范围。 同时，管理员可以使用用户和角色管理界面来定义涵盖XDM架构字段和区段的访问策略，以更好地管理提供给用户或组（内部、外部或第三方用户）的访问。 有关更多信息，请参阅 [基于属性的访问控制概述](../../access-control/abac/overview.md). |
| 权限 | 权限是Experience Cloud区域，管理员可以在其中定义用户角色和访问策略，以管理产品应用程序中功能和对象的访问权限。 通过“权限”，您可以创建和管理角色，为这些角色分配所需的资源权限，以及构建策略以利用标签并定义哪些用户角色有权访问特定的Platform资源。 权限还允许您管理与特定角色关联的标签、沙箱和用户。 有关更多信息，请参阅 [权限UI指南](../../access-control/abac/ui/browse.md). |

有关基于属性的访问控制的详细信息，请参阅 [基于属性的访问控制概述](../../access-control/abac/overview.md). 有关基于属性的访问控制工作流的全面指南，请阅读 [基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md).

## 数据卫生 {#data-hygiene}

Adobe Experience Platform提供了一组功能强大的工具来管理大型、复杂的数据操作，以编排客户体验。 随着数据逐渐被摄取到系统中，管理数据存储变得越来越重要，这样数据就可以按预期使用，错误数据需要更正时会更新，组织策略认为有必要时会删除。

Adobe Experience Platform的数据卫生功能允许您通过计划自动数据集过期时间以及按身份以编程方式删除消费者数据来清除数据。

>[!IMPORTANT]
>
>数据卫生功能仅适用于已购买Adobe医疗保健盾或隐私盾的组织。

请参阅以下文档，以开始使用数据卫生：

- [数据卫生概述](../../hygiene/home.md):了解有关Platform数据卫生功能的基础知识。
- [[!UICONTROL 数据卫生] UI指南](../../hygiene/ui/overview.md):了解如何在Platform用户界面中计划数据集过期和消费者删除请求。
- [数据卫生API指南](../../hygiene/api/overview.md):您可以在UI中执行的所有数据卫生活动也可以采用编程方式

## [!UICONTROL 隐私控制台] {#privacy-console}

的 [!UICONTROL 隐私控制台] Experience PlatformUI中的选项卡提供了一个功能板视图，其中提供了与隐私相关的功能(例如 [来自Privacy Service的数据主体请求](../../privacy-service/home.md), [数据卫生工作单](../../hygiene/home.md)和 [审核日志](../../landing/governance-privacy-security/audit-logs/overview.md). 该控制台还提供了一些产品内用例指南，以帮助您完成常见的隐私工作流程。

请参阅 [隐私控制台概述](../../landing/governance-privacy-security/privacy-console.md) 以了解有关该功能的更多信息。

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服务使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的功能。 这允许营销分析人员使用业务级别配置来设置特定于公司需求的模型，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| --- | --- |
| 保存草稿实例 | 这项新功能使营销分析人员能够将模型配置另存为草稿实例，并继续对其进行编辑，直到在培训和评分之前模型配置完成为止。 当用户在工作流中有多个要定义的字段，但由于时间限制而无法完成时，此功能会很有帮助。 另一种情况是，一个或多个数据集统计信息正在处理中，但尚未可用。 阅读 [Attribution AI用户指南](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 以了解更多。 |
| 治理政策 | 在用户通过配置工作流提交以创建实例后，新策略实施服务会检查是否存在任何违反数据使用策略的情况，并在弹出窗口中显示详细信息。 它可确保数据操作和营销操作符合在Adobe Experience Platform上配置的数据使用策略。 |

有关Attribution AI的更多信息，请参阅 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md). 有关数据管理策略的信息，请阅读 [策略概述](../../data-governance/policies/overview.md).

### 客户人工智能

Real-time Customer Data Platform中提供的Customer AI用于生成自定义倾向得分，例如大规模单个用户档案的流失率和转化。

| 功能 | 描述 |
| --- | --- |
| 保存草稿实例 | 这项新功能使营销分析人员能够将模型配置另存为草稿实例，并继续对其进行编辑，直到在培训和评分之前模型配置完成为止。 当用户在工作流中有多个要定义的字段，但由于时间限制而无法完成时，此功能会很有帮助。 另一种情况是，一个或多个数据集统计信息正在处理中，但尚未可用。 阅读 [Customer AI用户指南](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 以了解更多。 |
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

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关组织数据的重要分析（在每日快照中捕获）。

| 功能 | 描述 |
| --- | --- |
| 使用中标签 | 在小组件库中查看时，使用中的标签可轻松识别功能板中是否存在现有小组件。 这样可以轻松避免重复，不过您仍可以根据需要多次添加同一小组件。 |
| 用户定义的功能板 | 用户定义的功能板使您能够构建和管理自定义功能板，从而帮助加快分析和自定义可视化。 借助用户定义的功能板，您可以创建、添加和编辑定制小组件，以可视化与您的组织相关的关键量度。 阅读 [功能指南](../../dashboards/user-defined-dashboards.md) 以了解更多。 |
| 客户数据平台分析数据模型 | 客户数据平台(CDP)分析数据模型功能公开了数据模型和SQL，它们为各种配置文件、目标和分段小组件提供了分析支持。 您可以自定义这些SQL查询模板，以便为您的营销和关键绩效指标用例创建CDP报告。 然后，这些分析可用作用户定义的功能板的自定义小组件。 阅读 [CDP Insights Data Model功能指南](../../dashboards/cdp-insights-data-model.md) 以了解更多。 |
| 受众重叠报表小组件 | 此小组件可同时用于这两个组件 [!UICONTROL 用户档案] 和 [!UICONTROL 区段] 功能板。 报表提供按所选区段的重叠百分比最高或最低排名的受众的有序列表。 从 [!UICONTROL 用户档案] 功能板中，您可以通过从所有可用区段中合并策略来过滤和查看受众重叠。 的 [!UICONTROL 区段] 功能板允许您按特定区段过滤受众重叠。<br>使用此分析可构建新的高性能区段，并避免向不同目标发送相同的受众。 此报表还有助于识别隐藏的分析，以改进分段或查找要查找的独特用户档案。 |

有关 [!DNL Dashboards]，请参阅 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| Platform UI中的左侧导航集成 | 以前专用于数据收集UI的所有功能（包括标记、事件转发和数据流）现在也可通过Experience Platform中的左侧导航（位于类别下）使用 **[!UICONTROL 数据收集]**. 使用Platform中的数据收集功能时，无需在UI之间切换。 |
| 标记和事件转发中的用户归因 | 列表可用时 [!UICONTROL 属性] 在标记和事件转发中，每个列出的属性现在都会显示上次更新的时间以及进行更新的用户。 |
| [[!DNL User-Agent Client Hints] 在Web SDK中](../../edge/fundamentals/user-agent-client-hints.md) | Web SDK现在支持 [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 客户端提示允许网站所有者访问 [!DNL User-Agent] 字符串，但更能保护隐私。 |
| [逐页迁移Web SDK](../../edge/home.md#migrating-to-web-sdk) | 您现在可以从其他Experience Cloud库迁移现有Web资产，例如 [!DNL at.js]，到Web SDK，每次一个页面。 这支持分阶段迁移Web SDK的方法，而无需同时迁移您的所有页面。 |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 目标 SDK | Destination SDK现在为创建批量（或基于文件）产品化或专用目标的合作伙伴和客户提供完全支持。 有关更多信息，请阅读以下文档页面： <ul><li>[Destination SDK概述](/help/destinations/destination-sdk/overview.md)</li><li>[配置基于文件的目标](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[为基于文件的目标配置文件格式选项](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[测试基于文件的目标](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**新目标或更新的目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services提供了一个平台，用于设计跨渠道客户体验以及可视活动编排、实时交互管理和跨渠道执行的环境。 [Campaign快速入门](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 的 [!DNL Salesforce CRM] 目标已更新，可支持联系人和潜在客户更新以及性能改进，以便更快更新。 |

{style=&quot;table-layout:auto&quot;}

**新文档或更新的文档**

| 文档 | 描述 |
| ----------- | ----------- |
| 目标流服务API文档 | 的 [目标API参考文档](https://developer.adobe.com/experience-platform-apis/references/destinations/) 更新了，以包含有关如何对基于文件的目标执行操作的指导。 将在以后添加流目标的操作。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

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

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以连接 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、Data Science Workspace或摄取到实时客户资料。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 警报订阅API | Adobe Experience Platform查询服务允许您订阅临时查询和计划查询的警报。 警报可通过电子邮件、在Platform UI中或同时通过两者接收。 目前，查询警报只能使用 [查询服务API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| 数据集示例 | 查询服务数据集示例使您能够对大数据进行探索性查询，并大大缩短了处理时间，同时也降低了查询准确性。 |

有关 [!DNL Query Service]，请参阅 [[!DNL Query Service] 概述](../../query-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| Audience Manager区段人口对实时客户资料的影响 | 首次使用Audience Manager源将Audience Manager区段发送到Platform时，大量Audience Manager区段人口的摄取会直接影响用户档案总数。 这意味着选择所有区段可能会导致用户档案计数超过您的许可证使用权限。 有关更多信息，请阅读 [Audience Manager源概述](../../sources/connectors/adobe-applications/audience-manager.md). 有关许可证使用情况的信息，请阅读 [使用许可证使用功能板](../../dashboards/guides/license-usage.md). |
| 支持Adobe Campaign托管Cloud Service | 使用Adobe Campaign托管Cloud Service源将Adobe Campaign v8.4投放和跟踪日志数据Experience Platform。 阅读 [在UI中创建Adobe Campaign托管Cloud Service源连接](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 以了解更多信息。 |
| 支持批量源的按需摄取API | 使用按需摄取，通过 [!DNL Flow Service] API。 创建的流量运行必须设置为一次性摄取。 有关更多信息，请阅读 [使用API为按需摄取创建流程运行](../../sources/tutorials/api/on-demand-ingestion.md) 以了解更多信息。 |
| 支持为批处理源重试失败的数据流运行的API | 使用 `re-trigger` 通过API重试失败的数据流的操作。 阅读 [正在使用API重试失败的数据流运行](../../sources/tutorials/api/retry-flows.md) 以了解更多信息。 |
| 支持过滤 [!DNL Google BigQuery] 和 [!DNL Snowflake] 来源 | 使用逻辑运算符和比较运算符来筛选 [!DNL Google BigQuery] 和 [!DNL Snowflake] 来源。 阅读 [使用API过滤源的数据](../../sources/tutorials/api/filter.md) 以了解更多信息。 |

要进一步了解来源，请阅读 [源概述](../../sources/home.md).