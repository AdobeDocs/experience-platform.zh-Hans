---
title: Adobe Experience Platform 发行说明（2022 年 1 月）
description: Adobe Experience Platform 的 2022 年 1 月发行说明。
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 27%

---

# Adobe Experience Platform 发行说明

**发行日期： 2022年1月26日**

Adobe Experience Platform 中现有功能的更新：

- [警报](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 警报 {#alerts}

通过Experience Platform，您可以为各种Experience Platform活动订阅基于事件的警报。 您可以通过Experience Platform用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，还可以选择在UI中或通过电子邮件通知接收警报消息。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 几个新的警报规则现在可用于与数据摄取、身份、用户档案、分段和激活相关的工作流。 有关更新的警报类型列表，请参阅[警报规则](../../observability/alerts/rules.md)的概述。 |
| 源数据流的上下文警报 | 现在，您可以订阅以在摄取工作流期间接收关于数据流状态的警报消息。 有关详细信息，请参阅[在UI中订阅源警报指南](../../sources/tutorials/ui/alerts.md)。 |

有关Experience Platform中警报的更多信息，请参阅[警报概述](../../observability/alerts/overview.md)。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform 提供多个仪表板，通过这些仪表板，可查看在每天保存快照期间捕获的关于您组织的数据的重要见解。

| 功能 | 描述 |
| --- | --- |
| 智能字幕 | 机器学习算法会自动提供有关您的配置文件和受众数据的见解，并展示在30-90天或12个月期间内的模式和趋势。 字幕包含以下信息 <ul><li>总体形状和统计数据</li><li>趋势和突然变化</li><li>季节模式</li><li>意外异常</li></ul> 有关详细信息，请参阅[配置文件功能板](../../dashboards/guides/profiles.md#profiles-count-trend)和[区段功能板](../../dashboards/guides/audiences.md#audience-size-trend)文档。 |
| 功能板清单 | 在一个集中的位置访问预配置的配置文件、区段和目标功能板报表，包括任何已安装的集成，如PowerBI。 有关详细信息，请参阅[[!DNL Dashboards] 清单文档](../../dashboards/inventory.md)。 |
| PowerBI报表模板 | 使用新的PowerBI图表，从配置文件、区段和目标报表数据模型构建、自定义或扩展量度。 自动安装工作流允许您在PowerBI环境中跨组织共享营销见解。 有关详细信息，请参阅[PowerBI报表模板文档](../../dashboards/integrations/power-bi.md)。 |

有关 [!DNL Dashboards] 的详细信息，请查看 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 整合的映射体验 | Experience Platform UI中新的映射界面为您提供一致的映射体验，以便您利用智能映射推荐、手动配置映射规则并调试映射集发生的任何错误。 有关详细信息，请参阅[[!DNL Data Prep] 用户界面指南](../../data-prep/ui/mapping.md)。 |

有关 [!DNL Data Prep] 的详细信息，请查看 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 同一页面和下一页面个性化 | [同页和下一页个性化功能](../../destinations/ui/activate-edge-personalization-destinations.md)为Edge Network上的应用程序提供共享的、可定位的用户视图，以实现营销和客户渠道之间的一致性。 可以通过[Adobe Target连接](../../destinations/catalog/personalization/adobe-target-connection.md)和[自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md)进行此个性化。 要配置同页或下一页个性化营销活动，请参阅[专用教程](../../destinations/ui/activate-edge-personalization-destinations.md)。 |
| 批量目标监控和区段级别量度 | 目标监控功能现已从流式目标扩展到还包括激活数据流的批处理目标和区段级量度。 有关详细信息，请阅读[监视目标仪表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard)、[监视区段作业仪表板](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard)和[区段级别视图](/help/dataflows/ui/monitor-destinations.md#segment-level-view)。 |
| 在UI中计划编辑现有批量激活数据流 | 此版本引入了用于将现有激活数据流计划编辑到批处理目标的选项。 有关详细信息，请读取[将配置文件数据激活到批处理配置文件目标](/help/destinations/ui/activate-batch-profile-destinations.md)。 |
| Marketo目标增强功能 | 使用Marketo Engage的Experience Platform客户可以通过[Marketo目标连接器](/help/destinations/catalog/adobe/marketo-engage.md)将全新人员记录从Experience Platform推送到Marketo Engage，从而最大限度地利用其Marketo数据库。 <br>将受众区段从Experience Platform发送到Marketo Engage时，区段中尚不存在于Marketo Engage数据库中的人员会自动添加到该区段中。 有关详细信息，请参阅[将Adobe Experience Platform区段推送到Marketo静态列表](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html)&#x200B;(教程中的步骤9指示如何将全新人员记录推送到Marketo)。 |

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [Adobe Target连接](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target是一款应用程序，可在网站、移动应用程序等的所有入站客户互动中提供由AI支持的实时个性化和实验。 Adobe Target是Adobe Experience Platform中的个性化连接。 |
| [自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md) | 此个性化连接提供了一种方法，可将区段信息从Adobe Experience Platform检索到外部个性化平台、内容管理系统、广告服务器以及在客户网站上运行的其他应用程序。 |

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## 查询服务 {#query-service}

[!DNL Query Service]允许您使用标准SQL在Adobe Experience Platform [!DNL Data Lake]中查询数据。 您可以加入来自 [!DNL Data Lake] 的任何任何数据集，并将查询结果捕获为新数据集，以用于报告、Data Science Workspace，或将数据摄取到实时客户轮廓。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 匿名块 | 匿名块SQL构造允许您将查询服务中的大规模数据准备作业分解为较小的任务，然后重复使用并依次执行这些任务以进行增量数据加载。 有关详细信息，请参阅匿名块文档的[示例查询](../../query-service/key-concepts/anonymous-block.md)。 |
| 数据集组织 | 提供一个一致的逻辑数据结构，用于随着沙盒中数据资产量的增长组织数据资产以供查询服务使用。 有关详细信息，请参阅[组织数据资产文档](../../query-service/best-practices/organize-data-assets.md)。 |

有关 [!DNL Query Service] 的详细信息，请查看 [[!DNL Query Service] 概述](../../query-service/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙箱，以帮助开发和改进数字体验应用程序。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒用户界面增强 | 沙盒指示器现在集成在所有Experience Platform UI应用程序的标头中。 沙盒指示器显示沙盒名称、区域和类型，还允许您访问下拉菜单以在沙盒之间切换。 有关详细信息，请参阅[沙盒用户界面指南](../../sandboxes/ui/user-guide.md)。 |

有关沙箱的详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 区段匹配 | 区段匹配是一项数据协作服务，它允许两个或更多Experience Platform用户以安全、受管理和隐私友好的方式，基于通用标识符交换数据。 区段匹配使用Experience Platform隐私标准和个人标识符，例如经过哈希处理的电子邮件、经过哈希处理的电话号码和设备标识符（如IDFA和GAID）。 有关详细信息，请参阅[区段匹配概述](../../segmentation/ui/segment-match/overview.md)。 |

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| Beta源迁移到GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs]源增强功能 | [!DNL Event Hubs]源现在支持非根SAS密钥类型的身份验证以连接和创建源连接。 有关详细信息，请参阅[[!DNL Event Hubs] 概述](../../sources/connectors/cloud-storage/eventhub.md)。 |
| [!DNL SFTP]源增强功能 | [!DNL SFTP]源现在允许您建立数据流可用于连接到SFTP服务器的最大并发连接数。 有关详细信息，请参阅[[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md)。 |
