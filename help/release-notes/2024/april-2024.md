---
title: Adobe Experience Platform 发行说明（2024 年 4 月）
description: Adobe Experience Platform 的 2024 年 4 月发行说明。
exl-id: 86d72fd8-a464-4715-abc9-4177236e423c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 97%

---

# Adobe Experience Platform 发行说明

**发布日期：2024 年 4 月 30 日**

>[!TIP]
>
>使用 [Adobe Experience Platform 词汇表](/help/landing/glossary.md)，熟悉 Real-time Customer Data Platform 和 Adobe Experience Platform 中使用的术语。如果您找不到所需的特定术语，请使用页面上的反馈选项请求将新术语添加到词汇表中。

Experience Platform 中现有功能的更新：

- [仪表板](#dashboards)
- [数据收集](#data-collection)
- [目标](#destinations)
- [身份标识服务](#identity-service)
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
| Real-Time Customer Data Platform B2B 洞察 | 探索预先配置的[有关帐户和机会的 Real-Time CDP B2B 数据洞察](../../dashboards/insights/account-profiles.md)，以帮助您了解数据并为业务决策提供信息。您还可以[使用 Real-Time CDP B2B 数据模型](../../dashboards/data-models/cdp-insights-data-model-b2c.md)构建您自己的洞察，以可视化和探索您的数据，并在仪表板中保存您的自定义可视化效果。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Acxiom Anonymous Visitor Insights] 标记扩展 | 使用 [!DNL Acxiom's Visitor Insights]了解您的网站访问者来自哪里。通过利用地理 IP 查找技术，Acxiom 可以精确定位匿名浏览器的位置。一旦确定，在其组织的数据库中进行搜索就会产生额外的洞察，并将其发送回浏览器。内容创建者因此可以定制他们的内容来匹配这些数据点，为访问者提供更加个性化和更具吸引力的体验，即使他们一开始是陌生人。 |
| 数据流 | [Edge Network 机器人检测](../../datastreams/bot-detection.md) | 来自非人类实体（例如自动程序、网络爬虫、蜘蛛、脚本扫描器）的流量会使识别来自人类访问者的事件变得更加困难。这种类型的流量会对重要的业务指标产生负面影响，导致流量报告不正确。通过机器人检测，可将 Web SDK、Mobile SDK 和 Server API 生成的事件视为由已知的蜘蛛程序和机器人生成。<br>机器人检测允许您识别由 [Web SDK](../../web-sdk/home.md)、[Mobile SDK](https://developer.adobe.com/client-sdks/home/) 和 [[!DNL Server API]](../../server-api/overview.md) 生成的事件是否由已知的蜘蛛和机器人生成。通过为数据流配置机器人检测，您可以识别想要归类为机器人事件的特定 IP 地址、IP 范围和请求标头。<br> 识别机器人流量可以为您提供对网站或移动应用程序上用户活动的更准确测量。 |
| Mobile SDK | 主要版本发布 | 已针对以下平台发布了 Mobile SDK 的新主要版本：iOS Mobile Core 5.x 和兼容的 iOS 扩展、Android Mobile Core 3.x 和兼容的Android 扩展、React Native Core 6.x 和兼容的 React Native 扩展、Flutter Core 4.x 和兼容的 Flutter 扩展。这些版本提供了几个新功能和增强功能，包括 Android SDK 对 Jetpack Compose 的支持、对 Adobe Journey Optimizer 基于代码的体验的支持以及对 Flutter 的 Adobe Journey Optimizer Messaging 扩展的普遍可用性。有关更详细的发行说明，请参阅[移动 SDK 发行说明](https://developer.adobe.com/client-sdks/home/release-notes/)。 |
| Mobile SDK | 隐私 | 由于Apple 的政策更新，从 2024 年 5 月 1 日开始，开发人员必须实现新的隐私功能才能提交给 App Store。所有使用移动 SDK 的 Adobe 客户如果希望在 5 月 1 日之后获得 App Store 批准，都需要升级到 SDK 5.x 版本。 |
| Roku SDK | Roku SDK | Roku SDK的第一个主要版本已发布，并支持Experience Platform Edge Network的流媒体。 |
| 标记和事件转发 | 产品内指导 | Experience Platform [标签](../../tags/home.md)和 [ Event Forwarding ](../../tags/ui/event-forwarding/overview.md) 提供一系列全新的体验，帮助您快速入门并快速实现价值。这些体验包括新的加入屏幕、产品内教程和工具提示。<br>![Event Forwarding，并突出显示产品内的指导。](../2024/assets/april/event-forwarding.png "Schemas Editor 中类型和映射值类型字段突出显示。"){width="100" zoomable="yes"}<br> |
| Web SDK | 简化 Audience Manager 客户的 Web SDK 采用 | 现在，多个 Web SDK 更新简化了 Web SDK 的采用，无需使用体验数据模型 (XDM) 即可实现 Experience Cloud 解决方案，例如 Audience Manager、Analytics 和 Target。请通过以下指南了解有关 Audience Manager Web SDK 采用的更多信息： <ul><li><a href="https://experienceleague.adobe.com/zh-hans/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">将 Audience Manager 的数据收集库从 Audience Manager 标记扩展更新为 Web SDK 标记扩展</li><li><a href="https://experienceleague.adobe.com/zh-hans/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">将 Audience Manager 的数据收集库从 AppMeasurement JavaScript 库更新为 Web SDK JavaScript 库</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

要详细了解数据收集，请参阅[数据收集概述](../../collection/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| `isRequired` 参数现在可用于 Destination SDK 中的嵌套客户数据字段 | 在 Destination SDK 中配置目标时，您现在可以[根据需要设置嵌套的客户数据字段](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields)。这样，设置目标的用户在为该字段选择一个值之前无法继续他们的激活流程。 |
| 使用 Web SDK 设置 Adobe Target 目标时，边缘分段不再是强制性要求 | 以前，在配置 [Adobe Target 目标](/help/destinations/catalog/personalization/adobe-target-connection.md)使用 Web SDK，数据流必须能够实现个性化和边缘分段。要求数据流能够进行边缘分段[已被删除](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)。请注意，当使用 Adobe Target 与实时 CDP 时，此集成模式仅允许您从个性化用例的子集中受益。阅读更多关于[集成类型支持的用例](/help/destinations/catalog/personalization/adobe-target-connection.md#supported-use-cases)。 |
| [!BADGE Beta]{type=Informative} 从激活流程中删除多个受众和数据集 | 您现在可以从目标激活流中选择和删除多个受众和数据集。查看[目标详情](../../destinations/ui/destination-details-page.md#bulk-remove)和[数据集导出](../../destinations/ui/export-datasets.md)文档以了解更多详细信息。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## 身份标识服务 {#identity-service}

使用 Adobe Experience Platform 身份标识服务通过跨设备和系统桥接身份标识，全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 弃用 API 中的 `/orgs/{ORG}/` 端点 | [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) 中的以下端点已被弃用：<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> 您可以使用 `/idnamespace/identities` 和 `/idnamespace/identities/{ID}` 端点来完成相同的任务，并检索组织中的所有命名空间或组织中的特定命名空间。 |

{style="table-layout:auto"}

有关身份标识服务的更多信息，请参阅[身份标识服务概述](../../identity-service/home.md)。

## 监控 {#monitoring}

使用 Experience Platform UI 中的监控仪表板来监控源、身份标识服务、实时客户轮廓、受众和目标的数据历程。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 监控仪表板扩展 | 您现在可以根据您的业务用例使用监控仪表板来监控不同类型的数据类型。使用监控仪表板监控来源、受众和目标中的人员、帐户和潜在客户数据类型活动。 |

{style="table-layout:auto"}

若要了解更多信息，请阅读有关[使用监控仪表板](../../dataflows/ui/monitor.md)的指南。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以加入来自 [!DNL Data Lake] 的任何任何数据集，并将查询结果捕获为新数据集，以用于报告、Data Science Workspace，或将数据摄取到实时客户轮廓。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 查询隔离 | 自动隔离失败的查询执行以防止中断并保持一致的性能。有关更多信息，请参阅[查询隔离](../../query-service/ui/query-schedules.md#quarantine)文档。 |
| 取消查询 | 通过取消长时间运行的查询来控制查询执行并提高工作效率。有关更多信息，请参阅[取消查询](../../query-service/ui/user-guide.md#cancel-query)文档。 |
| 计划查询警报 | 在安排查询时通过主动通知随时了解情况，确保高效、及时的任务管理。您可以[在创建查询](../../query-service/ui/query-schedules.md#alerts-for-query-status)或使用现有计划查询的内联操作时订阅警报。有关详细信息，请参阅[使用内联操作订阅警报](../../query-service/ui/monitor-queries.md#alert-subscription)文档。 |
| 改进的计划查询导航 | 轻松在查询模板和计划运行之间导航以提高生产力。有关更多信息，请参阅[查看计划查询运行](../../query-service/ui/query-schedules.md#scheduled-query-runs)的文档。 |
| 扩展查询输出 | Access 控制台内最多可显示 500 行查询结果，以便对您的数据进行更深入的分析。有关更多信息，请参阅[结果计数](../../query-service/ui/user-guide.md#result-count)文档。 |
| 旧版查询编辑器停用 | 自 2024 年 4 月 30 日起，增强查询编辑器已成为所有用户的默认编辑器。旧版编辑器将于 2024 年 5 月 24 日弃用，并且不再可用。有关更多信息，请参阅[查询编辑器用户指南](../../query-service/ui/user-guide.md)。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [沙盒工具](../../sandboxes/ui/sandbox-tooling.md) | 使用沙盒工具将所有支持的对象类型[导出](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox)到完整的沙盒包中，然后将该包[导入](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox)到各个沙盒中以复制对象配置。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Experience Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 受众生命周期状态 | 受众生命周期状态已经得到简化，以简化生命周期管理。要了解有关这些生命周期状态的更多信息，请阅读[分段服务常见问题解答](../../segmentation/faq.md#lifecycle-states)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**新来源**

| 新来源 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | 使用 [[!DNL PathFactory] 源](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md)将您的访客、会话和页面浏览数据从 [!DNL PathFactory] 集成到 Experience Platform。阅读 [[!DNL PathFactory] 概述](../../sources/connectors/marketing-automation/pathfactory.md)，了解如何开始的信息。 |
| [!DNL Teradata Vantage] | 使用 [[!DNL Teradata Vantage] 源](../../sources/tutorials/ui/create/databases/teradata-vantage.md)将数据从混合多云环境提取到 Experience Platform。阅读 [[!DNL Teradata Vantage] 概述](../../sources/connectors/databases/teradata-vantage.md)，了解如何开始的信息。 |

{style="table-layout:auto"}

**新增和更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 更新 IP 地址以将其列入 VA7 的允许列表 | 以下 IP 地址已添加到 IP 地址列表中，以添加到 VA7（北美）的允许列表中： <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> 要查看要添加到允许列表中的 IP 地址的完整列表，请阅读 [IP 地址允许列表文档](../../sources/ip-address-allow-list.md)。 |
| 支持使用 [!DNL Azure Event Hubs] 源的新身份验证类型 | 您现在可以使用 [!DNL Azure Active Directory Authentication] 或 [!DNL Scoped Azure Active Directory Authentication] 将您的 [!DNL Event Hubs] 源连接到 Experience Platform。 阅读有关 [连接 [!DNL Event Hubs] Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) 的指南，了解更多信息。 |
|  [!DNL Data Landing Zone] 凭证检索更新 | 您现在可以使用源工作区中的右侧栏来检索您的 [!DNL Data Landing Zone] 凭证。您现在还可以使用右侧栏来刷新您的凭证。若要了解更多信息，请阅读 [[!DNL Data Landing Zone] UI 指南](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)。 |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

请参阅[源概述](../../sources/home.md)，了解有关源的更多信息。
