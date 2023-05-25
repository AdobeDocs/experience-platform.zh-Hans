---
title: Adobe Experience Platform发行说明2022年2月
description: Adobe Experience Platform 2022年2月版发行说明。
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: e2342a8a7d03074ac26fbd129a2e7fd520ccb0c3
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 9%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 3 月 7 日**

>[!NOTE]
>
>此版本已从最初的2月23日推迟到3月7日。

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多个 [!DNL dashboards] 通过它，您可以查看有关组织数据的重要见解，如在每日快照期间捕获的数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新的标准目标小组件 | 以下标准构件允许您可视化与目标相关的不同指标。<ul><li>最近激活的区段（按目标）. 此构件根据所选目标以降序显示最近激活的五个前段。</li><li>受众规模趋势. 此构件描述一段时间内映射到目标帐户的区段配置文件计数之间的关系。</li><li>未映射的区段（按标识）. 此构件列出了前五个未映射的区段，它们按给定目标和标识的标识计数以降序顺序排名。</li><li>映射的区段（按标识）. 此构件列出了前五个映射的区段。 区段会根据其各自的源ID计数（与从构件的下拉菜单中选择的目标ID相匹配）从高到低排序。</li><li>普通受众. 此构件提供跨页面顶部选择的目标帐户和构件下拉列表中选择的目标激活的前五个区段的列表。</li></ul> 有关可用标准构件的更多信息，请参见 [目标仪表板文档。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

有关的详细信息 [!DNL Dashboards]，请参阅 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 数据收集 {#data-collection}

Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中丰富和转换数据，并将其分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 改进了数据流配置的UI工作流 | 更新了在数据收集UI中创建新数据流的工作流。 将服务添加到数据流时，只有您有权访问的服务将包含在选项列表中。 请参阅指南，网址为 [配置数据流](../../edge/datastreams/overview.md) 了解更多信息。 |
| 为数据收集准备数据 | 如果您使用的是Adobe Experience Platform Web SDK，您现在可以利用数据准备功能将您的数据映射到服务器端的Experience Data Model (XDM)。 请参阅以下部分： [为数据收集准备数据](../../edge/datastreams/data-prep.md) 有关更多信息，请参阅数据流指南。 |
| 第一方设备Id | 在使用Platform Web SDK收集客户数据时，您现在可以将自己的设备ID发送到Adobe Experience Platform Edge Network，从而为最近对第三方Cookie生命周期的浏览器限制提供了一种解决方法。 请参阅指南，网址为 [第一方设备标识](../../edge/identity/first-party-device-ids.md) 了解更多信息。 |

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新增或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| (Beta)Destination SDK支持基于文件的目标 | [Destination SDK支持基于文件的目标](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) 目前为私人测试版，仅向部分合作伙伴和客户提供。 在正式发布之前，功能和相关文档可能会发生更改。<br><br>请联系您的Adobe客户代表以了解如何访问该功能。 Adobe内部客户代表应联系Experience Platform目标产品和工程团队，讨论支持的用例。 <br><br> 在对基于文件的目标的Destination SDK支持测试阶段，测试版合作伙伴和客户可以使用 [Experience PlatformDestination SDK](../../destinations/destination-sdk/overview.md) 构建专用目标以从以下功能中受益： <ul><li>通过Amazon S3、SFTP服务器、Azure Blob、Azure Data Lake Storage、Data Landing Zone Storage创建基于文件（批量）的目标。</li><li>配置和设置默认文件导出计划和频率选项。</li><li>配置并设置用于设置导出CSV文件格式的选项（分隔符、转义字符和其他选项）。</li><li>能够设置和编辑自定义文件标头。</li><li>能够接收有关文件和区段导出的事件通知。</li><li>能够导出其他文件类型，如CSV、TSV、JSON、Parquet。</li></ul>  <br>要开始使用新功能，请阅读 [（测试版）使用Destination SDK配置基于文件的目标](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> 创建私有或生产化的功能 *流* 所有Experience Platform客户和合作伙伴均已可使用Destination SDK目标。 阅读指南，了解如何 [使用Destination SDK配置流目标](../../destinations/destination-sdk/guides/configure-destination-instructions.md) 了解详细信息。 |

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当您的客户数据分散在不同的系统上，导致每个客户似乎都有多个“身份”时，就会使这一点变得更加困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，帮助您更好地了解客户及其行为。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 的新权限 `view-identity-graph` | 您现在可以使用 `view-identity-graph` 控制组织中的用户是否可以查看身份图数据的权限。 没有此权限的用户将被禁止在UI中或访问时访问身份图查看器 [!DNL Identity Service] 返回身份的API。 请参阅 [访问控制概述](../../access-control/home.md) 以了解有关权限的更多信息。 |

有关以下内容的更多常规信息： [!DNL Identity Service]，请参阅 [Identity服务概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Beta版源迁移至GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).