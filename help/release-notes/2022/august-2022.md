---
title: Adobe Experience Platform 发行说明（2022 年 8 月）
description: Adobe Experience Platform 的 2022 年 8 月发行说明。
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 26%

---

# Adobe Experience Platform 发行说明

**发行日期： 2022年8月24日**

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [实时客户轮廓](#profile)
- [Segmentation Service](#segmentation)
- [源](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服务使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 这允许营销分析人员使用业务级配置来设置特定于公司需求的模型，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户历程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 隐私支持 | <ul><li> 归因人工智能现在支持定义用户角色和访问策略，以管理产品应用程序内功能和对象的[权限](../../../help/access-control/abac/ui/permissions.md)。 </li><li>活动发生时，将自动记录审核日志资源。</li><li> 通过[基于属性的访问控制](../../access-control/abac/overview.md)，管理员可以控制对特定对象和/或基于特定属性的权能的访问，这些特定属性可以是添加到对象的元数据，如标签。管理员还可以定义用户角色，该角色只能访问特定字段以及与这些字段对应的数据。</li><li>归因人工智能利用Experience Platform数据集。 为了支持品牌可能收到的消费者权限请求，品牌应使用Experience Platform Privacy Service提交消费者访问和删除请求，以通过数据湖、身份服务和实时客户配置文件删除他们的数据。  </li><li>所有用于模型输入/输出的数据集将遵循Experience Platform准则。 Experience Platform数据加密适用于静态和传输中的数据。 请参阅文档以了解有关[数据加密](../../../help/landing/governance-privacy-security/encryption.md)的更多信息。</li></ul> |

{style="table-layout:auto"}

**注意**：在进一步通知之前，现有Healthcare Shield客户将无法使用归因人工智能。

有关归因人工智能的更多信息，请参阅[归因人工智能](../../intelligent-services/attribution-ai/overview.md)概述。

### 客户人工智能

Real-Time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，例如大规模单个用户档案的流失和转化率。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 隐私支持 | <ul><li> Customer AI现在支持定义用户角色和访问策略，以管理产品应用程序内功能和对象的[权限](../../../help/access-control/abac/ui/permissions.md)。 </li><li>活动发生时，将自动记录审核日志资源。</li><li> 通过[基于属性的访问控制](../../access-control/abac/overview.md)，管理员可以根据特定属性控制对特定对象和/或权能的访问。 这些属性可以是添加到对象的元数据，如标签。管理员还可以定义用户角色，使其仅有权访问特定字段和对应于这些字段的数据。</li><li>客户人工智能利用Experience Platform数据集。 为了支持品牌可能收到的消费者权限请求，品牌应使用Experience Platform Privacy Service提交消费者访问和删除请求，以通过数据湖、身份服务和实时客户配置文件删除他们的数据。 </li><li>所有用于模型输入/输出的数据集将遵循Experience Platform准则。 Experience Platform数据加密适用于静态和传输中的数据。 请参阅文档以了解有关[数据加密](../../../help/landing/governance-privacy-security/encryption.md)的更多信息。</li></ul> |

{style="table-layout:auto"}

**注意**：在进一步通知之前，现有Healthcare Shield客户将无法使用客户人工智能。

有关客户人工智能的更多信息，请参阅[客户人工智能](../../intelligent-services/customer-ai/overview.md)概述。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供了多个[!DNL dashboards]，通过它们可以查看有关贵组织数据的重要见解，如在每日快照期间捕获的数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 计划的激活构件 | [!UICONTROL 计划的激活]构件提供最近激活的目标的列表化视图。 对于每个区段，它包括名称、目标平台以及激活开始和结束日期。 利用此小组件，可快速发现激活受众的位置和时间，并使重复或不必要的激活更加透明。 此累积信息还突出显示任何激活被排除在外的位置。 |

有关 [!DNL Dashboards] 的详细信息，请查看 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持摄取有警告的记录 | 数据准备现在将警告（非严重错误）本地化到字段，并允许摄取行的其余部分。 现在，所有映射器转换错误都会报告为警告，而部分摄取的行会被视为成功，并带有警告。  具有警告和诊断详细信息的记录也支持监视。 部分摄取有警告的记录当前仅适用于流式传输数据。 查看有关[引入带有警告的记录](../../sources/tutorials/ui/monitor-streaming.md)的文档以了解更多信息。 |

{style="table-layout:auto"}

要了解有关[!DNL Data Prep]的更多信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ----------- | ----------- |
| (Beta)对个性化目标的基于属性的个性化支持 | 随着基于属性的个性化测试版的发布，您将在[目标目录](../../destinations/catalog/overview.md)中看到两张新卡片： <ul><li>**[!UICONTROL Adobe Target V2]**：此连接器当前为测试版，仅对部分客户可用。 除了Adobe Target V1信息卡提供的功能之外，Target V2连接器还向激活工作流中添加了[映射步骤](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes)，该步骤允许您将配置文件属性映射到Adobe Target，从而实现基于属性的同页和下一页个性化。</li><li>**[!UICONTROL 具有属性的自定义Personalization]**：此连接器当前为测试版，仅对部分客户可用。 除了&#x200B;**[!UICONTROL 自定义Personalization]**&#x200B;提供的功能外，**[!UICONTROL 具有属性的自定义Personalization]**&#x200B;连接器还向激活工作流中添加了一个可选的[映射步骤](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes)，该步骤允许您将配置文件属性映射到自定义个性化目标，从而启用基于属性的同一页面和下一页面个性化。</li></ul> <br>配置文件属性可能包含敏感数据。 为了保护此数据，**[!UICONTROL 具有属性的自定义Personalization]**&#x200B;目标要求您使用[Edge Network服务器API](../../server-api/overview.md)进行数据收集。 此外，所有服务器API调用必须在[经过身份验证的上下文](../../server-api/authentication.md)中进行。 |

{style="table-layout:auto"}

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/)是Sales Execution Experience Platform，拥有世界上最丰富的B2B买方与卖方交互数据，并在专有人工智能技术方面投入了大量资金，以将销售数据转换为智能。 [!DNL Outreach]帮助企业自动执行销售活动并根据收入情报采取行动，以提高其效率、可预测性和增长。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL AJO实体类]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | 基于记录的类，用于为Adobe Journey Optimizer创建查找架构。 |
| 字段组 | [[!UICONTROL Workfront工作对象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | 一个包装字段组，它引用Adobe Workfront的所有较低级别的特定于对象的字段组。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL Journey Orchestration步骤事件常用字段]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 已添加两个新属性：`origTimeStamp`和`experienceID`。 |
| 字段组 | [[!UICONTROL 区段成员关系详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 除了[!UICONTROL XDM个人资料]之外，此字段组现在还可用于基于XDM业务帐户类的架构中。 |
| 字段组 | （多种） | 多个与Marketo B2B活动相关的字段组已更新为稳定状态。 有关详细信息，请参阅以下[拉取请求](https://github.com/adobe/xdm/pull/1593/files)。 |
| 字段组 | （多种） | 已更新多个与天气相关的字段组，以修复`uvIndex`和`sunsetTime`发生的错误。 有关详细信息，请参阅以下[拉取请求](https://github.com/adobe/xdm/pull/1602/files)。 |
| 数据类型 | [[!UICONTROL 产品列表项目]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 已添加新属性`productImageUrl`。 |
| 数据类型 | [[!UICONTROL Qoe 数据详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 已添加新属性`framesPerSecond`。 |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` 已更名为 `appVersion`。`meta:enum`和`description`字段也已更新。 |
| 数据类型和字段组 | （多种） | 多个媒体数据类型和字段组都有新字段和更新的描述。 有关详细信息，请参阅以下[拉取请求](https://github.com/adobe/xdm/pull/1582/files)。 |
| （全部） | （多种） | 现在包含`enum`字段的所有架构对象也包含相应的`meta:enum`字段，以表示每个约束的显示值。 有关详细信息，请参阅以下[拉取请求](https://github.com/adobe/xdm/pull/1601/files)。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。轮廓允许您将客户数据整合到一个统一视图中，并为每一次客户交互提供可操作的、有时间戳的描述。

| 功能 | 描述 |
| ------- | ----------- |
| 合并策略硬性限制 | Experience Platform现在将强制每个沙盒实施&#x200B;**5个**&#x200B;合并策略的硬性限制。 如果您的沙盒当前具有超过五个合并策略，则在该沙盒具有少于五个合并策略之前，您&#x200B;**无法**&#x200B;创建新的合并策略。 |
| 孤立的配置文件边缘属性清理 | 对于所有组织，配置文件服务现在每天都会删除用户活动区域的剩余边缘属性，以便更准确地表示您系统中的配置文件。 此清理在删除给定配置文件的所有配置文件片段之后发生，并且应该影响从将`com_adobe_aep_profile_region_dataset`标记为`true`的数据集中合并的配置文件。 这可能显示在许可证使用情况仪表板中的“可寻址受众”量度下降，也可能显示在配置文件仪表板中的“配置文件计数”量度下降，因为这些量度包含此版本之前的剩余边缘属性片段。 |

{style="table-layout:auto"}

要详细了解实时客户轮廓，包括使用轮廓数据的教程和最佳实践，请首先阅读[实时客户轮廓概述](../../profile/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持4000个区段 | 现在，所有具有Experience Platform的组织最多可支持4000个区段定义。 有关此更改如何影响区段作业API的更多信息，请阅读[区段作业终结点指南](../../segmentation/api/segment-jobs.md) |

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自助服务源的正式发布(批处理SDK) | 开发、测试和集成基于REST API的数据源，以通过易于配置的源规范将批量数据摄取到Experience Platform中。 通过源SDK，您可以： <ul><li>配置Experience Platform目录的新源。</li><li>定义源的规范，包括与支持的身份验证类型、计划以及如何获取资源数据相关的信息。</li><li>为新源创建面向用户的文档。</li></ul> 有关详细信息，请阅读有关[自助源(批处理SDK)](../../sources/sources-sdk/overview.md)的文档。 |
| [!DNL Google BigQuery] 源全面可用 | 使用[!DNL Google BigQuery]源将数据从[!DNL Google BigQuery]数据仓库摄取到Experience Platform。 有关详细信息，请参阅[[!DNL Google BigQuery] 源](../../sources/connectors/databases/bigquery.md)上的文档。 |
| [!DNL Teradata Vantage]源(Beta) | 使用[!DNL Teradata Vantage]源将数据从混合多云环境摄取到Experience Platform。 有关详细信息，请参阅[[!DNL Teradata Vantage] 源](../../sources/connectors/databases/teradata-vantage.md)上的文档。 |
| 对Adobe Analytics源的跨区域支持 | 您现在可以从任何区域（美国、英国或新加坡）摄取报告包。 必须将报表包映射到与在中创建源连接的Experience Platform沙盒实例相同的组织。 有关详细信息，请参阅[在UI中创建Adobe Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md)指南。 |

{style="table-layout:auto"}

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
