---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 的 2024 年 4 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 17%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年4月30日**

>[!TIP]
>
>使用 [Adobe Experience Platform术语表](/help/landing/glossary.md) 以熟悉Real-time Customer Data Platform和Adobe Experience Platform中使用的术语。 如果找不到要查找的特定术语，请使用页面上的反馈选项来请求将新术语添加到术语表中。

对Experience Platform中现有功能的更新：

- [仪表板](#dashboards)
- [数据收集](#data-collection)
- [目标](#destinations)
- [身份服务](#identity-service)
- [监控](#monitoring)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Real-time Customer Data Platform B2B见解 | 浏览预配置的 [关于客户和机会的Real-Time CDP B2B数据见解](../../dashboards/insights/account-profiles.md) 帮助您了解数据并告知业务决策。 您还可以 [使用Real-Time CDP B2B数据模型构建您自己的见解](../../dashboards/data-models/cdp-insights-data-model-b2c.md) 用于可视化和浏览您的数据，并将您的自定义可视化保存在仪表板中。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Experience PlatformEdge Network，可在其中丰富和转换数据，并将其分发到Adobe或非Adobe目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Acxiom Anonymous Visitor Insights] 标记扩展 | 了解您的网站访客来自何处 [!DNL Acxiom's Visitor Insights]. 通过利用地域IP查找技术， Acxiom可以查明匿名浏览器的位置。 识别之后，在他们的组织数据库中进行搜索会生成其他洞察，并会发送回浏览器。 内容创建者因此可以定制其内容以匹配这些数据点，为访客提供更加个性化和引人入胜的体验，即使他们一开始是陌生人。 |
| 数据流 | [Edge Network 机器人检测](../../datastreams/bot-detection.md) | 源自非人类实体（如自动化程序、网页抓取程序、蜘蛛程序、脚本扫描程序）的流量，可能使识别来自人类访客的事件变得更加困难。 此类流量可能会对重要的业务量度产生负面影响，从而导致不正确的流量报表。 <br>机器人检测允许您识别由生成的事件 [Web SDK](../../web-sdk/home.md)， [移动SDK](https://developer.adobe.com/client-sdks/home/) 和 [[!DNL Server API]](../../server-api/overview.md) 由已知的蜘蛛和机器人生成。 通过为数据流配置机器人检测，您可以识别要分类为机器人事件的特定IP地址、IP范围和请求标头。 <br> 识别机器人流量可以为您提供对网站或移动应用程序上的用户活动的更准确测量。 |
| Mobile SDK | 主要版本发布 | Mobile SDK的新主要版本已针对以下平台发布： iOS Mobile Core 5.x和兼容的iOS扩展、Android Mobile Core 3.x和兼容的Android扩展、React Native Core 6.x和兼容的React本机扩展、Flutter Core 4.x和兼容的Flutter扩展。 这些版本提供了多项新增功能和增强功能，包括支持适用于Jetpack撰写的Android SDK、支持基于Adobe Journey Optimizer代码的体验，以及正式提供了适用于Flutter的Adobe Journey Optimizer消息传送扩展。 有关更详细的发行说明，请参阅 [Mobile SDK发行说明](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobile SDK | 隐私 | 由于Apple的策略更新，从2024年5月1日开始，开发人员必须实施新的隐私功能才能提交到App Store。 所有使用Mobile SDK的Adobe客户，如果他们希望在5月1日后获得App Store批准，则需要升级到SDK版本5.x。 |
| Roku SDK | Roku SDK | Roku SDK的第一个主要版本已发布，支持适用于平台Edge Network的流媒体。 |
| 标记和事件转发 | 产品内指南 | Experience Platform [标记](../../tags/home.md) 和 [事件转发](../../tags/ui/event-forwarding/overview.md) 提供一系列新的体验，帮助您快速入门，并快速实现价值。 这些体验包括新的载入屏幕、产品内教程和工具提示。 <br>![突出显示产品内指南的事件转发。](../2024/assets/april/event-forwarding.png "模式编辑器，其中高亮显示了“Type”和“Map”值类型字段。"){width="100" zoomable="yes"}<br> |
| Web SDK | 简化了Audience Manager客户的Web SDK采用过程 | 多项Web SDK更新现在可以简化Web SDK的使用，而无需使用适用于Experience Cloud解决方案(如Audience Manager、Analytics和Target)的Experience Data Model (XDM)。 请参阅以下指南以了解有关Audience ManagerWeb SDK采用率的更多信息： <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">将用于Audience Manager的数据收集库从Audience Manager标记扩展更新为Web SDK标记扩展</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">将您的用于Audience Manager的数据收集库从AppMeasurementJavaScript库更新到Web SDK JavaScript库</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

要了解有关数据集合的更多信息，请阅读 [数据收集概述](../../collection/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| `isRequired` 参数现在可用于Destination SDK中的嵌套客户数据字段 | 在Destination SDK中配置目标时，您现在可以 [根据需要设置嵌套的客户数据字段](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). 这样，设置目标的用户便无法继续其激活流程，除非为该字段选择值。 |
| 使用Web SDK设置Adobe Target目标时，边缘分段不再是强制要求 | 以前，在配置 [Adobe Target目标](/help/destinations/catalog/personalization/adobe-target-connection.md) 使用Web SDK时，必须为个性化和边缘分段启用数据流。 要求为边缘分段启用数据流 [现已删除](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream). 请注意，在将Adobe Target与Real-Time CDP结合使用时，此集成模式仅允许您从一部分个性化用例中受益。 详细了解 [按集成类型启用的用例](/help/destinations/catalog/personalization/adobe-target-connection.md#parameters). |
| [!BADGE 测试版]{type=Informative}从激活流中删除多个受众和数据集 | 您现在可以选择并从目标激活流中删除多个受众和数据集。 请参阅 [目标详细信息](../../destinations/ui/destination-details-page.md#bulk-remove) 和 [数据集导出](../../destinations/ui/export-datasets.md) 文档，以了解更多详细信息。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## 身份服务 {#identity-service}

使用Adobe Experience Platform Identity Service跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而全面了解客户及其行为。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 弃用 `/orgs/{ORG}/` API中的端点 | 中的以下端点 [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) 已弃用：<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> 您可以使用 `/idnamespace/identities` 和 `/idnamespace/identities/{ID}` 端点完成相同的任务，并检索组织中的所有命名空间或组织中的特定命名空间。 |

{style="table-layout:auto"}

有关Identity Service的详细信息，请阅读 [Identity服务概述](../../identity-service/home.md).

## 监控 {#monitoring}

使用Experience PlatformUI中的监视仪表板可监视来自源、身份服务、实时客户个人资料、受众和目标的数据的历程。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 监控仪表板扩展 | 您现在可以根据业务用例对不同数据类型使用监控仪表板。 使用监视仪表板可监视源、受众和目标中人员、帐户和潜在客户数据类型活动。 |

{style="table-layout:auto"}

有关详细信息，请阅读上的指南 [使用监视仪表板](../../dataflows/ui/monitor.md).

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以从以下位置连接任何数据集： [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 查询隔离 | 自动隔离失败的查询执行，以防止中断并维护一致的性能。 请参阅 [查询隔离](../../query-service/ui/query-schedules.md#quarantine) 文档，以了解更多信息。 |
| 取消查询 | 通过取消长时间运行的查询来控制查询执行并提高工作效率。请参阅 [取消查询](../../query-service/ui/user-guide.md#cancel-query) 文档，以了解更多信息。 |
| 计划的查询警报 | 在计划查询时通过主动通知及时了解最新信息，确保高效及时的任务管理。 您可以 [创建查询时订阅警报](../../query-service/ui/query-schedules.md#alerts-for-query-status) 或使用现有计划查询的内联操作。 请参阅 [订阅具有内联操作的警报](../../query-service/ui/monitor-queries.md#alert-subscription) 文档，以了解更多信息。 |
| 改进了计划的查询导航 | 可在查询模板和计划运行之间轻松导航，以提高工作效率。 请参阅相关文档 [查看计划的查询运行](../../query-service/ui/query-schedules.md#scheduled-query-runs) 以了解更多信息。 |
| 扩展查询输出 | 可在控制台中访问多达500行查询结果，以更深入地分析您的数据。请参见 [结果计数](../../query-service/ui/user-guide.md#result-count) 文档，以了解更多信息。 |
| 旧版查询编辑器失效 | 自2024年4月30日起，增强型查询编辑器已成为所有用户的默认编辑器。 旧版编辑器将于2024年5月30日弃用，并且不再可用。 请参阅 [查询编辑器用户指南](../../query-service/ui/user-guide.md) 以了解更多信息。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform旨在丰富全球范围内的数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。 为了满足此需求，Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的沙箱，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [沙盒工具](../../sandboxes/ui/sandbox-tooling.md) | 使用沙盒工具执行以下操作 [导出](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) 将所有支持的对象类型放入完整的沙盒包中，然后 [导入](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) 跨各种沙盒的包以复制对象配置。 |

{style="table-layout:auto"}

有关沙箱的详细信息，请阅读 [沙盒概述](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**更新了功能**

| 功能 | 描述 |
| ------- | ----------- |
| 受众生命周期状态 | 受众生命周期状态已得到简化，以简化生命周期管理。 要了解有关这些生命周期状态的更多信息，请阅读 [Segmentation Service常见问题](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

在Experience Platform中使用源从Adobe应用程序或第三方数据源中摄取数据。

**新源**

| 新源 | 描述 |
| --- | --- |
| [!BADGE 测试版]{type=Informational} [!DNL PathFactory] | 使用 [[!DNL PathFactory] 源](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) 要集成您的访客、会话和页面查看数据，请执行以下操作 [!DNL PathFactory] Experience Platform。 阅读 [[!DNL PathFactory] 概述](../../sources/connectors/marketing-automation/pathfactory.md) 以获取有关如何开始的信息。 |
| [!DNL Teradata Vantage] | 使用 [[!DNL Teradata Vantage] 源](../../sources/tutorials/ui/create/databases/teradata-vantage.md) 将数据从混合多云环境摄取到Experience Platform。 阅读 [[!DNL Teradata Vantage] 概述](../../sources/connectors/databases/teradata-vantage.md) 以获取有关如何开始的信息。 |

{style="table-layout:auto"}

**新增功能和更新功能**

| 功能 | 描述 |
| --- | --- |
| 更新了VA7中允许列表的IP地址 | 以下IP地址已添加到要添加到VA7（北美洲）允许列表中的IP地址列表： <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> 有关要添加到允许列表的IP地址的完整列表，请阅读 [IP地址允许列表文档](../../sources/ip-address-allow-list.md). |
| 支持新的身份验证类型 [!DNL Azure Event Hubs] 源 | 您现在可以连接 [!DNL Event Hubs] 使用以下任一方式Experience Platform的源 [!DNL Azure Active Directory Authentication] 或 [!DNL Scoped Azure Active Directory Authentication]. 阅读指南： [连接 [!DNL Event Hubs] 至Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) 以了解更多信息。 |
| 更新至 [!DNL Data Landing Zone] 凭据检索 | 现在，您可以在源工作区中使用右边栏来检索 [!DNL Data Landing Zone] 凭据。 您现在还可以使用右边栏刷新凭据。 阅读 [[!DNL Data Landing Zone] UI指南](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) 以了解更多信息。 |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

欲知关于来源的更多信息，请阅读 [源概述](../../sources/home.md).
