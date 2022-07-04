---
title: Adobe Experience Platform发行说明2022年4月
description: 2022年4月的Adobe Experience Platform发行说明。
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 6798c15b1cee781c41b9faf5cc6dcfa73090a60a
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 4 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [数据流](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [目标](#destinations)
- [体验数据模型(XDM)](#xdm)
- [Real-time Customer Data Platform B2B 版本](#B2B)
- [源](#sources)

## [!DNL Dashboards] {#dashboards}

平台提供了多个功能板，您可以通过该功能板查看有关贵组织数据的重要信息（在每日快照期间捕获）。

功能板为您的组织数据提供预配置的报表选项，并直接内置到平台内的营销人员工作流程中。 这些功能板可用，无需额外的IT支持，也无需花费时间和精力，即可通过额外的数据仓库设计和实施导出和处理数据。

可通过小组件库访问其各自功能板上的以下小组件。 有关 [如何通过小组件库添加小组件](../../dashboards/customize/widget-library.md).

**新小组件**

| 构件 | 功能板 | 描述 |
| ------ | --------- | ----------- |
| [!UICONTROL 用户档案已添加趋势] | 用户档案 | 此小组件使用折线图来说明过去30天、90天或12个月内每天添加到用户档案存储的合并用户档案总数。 |
| [!UICONTROL 映射到目标状态的受众] | 用户档案 | 此小组件在单个量度中显示已映射和未映射受众的总数，并使用圆环图来说明其总数之间的比例差异。 |
| [!UICONTROL 受众大小] | 用户档案 | 此小组件提供了一个两列表，其中列出了最多20个区段以及每个区段中包含的受众总数。 此列表取决于所应用的合并策略，并根据受众总数从高到低进行排序。 |
| [!UICONTROL 用户档案计数趋势] | 用户档案 | 此小组件使用折线图来说明一段时间内系统中包含的配置文件总数的趋势。 数据可在30天、90天和12个月期间显示。 |
| [!UICONTROL 按身份划分的单个身份配置文件] | 用户档案 | 此小组件使用条形图来说明仅使用单个唯一标识符标识的用户档案总数。 该小组件最多支持五种最常出现的身份。 |
| [!UICONTROL 目标状态] | 目标 | 此小组件将已启用目标的总数显示为单个量度，并使用圆环图来说明已启用目标与已禁用目标之间的比例差异。 |
| [!UICONTROL 按目标平台划分的活动目标] | 目标 | 此小组件使用两列表来显示活动目标平台的列表以及每个目标平台的活动目标总数。 |
| [!UICONTROL 所有目标中的已激活受众] | 目标 | 此小组件以单个量度提供所有目标中激活的受众总数。 |
| [!UICONTROL Audience Activation订单] | 区段 | 此小组件提供了一个三列表，其中列出了受众的目标名称、平台和激活日期。 |
| [!UICONTROL 受众大小趋势] | 区段 | 此小组件提供了折线图插图，用于显示在30天、90天和12个月期间内符合任何区段定义标准的用户档案总数。 |
| [!UICONTROL 受众大小更改趋势] | 区段 | 此小组件提供了一个折线图图，用于显示符合给定区段资格的配置文件总数与最近的每日快照之间的差异。 趋势分析的周期可以显示为30天、90天和12个月。 |
| [!UICONTROL 按身份划分的受众大小趋势] | 区段 | 此小组件根据选定的身份类型展示特定区段的受众大小趋势。 趋势分析的周期可以显示为30天、90天和12个月。 |

**新增功能** {#new-features}

| 功能 | 功能板 | 描述 |
| ------- | --------- | ----------- |
| 孤立的配置文件区段成员资格清理 | 用户档案和许可证使用情况 | 用户档案服务现在每天删除剩余的区段成员，以便在系统中更准确地显示用户档案。 在删除给定配置文件的所有配置文件片段后，会进行此清理。 这可能会在许可证使用情况功能板的“可寻址受众”量度中显示一个下降，也可能在“配置文件”功能板的“配置文件计数”量度中显示一个下降，因为这些量度包含此版本之前剩余的区段片段。 |

{style=&quot;table-layout:auto&quot;}

有关 [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md)和 [[!DNL Segments]](../../dashboards/guides/segments.md) 功能板。

## 数据流 {#dataflows}

在Platform中，数据是从许多不同的源中摄取的，在系统内进行分析，并激活到各种不同的目标。 Platform通过提供数据流的透明度，使跟踪这种潜在的非线性数据流的过程变得更加容易。

数据流是跨平台移动数据的作业的表示形式。 这些数据流是跨不同服务配置的，有助于将数据从源连接器移动到目标数据集，然后由Identity服务和实时客户资料使用这些数据流，最终激活到目标。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 区段功能板 | 您现在可以使用监控仪表板来监控区段的数据流。 要了解更多信息，请阅读 [在UI中监控区段](../../dataflows/ui/monitor-segments.md) |

有关数据流的更多常规信息，请参阅 [数据流概述](../../dataflows/home.md). 要了解有关分段的更多信息，请参阅 [分段概述](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持Adobe Analytics源 | Adobe Analytics源现在支持数据准备功能，允许您在创建数据流时将Analytics报表包数据映射到目标XDM架构。 请参阅 [创建Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以了解更多信息。 |
| 支持导入现有映射规则 | 您现在可以从现有数据流导入映射规则，以加速数据流配置并限制错误。 请参阅 [导入现有映射规则](../../data-prep/ui/mapping.md) 以了解更多信息。 |

有关 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 高级企业目标连接器 | 现在通常提供三个企业目标连接器： [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)和 [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> 企业目标连接器的一般可用性包括之前在测试阶段提供的所有功能，等等： <ul><li>新的身份验证功能，包括 [Azure事件中心中的共享访问签名](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 更多 [身份验证类型](../../destinations/catalog/streaming/http-destination.md#authentication-information) （载体令牌、OAuth 2）；</li><li>[回填历史用户档案数据](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) （在首次激活时发送符合区段资格条件的历史用户档案）；</li><li>现在，这些目标支持数据流运行量度；</li><li>[其他区段元数据](../../destinations/catalog/streaming/http-destination.md#destination-details) 包含在数据有效负载中，包括区段名称和区段时间戳；</li><li>支持 [静态IP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 适用于需要允许列表Experience Platform的客户。</li></ul> |
| 目标数据流的上下文关联警报 | 您现在可以 [订阅警报](../../destinations/ui/alerts.md) 创建目标数据流时，接收有关数据流运行状态、成功或失败的警报消息。 您可以选择在Experience PlatformUI中或通过电子邮件接收警报。 |

### 高级企业目标连接器的发布流程 {#release-process-enterprise-destinations}

对于Amazon Kinesis、Azure事件中心和HTTP API目标，在发行过程（从4月27日开始）中，您将在目标目录中看到以前的测试版目标卡，以及新的通用(GA)目标卡。 使用测试版目标的客户配置的任何数据流将在未来几天内迁移到同一目标的GA版本。 此迁移最终应在4月29日星期五的星期五结束前完成。 测试版目标将在此短暂的时间范围内继续可见，并标记为 **已弃用**.

如果您已在测试阶段利用这些目标，请注意以下事项：

- 如果之前已在测试版中且包含3个目标中的任意一个，则无需执行任何操作。 作为测试版一部分设置的所有数据流都将继续正常运行，并将迁移到GA版本。
- 如果您希望从4月27日开始设置这些目标，请使用新的GA版本的目标进行设置。
- 完成发行操作后，标记为已弃用的测试版卡将被删除，预计在4月29日星期五当天结束前完成。 Experience Platform工程团队正在密切监控是否成功进行发布操作。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Criteo] | 将数据连接并激活到 [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 广告平台。 |
| [!DNL Sendgrid] | 将数据连接并激活到 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 平台。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 添加或删除架构的单个标准字段 | 架构编辑器UI现在允许您向架构中添加部分标准字段组，从而为您选择包含的字段提供了更大的灵活性，而无需从头开始构建自定义资源。<br><br>现在，您还可以直接在架构结构中定义临时自定义字段，并将它们分配给新的或现有的自定义字段组，而无需事先创建或编辑字段组。<br><br>请参阅 [在UI中创建和编辑架构](../../xdm/ui/resources/schemas.md) 以了解有关这些新工作流的更多信息。 |

{style=&quot;table-layout:auto&quot;}

**新的XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 全局模式 | [[!UICONTROL 数据卫生操作请求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 捕获用于删除或修改指定数据集或沙盒中记录的数据清理请求的详细信息。 |
| 描述符 | [[!UICONTROL 时间序列粒度描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 指示时间系列和概要数据的粒度。 当应用到架构时，该架构的 `timestamp` 字段是此粒度的时段中的第一个时间戳。 |
| 类 | [[!UICONTROL XDM概要量度]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分组维的预汇总量度，例如具有GROUP BY的SQL SELECT的结果。 |
| 字段组 | [[!UICONTROL 同意策略评估结果图]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 捕获个人的同意策略评估结果。 |
| 字段组 | [[!UICONTROL 网站搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕获与网站搜索相关的信息，如搜索查询、过滤和排序。 |
| 字段组 | [[!UICONTROL 合并潜在客户]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 捕获合并两个或更多潜在客户的事件的详细信息。 |
| 字段组 | [[!UICONTROL 已发送电子邮件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 捕获向收件人发送电子邮件的事件的详细信息。 |
| 字段组 | [[!UICONTROL 拼合字段]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 捕获通过事件的身份拼合流程计算的值。 |
| 字段组 | [[!UICONTROL 审核的辅助收件人详细信息]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 用于捕获审核的辅助收件人详细信息的Adobe Journey Optimizer字段组。 |
| 字段组 | [[!UICONTROL XDM业务帐户人员关系详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕获与帐户与人员关系相关的详细信息。 |
| 字段组 | [[!UICONTROL 帐户人员详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕获与帐户与人员关系相关的详细信息。 |
| 数据类型 | [[!UICONTROL 购物车]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 捕获有关电子商务购物车的信息。 |
| 数据类型 | [[!UICONTROL 装运]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 捕获一个或多个产品的装运信息。 |
| 数据类型 | [[!UICONTROL 网站搜索]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 捕获有关网站搜索活动的信息。 |
| 扩展(Workfront) | [[!UICONTROL 操作任务属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 捕获与操作任务相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作Portfolio属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕获与工作组合相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作计划属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 捕获与工作程序相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作项目属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 捕获与工作项目相关的详细信息。 |

{style=&quot;table-layout:auto&quot;}

**更新了XDM组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 全局模式 | [[!UICONTROL 目标]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 的新枚举值 `destinationCategory`. |
| 描述符 | [[!UICONTROL 友好名称描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 添加了对删除建议值(`meta:enum`)，而不是标准字段中需要的字段。 |
| 字段组 | [[!UICONTROL 用户登录过程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 字段。 |
| 数据类型 | [[!UICONTROL 商务]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 添加了几个与购物车相关的字段。 |
| 数据类型 | [[!UICONTROL 产品列表项]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 为选定选项和折扣金额添加了新字段。 |
| 扩展（智能服务） | [[!UICONTROL 智能服务历程AI发送时间优化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 优化发送时间得分的存储格式。 |
| 扩展(Workfront) | [[!UICONTROL Workfront更改事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 多个字段替换为 `workfront:customData` 字段。 |
| 扩展(Workfront) | [[!UICONTROL 工作任务属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 添加了多个字段。 |
| 扩展(Workfront) | [[!UICONTROL 工作对象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父对象类型和自定义表单字段的新字段。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML服务使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的功能。 这允许营销分析人员使用业务级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

**更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持多数据集 | 现在，多数据集功能支持所有体验事件数据集以及选择身份映射作为身份。 只要跨数据集存在通用的身份命名空间，客户就可以选择身份映射和任何关联的ID。 Attribution AI支持以下架构：Adobe Analytics、体验事件、消费者体验事件。 有关Attribution AI中多数据集支持的更多信息，请参阅 [Attribution AI用户指南](../../intelligent-services/attribution-ai/user-guide.md). |

有关 [!DNL Intelligent Services]，请参阅 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md).

### 客户人工智能

Real-time Customer Data Platform中提供的Customer AI用于生成自定义倾向得分，例如大规模单个用户档案的流失率和转化。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持多数据集 | 现在，多数据集功能支持所有体验事件数据集以及选择身份映射作为身份。 只要跨数据集存在通用的身份命名空间，客户就可以选择身份映射和任何关联的ID。 Customer AI支持以下模式：Adobe Analytics、体验事件、消费者体验事件和Adobe Audience Manager架构。 有关Customer AI中多数据集支持的更多信息，请参阅 [Customer AI用户指南](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Customer AI中新的模型评估量度 | Customer AI中的新增益图表允许营销人员根据其预算和ROI目标确定要定位的组大小。 新的提升图可测量模型的质量，从而更好地显示他们比随机定位更轻松的提升度。 有关更多信息，请参阅 [通过Customer AI发现洞察](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 文档。 |

有关 [!DNL Intelligent Services]，请参阅 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md).

## Real-time Customer Data Platform B2B 版本 {#B2B}

Real-time CDP B2B Edition构建于Real-time Customer Data Platform(Real-time CDP)之上，专为在业务到业务服务模型中运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其整合为人员和帐户配置文件的单一视图。 通过这种统一的数据，营销人员可以准确定位特定受众并在所有可用渠道中吸引这些受众。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持 `isDeleted` 功能 | 全部 [!DNL Marketo] 数据集除外 `Activities` 现在支持 `isDeleted` 映射。 新映射会自动添加到您现有的B2B数据流中。 您可以使用 `isDeleted` 映射以过滤已删除的记录，以便您的数据 [!DNL Data Lake] 与源数据一致。 请参阅 [[!DNL Marketo] 映射字段指南](../../sources/connectors/adobe-applications/mapping/marketo.md) 有关 `isDeleted`. |

要了解有关Real-time Customer Data Platform B2B Edition的更多信息，请参阅 [B2B概述](../../rtcdp/b2b-overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持 [!DNL OneTrust Integration] | 您现在可以使用 [!DNL OneTrust Integration] 源，用于从 [!DNL OneTrust] 帐户到平台。 请参阅 [创建 [!DNL OneTrust Integration] 源连接](../../sources/connectors/consent-and-preferences/onetrust.md) 以了解更多信息。 |
| 支持 [!DNL Square] | 您现在可以使用 [!DNL Square] 源，用于从 [!DNL Square] 帐户到平台。 |
| 支持删除客户属性数据流 | 您现在可以删除使用客户属性源连接器创建的数据流。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
