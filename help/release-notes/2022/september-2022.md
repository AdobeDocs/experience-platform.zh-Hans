---
title: Adobe Experience Platform发行说明2022年9月
description: Adobe Experience Platform 2022年9月版发行说明。
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 4bdbb987905b6010f4b4f75bee060828d0e07368
workflow-type: tm+mt
source-wordcount: '2940'
ht-degree: 19%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 9 月 28 日**

Adobe Experience Platform中的新增功能：

- [基于属性的访问控制](#abac)

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [审核日志](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [身份服务](#identity-service)
- [查询服务](#query-service)
- [源](#sources)

## 基于属性的访问控制 {#abac}

>[!IMPORTANT]
>
>基于属性的访问控制将从2022年10月开始启用。 如果您希望成为率先采用者，请联系您的Adobe代表。

基于属性的访问控制是Adobe Experience Platform的一项功能，它使关注隐私的品牌在管理用户访问方面拥有更大的灵活性。 可以将各个对象（如架构字段和区段）分配给用户角色。 通过此功能，您可以授予或撤销组织中特定Platform用户对各个对象的访问权限。

通过基于属性的访问控制，贵组织的管理员可以控制用户对所有平台工作流和资源中敏感个人数据(SPD)、个人身份信息(PII)和其他自定义类型数据的访问。 管理员可以定义仅有权访问特定字段的用户角色以及与这些字段对应的数据的用户角色。

| 功能 | 描述 |
| --- | --- |
| 基于属性的访问控制 | 基于属性的访问控制允许您使用定义组织或数据使用范围的标签来标记体验数据模型(XDM)架构字段和区段。 同时，管理员可以使用用户和角色管理界面定义涵盖XDM架构字段和区段的访问策略，以便更好地管理授予用户或用户组（内部、外部或第三方用户）的访问权限。 欲了解更多信息，请参见 [基于属性的访问控制概述](../../access-control/abac/overview.md). |
| 权限 | 权限是Experience Cloud的区域，管理员可以在其中定义用户角色和访问策略，以管理产品应用程序内功能和对象的访问权限。 通过权限，您可以创建和管理角色、为这些角色分配所需的资源权限，以及构建策略以利用标签并定义哪些用户角色有权访问特定Platform资源。 权限还允许您管理与特定角色关联的标签、沙盒和用户。欲了解更多信息，请参见 [权限UI指南](../../access-control/abac/ui/browse.md). |

有关基于属性的访问控制的详细信息，请参见 [基于属性的访问控制概述](../../access-control/abac/overview.md). 有关基于属性的访问控制工作流的全面指南，请阅读 [基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服务使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 这样，营销分析人员就可以使用业务级别配置来设置特定于公司需求的模型，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户历程中每个营销接触点的营销影响。

| 功能 | 描述 |
| --- | --- |
| 保存草稿实例 | 借助此新功能，营销分析人员可以将模型配置另存为草稿实例，并继续编辑直到训练和评分前完成。 此功能有用的情况包括：用户在工作流中有多个要定义的字段，但由于时间限制无法完成它。 另一种情况是当一个或多个数据集统计信息正在处理中但尚未可用时。 阅读 [Attribution AI用户指南](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 了解更多信息。 |
| 治理策略 | 用户通过配置工作流提交以创建实例后，新的策略实施服务会检查是否存在任何违反数据使用的策略，并在弹出窗口中显示详细信息。 它确保数据操作和营销操作符合Adobe Experience Platform上配置的数据使用策略。 |

欲了解有关Attribution AI的更多信息，请参见 [Attribution AI概述](../../intelligent-services/attribution-ai/overview.md). 有关数据治理策略的信息，请阅读 [策略概述](../../data-governance/policies/overview.md).

### 客户人工智能

Real-time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，例如大规模单个用户档案的流失和转化率。

| 功能 | 描述 |
| --- | --- |
| 保存草稿实例 | 借助此新功能，营销分析人员可以将模型配置另存为草稿实例，并继续编辑直到训练和评分前完成。 此功能有用的情况包括：用户在工作流中有多个要定义的字段，但由于时间限制无法完成它。 另一种情况是当一个或多个数据集统计信息正在处理中但尚未可用时。 阅读 [Customer AI用户指南](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 了解更多信息。 |
| 治理策略 | 用户通过配置工作流提交以创建实例后，新的策略实施服务会检查是否存在任何违反数据使用的策略，并在弹出窗口中显示详细信息。 它确保数据操作和营销操作符合Adobe Experience Platform上配置的数据使用策略。 |

有关客户人工智能的更多信息，请阅读 [Customer AI概述](../../intelligent-services/customer-ai/overview.md). 有关数据治理策略的信息，请阅读 [策略概述](../../data-governance/policies/overview.md).

## 审核日志 {#audit-logs}

Experience Platform允许您审核各种服务和功能的用户活动。 审核日志提供有关谁在什么时候做了哪些事情的信息。

**更新的功能**

| 功能 | 名称 | 描述 |
| --- | --- | --- |
| 已添加资源 | <ul><li>Attribution AI实例</li><li>客户人工智能实例</li><li>数据流</li></ul> | 审计日志资源在活动发生时自动记录。 如果启用了此功能，则无需手动启用日志收集。 |

{style="table-layout:auto"}

有关Platform中由审核日志跟踪的不同特定于资源的事件类型的更多信息，请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

| 功能 | 描述 |
| --- | --- |
| 使用中标签 | 在Widget库中查看时，使用中标签可以轻松识别仪表板中现有构件是否存在。 这样可以轻松避免重复，不过您仍然可以根据需要多次添加同一构件。 |
| 用户定义的仪表板 | 通过允许您构建和管理自定义仪表板，用户定义的仪表板有助于加快洞察和自定义可视化图表。 通过用户定义的仪表板，您可以创建、添加和编辑定制的小部件，以可视化与您的组织相关的关键量度。 阅读 [功能指南](../../dashboards/user-defined-dashboards.md) 了解更多信息。 |
| 客户数据平台分析数据模型 | 客户数据平台(CDP)分析数据模型功能可公开为各种用户档案、目标和分段构件提供分析功能的数据模型和SQL。 您可以自定义这些SQL查询模板，以便为您的营销和关键绩效指标用例创建CDP报表。 这些见解随后可用作用户定义的功能板的自定义构件。 阅读 [CDP Insights数据模型功能指南](../../dashboards/cdp-insights-data-model.md) 了解更多信息。 |
| 受众重叠报表构件 | 此构件可用于两者 [!UICONTROL 配置文件] 和 [!UICONTROL 区段] 功能板。 此报表按所选区段的最高或最低重叠百分比排名的有序受众列表。 从 [!UICONTROL 配置文件] 仪表板您可以按合并策略从所有可用区段中过滤和查看受众重叠。 此 [!UICONTROL 区段] 利用功能板，可按特定区段筛选受众重叠。<br>使用此分析构建新的、高性能区段，并避免将相同的受众发送到不同的目标。 报表还有助于识别隐藏的洞察信息以改进分段或找到要追求的独特用户档案。 阅读相应的 [用户档案](../../dashboards/guides/profiles.md#audience-overlap-report) 和 [区段](../../dashboards/guides/audiences.md#audience-overlap-report) 构件指南，以了解更多信息。 |

有关的详细信息 [!DNL Dashboards]，请参阅 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Platform UI中的左侧导航集成 | 之前专用于数据收集UI的所有功能（包括标记、事件转发和数据流）现在也可通过左侧导航中的Experience Platform类别下使用 **[!UICONTROL 数据收集]**. 当在Platform中使用数据收集功能时，无需在UI之间切换。 |
| 标记中的用户归因和事件转发 | 当列表可用时 [!UICONTROL 属性] 在标记和事件转发中，每个列出的属性现在会显示其上次更新时间以及进行更新的用户。 |
| [[!DNL Snap Conversions API] 扩展](https://exchange.adobe.com/apps/ec/108550) 用于事件转发 | 您现在可以将数据发送到 [!DNL Snapchat Conversions API] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 有关如何验证和使用API的更多信息，请参阅 [[!DNL Snapchat Marketing API] 文档](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] 在Web SDK中](../../edge/fundamentals/user-agent-client-hints.md) | Web SDK现在支持 [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 客户端提示允许网站所有者访问 [!DNL User-Agent] 字符串，但采用更保护隐私的方式。 |
| [Web SDK逐页迁移](../../edge/home.md#migrating-to-web-sdk) | 您现在可以从其他Experience Cloud库中迁移现有Web资产，例如 [!DNL at.js]，转到Web SDK，一次显示一个页面。 这支持分阶段进行Web SDK迁移，而无需一次迁移所有页面。 |
| [[!DNL Adobe Journey Optimizer] 支持数据流](../../edge/datastreams/overview.md#aep) | 适用于数据流的Adobe Experience Platform服务现在支持 [!DNL Adobe Journey Optimizer]. 此选项允许您在中使用基于Web和应用程序的入站渠道 [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 目标 SDK | Destination SDK现在为创建批量（或基于文件）生产目的地或专用目的地的合作伙伴和客户提供全面支持。 有关更多信息，请阅读以下文档页面： <ul><li>[Destination SDK概述](../../destinations/destination-sdk/overview.md)</li><li>[配置基于文件的目标](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[为基于文件的目标配置文件格式选项](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[测试您的基于文件的目标](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**新增或更新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services提供了跨渠道客户体验设计平台，并为可视化的活动编排、实时互动管理和跨渠道执行提供了环境。 [Campaign入门](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). 请注意，此集成可与 [Adobe Campaign版本8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 此 [!DNL Salesforce CRM] 目标已更新，可支持联系人和潜在客户更新，以及性能改进，以实现更快的更新。 |

{style="table-layout:auto"}

**新增或更新文档**

| 文档 | 描述 |
| ----------- | ----------- |
| 目标流服务API文档 | 此 [目标API参考文档](https://developer.adobe.com/experience-platform-apis/references/destinations/) 更新了内容，以包括关于如何对基于文件的目标执行操作的指导。 稍后将添加流目标的操作。 |

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| UI支持枚举和建议值 | 除了启用数据验证的枚举之外，您现在还可以 [添加或删除建议值](../../xdm/ui/fields/enum.md) 用于标准或自定义字符串字段，以便Platform用户可在创建区段时从中选择一个友好的值列表。 |

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL AJO分类字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 与交互导致建议事件触发的特定元素的属性。 |
| 字段组 | [[!UICONTROL MediaAnalytics 交互详情]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 随时间跟踪媒体交互。 |
| 字段组 | [[!UICONTROL 媒体详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 跟踪媒体详细信息。 |
| 字段组 | [[!UICONTROL AdobeCJM ExperienceEvent — 表面]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | 描述Adobe Journey Optimizer中体验事件的表面。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 行为 | [[!UICONTROL 时间序列]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>已添加以下项的值： `eventType`：<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>已移除以下项的值： `eventType`：<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 字段组 | （多种） | [更新了多个字段描述](https://github.com/adobe/xdm/pull/1628/files) 跨Journey Orchestration组件。 |
| 字段组 | （多种） | [更新了多个Adobe Workfront组件的标题](https://github.com/adobe/xdm/pull/1634/files) 以保持一致性。 |
| 字段组 | [[!UICONTROL AJO分类字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 已将多个字段的命名空间更新为 `xdm`. |
| 字段组 | [[!UICONTROL Journey Orchestration步骤事件常用字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 添加了一个新字段， `isReadSegmentTriggerStartEvent`. |
| 字段组 | [[!UICONTROL 天气预报]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 已更改 `xdm:uvIndex` 字段中的任意值，并将 `xdm` 名称空间到缺少的多个字段。 |
| 字段组 | [[!UICONTROL 媒体详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 和 `xdm:implementationDetails` 已从字段组删除。 |
| 数据类型 | （多种） | [更新了多个媒体属性名称](https://github.com/adobe/xdm/pull/1626/files) 跨多种数据类型实现一致性。 |
| 数据类型 | [[!UICONTROL 实施详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 添加了颤振的已知名称。 |
| 数据类型 | [[!UICONTROL 兴趣点详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 数据类型现在可以接受与目标点关联的元数据键值对列表。 |
| 数据类型 | [[!UICONTROL 建议操作]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 已重命名为 [!UICONTROL 建议操作]. |
| 数据类型 | [[!UICONTROL 建议事件类型]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 已重命名为 [!UICONTROL 建议操作]. |
| （多种） | （多种） | 实验性能已经达到 [在所有B2B组件中稳定](https://github.com/adobe/xdm/pull/1617/files). |
| （多种） | （多种） | Adobe Journey Optimizer实体已 [已稳定](https://github.com/adobe/xdm/pull/1625/files). |
| （多种） | （多种） | 某些字段的命名空间跨多个实验组件 [已更新以保持一致性](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

有关 Platform 中 XDM 的详细信息，请查看 [XDM 系统概述](../../xdm/home.md)。

## 身份服务 {#identity-service}

提供相关的数字体验需要全面了解您的客户。 当您的客户数据分散在不同的系统上，导致每个客户似乎都有多个“身份”时，这会使问题变得更加困难。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持数据集删除 | 现在，Identity Service在通过 [目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或数据卫生。 阅读以下内容中的指南： [在UI中删除数据集](../../catalog/datasets/user-guide.md#delete-a-dataset) 了解更多信息。 |

要了解有关身份服务的更多信息，请阅读[身份服务概述](../../identity-service/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以从以下位置连接任何数据集 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 警报订阅API | Adobe Experience Platform查询服务允许您为临时查询和计划查询订阅警报。 警报可以通过电子邮件和/或Platform UI接收。 目前，查询警报只能使用订阅 [查询服务API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| 数据集样本 | 查询服务数据集示例使您能够针对大数据执行探索性查询，并显着减少处理时间，而代价是查询准确性。 请参阅 [数据集示例指南](../../query-service/essential-concepts/dataset-samples.md) 了解更多信息。 |

有关的详细信息 [!DNL Query Service]，请参阅 [[!DNL Query Service] 概述](../../query-service/home.md).

请参阅 [查询警报文档](../../query-service/api/alert-subscriptions.md) 了解更多信息。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Audience Manager区段人口对实时客户个人资料的影响 | 当您首次使用Audience Manager源向Platform发送Audience Manager区段时，大量的Audience Manager区段群体的摄取会直接影响您的总配置文件计数。 这意味着选择所有区段可能会导致配置文件计数超过您的许可证使用授权。 有关详细信息，请阅读 [Audience Manager源概述](../../sources/connectors/adobe-applications/audience-manager.md). 有关许可证使用情况的信息，请阅读以下文档： [使用许可证使用情况仪表板](../../dashboards/guides/license-usage.md). |
| 支持Adobe Campaign托管Cloud Service | 使用Adobe Campaign托管Cloud Service源将Adobe Campaign v8.4投放和跟踪日志数据引入Experience Platform。 阅读以下内容中的指南： [在UI中创建Adobe Campaign托管Cloud Service源连接](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 了解更多信息。 |
| API支持批量来源的按需摄取 | 使用按需引入为给定数据流创建临时流运行，使用 [!DNL Flow Service] API。 创建的流运行必须设置为一次性摄取。 有关详细信息，请阅读以下指南： [使用API为按需引入创建流运行](../../sources/tutorials/api/on-demand-ingestion.md) 了解更多信息。 |
| API支持重试批处理源的失败数据流运行 | 使用 `re-trigger` 操作，以通过API重试失败的数据流。 阅读以下内容中的指南： [使用API重试失败的数据流运行](../../sources/tutorials/api/retry-flows.md) 了解更多信息。 |
| API支持筛选的行级别数据 [!DNL Google BigQuery] 和 [!DNL Snowflake] 源 | 使用逻辑运算符和比较运算符筛选 [!DNL Google BigQuery] 和 [!DNL Snowflake] 源。 有关更多信息，请阅读[使用 API 过滤源数据](../../sources/tutorials/api/filter.md)的指南。 |

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
