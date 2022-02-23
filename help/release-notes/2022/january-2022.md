---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: 734ce1b3-e270-4c37-958c-88bcc39fbf20
source-git-commit: 6d360721a598ff3fa82169aea608263a09c1f05f
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 1 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Destinations]](#destinations)
- [查询服务](#query-service)
- [沙盒](#sandboxes)
- [分段服务](#segmentation)
- [源](#sources)

## 警报 {#alerts}

Experience Platform允许您订阅各种平台活动的基于事件的警报。 您可以通过 [!UICONTROL 警报] 选项卡，可以选择通过UI本身或电子邮件通知接收警报消息。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 现在，有几个新的警报规则可用于与数据获取、身份、用户档案、分段和激活相关的工作流。 请参阅 [警报规则](../../observability/alerts/rules.md) ，以了解更新的警报类型列表。 |
| 源数据流的上下文关联警报 | 现在，您可以在摄取工作流期间订阅接收有关数据流状态的警报消息。 有关详细信息，请参阅 [在UI中订阅源警报](../../sources/tutorials/ui/alerts.md). |

有关平台中警报的更多信息，请参阅 [警报概述](../../observability/alerts/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关组织数据的重要分析（在每日快照中捕获）。

| 功能 | 描述 |
| --- | --- |
| 智能字幕 | 机器学习算法可自动提供对用户档案和受众数据的分析，并展示30-90天或12个月期间的模式和趋势。 字幕包括 <ul><li>总体形状和统计</li><li>趋势和突变</li><li>季节性模式</li><li>意外异常</li></ul> 有关详细信息，请参阅 [配置文件功能板](../../dashboards/guides/profiles.md#profiles-count-trend) 和 [区段功能板](../../dashboards/guides/segments.md#audience-size-trend) 文档。 |
| 功能板清单 | 在集中位置访问预配置的配置文件、区段和目标功能板报表，包括任何已安装的集成（如PowerBI）。 有关更多信息，请参阅 [[!DNL Dashboards] 库存文档](../../dashboards/inventory.md). |
| PowerBI报表模板 | 使用新的PowerBI图表从配置文件、区段和目标报表数据模型构建、自定义或扩展量度。 自动安装工作流允许您从PowerBI环境中在您的组织内共享营销分析。 有关更多信息，请参阅 [PowerBI报表模板文档](../../dashboards/integrations/power-bi.md). |

有关 [!DNL Dashboards]，请参阅 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 整合的映射体验 | Platform UI中的新映射界面为您提供了一致的映射体验，以便利用智能映射推荐、手动配置映射规则以及调试映射集中发生的任何错误。 有关更多信息，请参阅 [[!DNL Data Prep] UI指南](../../data-prep/ui/mapping.md). |

有关 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 同页和下一页个性化 | 的 [同页和下一页个性化功能](../../destinations/ui/configure-personalization-destinations.md) 为Experience Edge上的应用程序提供了用户的共享、可定位视图，以保持营销渠道和客户渠道之间的一致性。 此个性化可通过 [Adobe Target连接](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md). 要配置同页或下一页个性化促销活动，请参阅 [专用教程](../../destinations/ui/configure-personalization-destinations.md). |
| 批量目标监控和区段级别量度 | 目标监控功能现已从流目标扩展到还包含激活数据流的批处理目标和区段级别量度。 有关更多信息，请阅读 [监控目标仪表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard), [监控区段作业仪表板](/help/dataflows/ui/monitor-destinations.md#monitoring-segment-jobs-dashboard)和 [区段级别视图](/help/dataflows/ui/monitor-destinations.md#segment-level-view). |
| 在UI中为现有的批量激活数据流计划编辑 | 此版本引入了用于编辑现有激活数据流到批处理目标的计划的选项。 有关更多信息，请阅读 [将配置文件数据激活到批处理配置文件目标](/help/destinations/ui/activate-batch-profile-destinations.md). |
| Marketo目标增强功能 | 使用Marketo Engage的Experience Platform客户可以通过Marketo将新人员记录从Marketo Engage推送到Experience Platform，从而最大限度地提升其数据库 [Marketo目标连接器](/help/destinations/catalog/adobe/marketo-engage.md). <br> 在将受众区段从Experience Platform发送到Marketo Engage时，可以自动将区段中Marketo Engage数据库中不存在的人添加到受众区段中。 有关更多信息，请阅读 [将Adobe Experience Platform区段推送到Marketo静态列表](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list.html?lang=en) (本教程中的步骤9指示如何将新人员记录推送到Marketo)。 |

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [Adobe Target连接](../../destinations/catalog/personalization/adobe-target-connection.md) | Adobe Target是一款应用程序，可跨网站、移动设备应用程序等的所有入站客户交互提供基于AI的实时个性化和实验。 Adobe Target是Adobe Experience Platform中的一个个性化连接。 |
| [自定义个性化连接](../../destinations/catalog/personalization/custom-personalization.md) | 此个性化连接提供了一种方法，用于从Adobe Experience Platform检索区段信息到外部个性化平台、内容管理系统、广告服务器以及在客户网站上运行的其他应用程序。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 查询服务 {#query-service}

[!DNL Query Service] 允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以连接 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、Data Science Workspace或摄取到实时客户资料。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 匿名块 | 匿名块SQL结构允许您将查询服务中的大规模数据准备作业分解为较小的任务，然后为增量数据加载依次重复使用和执行这些任务。 有关更多信息，请参阅 [匿名块文档的示例查询](../../query-service/best-practices/anonymous-block.md). |
| 数据集组织 | 提供了一种连贯的逻辑数据结构，用于随着沙盒中数据资产数量的增加，组织数据资产以与查询服务一起使用。 有关更多信息，请参阅 [组织数据资产文档](../../query-service/best-practices/organize-data-assets.md). |

有关 [!DNL Query Service]，请参阅 [[!DNL Query Service] 概述](../../query-service/home.md).

## 沙盒 {#sandboxes}

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。 为了满足这一需求，Experience Platform提供了将单个Platform实例分区为单独虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒UI增强 | 沙盒指示器现在集成在所有Platform UI应用程序的标头中。 沙盒指示器可显示沙盒名称、区域和类型，并允许您访问下拉菜单以在沙盒之间切换。 有关更多信息，请参阅 [sandbox UI指南](../../sandboxes/ui/user-guide.md). |

有关沙箱的详细信息，请参阅 [沙箱概述](../../sandboxes/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 区段匹配 | 区段匹配是一项数据协作服务，允许两个或更多Platform用户以安全、受管理和隐私友好的方式，基于通用标识符交换数据。 区段匹配使用平台隐私标准和个人标识符（如经过哈希处理的电子邮件、经过哈希处理的电话号码），以及设备标识符（如IDFA和GAID）。 有关更多信息，请参阅 [区段匹配概述](../../segmentation/ui/segment-match/overview.md). |

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| 测试版源迁移至GA | 以下来源已从测试版提升为正式发布： <ul><li>[[!DNL Snowflake]](../../sources/connectors/databases/snowflake.md)</li><li>[[!DNL Veeva CRM]](../../sources/connectors/crm/veeva.md)</li></ul> |
| [!DNL Event Hubs] 源增强功能 | 的 [!DNL Event Hubs] 源现在支持非根SAS密钥类型的身份验证，以连接和创建源连接。 有关更多信息，请参阅 [[!DNL Event Hubs] 概述](../../sources/connectors/cloud-storage/eventhub.md). |
| [!DNL SFTP] 源增强功能 | 的 [!DNL SFTP] “源”现在允许您建立数据流可用于连接到SFTP服务器的最大并发连接数。 有关更多信息，请参阅 [[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md). |
