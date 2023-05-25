---
title: Adobe Experience Platform发行说明2022年4月
description: Adobe Experience Platform 2022年4月版发行说明。
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2904'
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
- [Real-Time Customer Data Platform B2B 版](#B2B)
- [源](#sources)

## [!DNL Dashboards] {#dashboards}

Platform提供了多个仪表板，您可以通过该仪表板查看有关您组织的数据的重要信息，如在每日快照期间捕获的数据。

功能板为您的组织数据提供预配置的报表选项，并且直接内置于Platform内的营销人员工作流程中。 无需额外的IT支持，也不必花时间和精力通过额外的数据仓库设计和实施导出和处理数据，即可使用这些功能板。

以下构件可通过其各自功能板上的构件库使用。 有关以下内容的更多信息，请参阅文档 [如何通过构件库添加构件](../../dashboards/customize/widget-library.md).

**新构件**

| 构件 | 功能板 | 描述 |
| ------ | --------- | ----------- |
| [!UICONTROL 配置文件添加趋势] | 用户档案 | 此构件使用线形图说明过去30天、90天或12个月内每天添加到配置文件存储区的合并配置文件总数。 |
| [!UICONTROL 映射到目标状态的受众] | 用户档案 | 此构件在单个量度中显示已映射和未映射受众的总数，并使用圆环图说明其总数之间的比例差异。 |
| [!UICONTROL 受众规模] | 用户档案 | 此构件提供一个两列表格，其中列出最多20个区段以及每个区段中包含的受众总数。 该列表取决于根据受众总数从高到低应用并排序的合并策略。 |
| [!UICONTROL 配置文件计数趋势] | 用户档案 | 此构件使用线形图说明系统中包含的配置文件总数随时间变化的趋势。 数据可以在30天、90天和12个月的时段内可视化。 |
| [!UICONTROL 按身份列出的单一身份配置文件] | 用户档案 | 此构件使用条形图说明仅通过单个唯一标识符标识的用户档案总数。 该构件支持最多五个最常见的身份。 |
| [!UICONTROL 目标状态] | 目标 | 此构件将启用的目标总数显示为单个量度，并使用圆环图来说明启用目标和禁用目标之间的比例差异。 |
| [!UICONTROL 按目标平台列出的活动目标] | 目标 | 此构件使用两列表格来显示活动目标平台的列表以及每个目标平台的活动目标总数。 |
| [!UICONTROL 所有目标中的已激活受众] | 目标 | 此构件在一个量度中提供跨所有目标激活的受众总数。 |
| [!UICONTROL Audience激活顺序] | 区段 | 此构件提供了一个三列表格，其中列出了目标名称、平台和受众的激活日期。 |
| [!UICONTROL 受众规模趋势] | 区段 | 此小组件在30天、90天和12个月期间提供符合任何区段定义标准的配置文件总数的线形图说明。 |
| [!UICONTROL 受众规模变化趋势] | 区段 | 此构件用线形图说明了最近每日快照之间符合给定区段条件的配置文件总数之间的差异。 趋势分析期间可以在30天、90天和12个月期间中进行可视化。 |
| [!UICONTROL 按身份划分的受众规模趋势] | 区段 | 此构件说明了基于选定身份类型的特定区段的受众规模趋势。 趋势分析期间可以在30天、90天和12个月期间中进行可视化。 |

**新增功能** {#new-features}

| 功能 | 功能板 | 描述 |
| ------- | --------- | ----------- |
| 孤立的配置文件区段会员资格清理 | 配置文件和许可证使用情况 | 现在，配置文件服务每天都会删除剩余的区段成员，以便更准确地表示您系统中的配置文件。 删除给定配置文件的所有配置文件片段后，将进行此清理。 这可能显示在许可证使用情况仪表板中的“可寻址受众”量度下降，也可能显示在配置文件仪表板中的“配置文件计数”量度下降，因为这些量度包含此版本之前的剩余区段片段。 |

{style="table-layout:auto"}

有关以下内容的更多信息，请参阅文档 [[!DNL Profiles]](../../dashboards/guides/profiles.md)， [[!DNL Destinations]](../../dashboards/guides/destinations.md)、和 [[!DNL Segments]](../../dashboards/guides/segments.md) 功能板。

## 数据流 {#dataflows}

在Platform中，数据从许多不同的来源摄取，在系统中进行分析，并激活到各种目的地。 Platform通过提供数据流透明性，使跟踪这种潜在非线性数据流的过程更加容易。

数据流是跨Platform移动数据的作业的表示形式。 这些数据流在不同的服务中配置，有助于将数据从源连接器移动到目标数据集，然后在最终激活到目标之前，身份服务和实时客户资料将在目标数据集中使用这些数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 区段仪表板 | 您现在可以使用监控仪表板监控区段的数据流。 要了解更多信息，请阅读以下指南： [在UI中监控区段](../../dataflows/ui/monitor-segments.md) |

有关数据流的更多常规信息，请参阅 [数据流概述](../../dataflows/home.md). 要了解有关分段的更多信息，请参阅 [分段概述](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师映射、转换和验证数据到/传出体验数据模型(XDM)。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持Adobe Analytics源 | Adobe Analytics源现在支持数据准备功能，允许您在创建数据流时将Analytics报表包数据映射到目标XDM架构。 请参阅上的教程 [创建Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 了解更多信息。 |
| 支持导入现有映射规则 | 您现在可以从现有数据流导入映射规则，以加快数据流配置并限制错误。 请参阅上的教程 [导入现有映射规则](../../data-prep/ui/mapping.md) 了解更多信息。 |

有关的详细信息 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新增或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 高级企业目标连接器 | 现已正式提供三个企业目标连接器： [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)， [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)、和 [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> 企业目标连接器的正式发布包括之前在Beta阶段提供的所有功能，以及更多： <ul><li>新的身份验证功能，包括 [Azure事件中心中的共享访问签名](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 及更多内容 [身份验证类型](../../destinations/catalog/streaming/http-destination.md#authentication-information) （持有者令牌，OAuth 2）在HTTP API目标中；</li><li>[正在回填历史配置文件数据](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) （首次激活时发送符合区段条件的历史用户档案）；</li><li>这些目标现在支持数据流运行量度；</li><li>[其他区段元数据](../../destinations/catalog/streaming/http-destination.md#destination-details) 包括区段名称和区段时间戳；</li><li>支持 [静态IP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 适用于需要Experience Platform的允许列表。</li></ul> |
| 目标数据流的上下文警报 | 您现在可以 [订阅警报](../../destinations/ui/alerts.md) 创建目标数据流时，接收有关数据流运行的状态、成功或失败的警报消息。 您可以选择在Experience PlatformUI中或通过电子邮件接收警报。 |

### 高级企业目标连接器的发布流程 {#release-process-enterprise-destinations}

对于Amazon Kinesis、Azure事件中心和HTTP API目标，在发布过程（从4月27日开始）中，您将在目标目录中看到之前的Beta测试版目标卡和新的通常可用(GA)目标卡。 客户使用Beta目标配置的任何数据流都将在未来几天内迁移到同一目标的GA版本。 此迁移应在4月29日星期五结束前完成。 在此较短的时间范围内，测试版目标将继续可见，并标记为 **已弃用**.

如果您一直在Beta阶段利用这些目标，请注意以下事项：

- 如果之前已在3个目标中的任何一个目标上处于测试阶段，则无需执行任何操作。 作为测试版的一部分设置的所有数据流将继续正常运行，并将迁移到GA版本。
- 如果您要从4月27日起设置这些目标，请使用目标的新GA版本进行设置。
- 预计在4月29日星期五结束前发布操作完成后，将删除标记为已弃用的Beta卡。 Experience Platform工程团队正在密切监控成功的发布操作。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Criteo] | 将数据连接并激活到 [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 广告平台。 |
| [!DNL Sendgrid] | 将数据连接并激活到 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 用于交易和营销电子邮件的平台。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一个开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵守XDM标准，所有客户体验数据都可以纳入到通用表示中，从而以更快、更集成的方式提供见解。 您可以从客户操作中获得有价值的见解，通过区段定义客户受众，并将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 为架构添加或删除单个标准字段 | 架构编辑器UI现在允许您将标准字段组的部分添加到架构中，为您选择包含的字段提供了更大的灵活性，而无需从头开始构建自定义资源。<br><br>您现在还可以直接在架构结构中定义临时自定义字段，并将其分配给新的或现有的自定义字段组，而无需预先创建或编辑字段组。<br><br>请参阅指南，网址为 [在UI中创建和编辑架构](../../xdm/ui/resources/schemas.md) 以了解有关这些新工作流的详细信息。 |

{style="table-layout:auto"}

**新XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 全局架构 | [[!UICONTROL 数据卫生操作请求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 捕获数据清理请求的详细信息，以删除或修改指定数据集或沙盒中的记录。 |
| 描述符 | [[!UICONTROL 时间序列粒度描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 指示时间序列和摘要数据的粒度。 当应用于架构时，架构的 `timestamp` 字段是此粒度期间的第一个时间戳。 |
| 类 | [[!UICONTROL XDM摘要量度]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供带有分组维度的预摘要量度，例如带有GROUP BY的SQL SELECT的结果。 |
| 字段组 | [[!UICONTROL 同意政策评估结果映射]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 捕获个人的同意策略评估结果。 |
| 字段组 | [[!UICONTROL 网站搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕获与网站搜索相关的信息，例如搜索查询、筛选和排序。 |
| 字段组 | [[!UICONTROL 合并潜在客户]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 捕获合并两个或多个潜在客户的事件的详细信息。 |
| 字段组 | [[!UICONTROL 已发送电子邮件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 捕获向收件人发送电子邮件的事件的详细信息。 |
| 字段组 | [[!UICONTROL 拼接字段]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 捕获通过事件的身份拼接过程计算的值。 |
| 字段组 | [[!UICONTROL 用于审核的辅助收件人详细信息]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 捕获审核的辅助收件人详细信息的Adobe Journey Optimizer字段组。 |
| 字段组 | [[!UICONTROL XDM业务帐户人员关系详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕获与帐户 — 人员关系相关的详细信息。 |
| 字段组 | [[!UICONTROL 帐户人员详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕获与帐户 — 人员关系相关的详细信息。 |
| 数据类型 | [[!UICONTROL 购物车]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 捕获有关电子商务购物车的信息。 |
| 数据类型 | [[!UICONTROL 配送]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 捕获一个或多个产品的送货信息。 |
| 数据类型 | [[!UICONTROL 网站搜索]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 捕获有关网站搜索活动的信息。 |
| 扩展(Workfront) | [[!UICONTROL 操作任务属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 捕获与操作任务相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作Portfolio属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕获与工作组合相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作计划属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 捕获与工作方案相关的详细信息。 |
| 扩展(Workfront) | [[!UICONTROL 工作项目属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 捕获与工作项目相关的详细信息。 |

{style="table-layout:auto"}

**更新的XDM组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 全局架构 | [[!UICONTROL 目标]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 的新枚举值 `destinationCategory`. |
| 描述符 | [[!UICONTROL 友好名称描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 添加了对删除建议值的支持(`meta:enum`)，这些参数不需要来自标准字段。 |
| 字段组 | [[!UICONTROL 用户登录过程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 字段已添加。 |
| 数据类型 | [[!UICONTROL 商务]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已添加多个与购物车相关的字段。 |
| 数据类型 | [[!UICONTROL 产品列表项]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 为所选选项和折扣金额添加了新字段。 |
| 扩展（智能服务） | [[!UICONTROL 智能服务JourneyAI发送时间优化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 针对发送时间分数优化存储格式。 |
| 扩展(Workfront) | [[!UICONTROL Workfront更改事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 多个字段已替换为 `workfront:customData` 自定义表单字段的字段。 |
| 扩展(Workfront) | [[!UICONTROL 工作任务属性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 添加了多个字段。 |
| 扩展(Workfront) | [[!UICONTROL 工作对象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父对象类型和自定义表单字段的新字段。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML服务使营销分析师和从业人员能够在客户体验用例中利用人工智能和机器学习的强大功能。 借助此功能，营销分析人员可使用商业级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持多个数据集 | 多数据集功能现在支持所有体验事件数据集，以及选择身份映射作为身份。 只要数据集中有一个共同的身份命名空间，客户就可以选择身份映射和任何关联的ID。 Attribution AI支持以下架构：Adobe Analytics、体验事件、使用者体验事件。 有关Attribution AI中支持多数据集的更多信息，请参阅 [Attribution AI用户指南](../../intelligent-services/attribution-ai/user-guide.md). |

有关的详细信息 [!DNL Intelligent Services]，请参阅 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md).

### 客户人工智能

Real-time Customer Data Platform中提供的客户人工智能，用于生成自定义倾向分数，例如大规模单个用户档案的流失和转化率。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支持多个数据集 | 多数据集功能现在支持所有体验事件数据集，以及选择身份映射作为身份。 只要数据集中有一个共同的身份命名空间，客户就可以选择身份映射和任何关联的ID。 客户人工智能支持以下架构：Adobe Analytics、体验事件、消费者体验事件和Adobe Audience Manager架构。 有关Customer AI中多数据集支持的更多信息，请参阅 [Customer AI用户指南](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Customer AI中的新模型评估指标 | Customer AI中新的收益图允许营销人员根据其预算和ROI目标确定要定位的群组规模。 新的提升图可衡量模型的质量，从而更好地显示他们将超过随机定位的提升度。 欲了解更多信息，请参见 [用Customer AI发现洞察](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 文档。 |

有关的详细信息 [!DNL Intelligent Services]，请参阅 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B 版 {#B2B}

Real-Time CDP B2B版构建于Real-time Customer Data Platform (Real-Time CDP)之上，专为以B2B服务模式运营的营销人员而构建。 它将来自多个来源的数据整合在一起，并将其合并到人员和帐户配置文件的单一视图中。 此统一数据允许营销人员准确地定位特定受众，并在所有可用渠道中吸引这些受众。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持 `isDeleted` 功能 | 全部 [!DNL Marketo] 数据集除外 `Activities` 现在支持 `isDeleted` 映射。 新映射会自动添加到现有B2B数据流中。 您可以使用 `isDeleted` 用于筛选已删除的记录的映射，以使您的数据位于 [!DNL Data Lake] 与源数据一致。 请参阅 [[!DNL Marketo] 映射字段指南](../../sources/connectors/adobe-applications/mapping/marketo.md) 有关的详细信息 `isDeleted`. |

要了解有关Real-time Customer Data Platform B2B版本的更多信息，请参阅 [B2B概述](../../rtcdp/b2b-overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持 [!DNL OneTrust Integration] | 您现在可以使用 [!DNL OneTrust Integration] 从中摄取同意和偏好设置数据的源 [!DNL OneTrust] Platform帐户。 请参阅相关文档 [创建 [!DNL OneTrust Integration] 源连接](../../sources/connectors/consent-and-preferences/onetrust.md) 了解更多信息。 |
| 支持 [!DNL Square] | 您现在可以使用 [!DNL Square] 从贵机构提取支付数据的来源 [!DNL Square] Platform帐户。 |
| 支持删除客户属性数据流 | 您现在可以删除使用客户属性源连接器创建的数据流。 |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
