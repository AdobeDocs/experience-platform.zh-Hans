---
title: Adobe Experience Platform 发行说明（2022 年 2 月）
description: Adobe Experience Platform 的 2022 年 2 月发行说明。
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 17%

---

# Adobe Experience Platform 发行说明

**发行日期： 2022年3月7日**

>[!NOTE]
>
>此版本已从原始日期2月23日更改为3月7日。

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供了多个[!DNL dashboards]，通过它们可以查看有关贵组织数据的重要见解，如在每日快照期间捕获的数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 新的标准目标构件 | 以下标准构件允许您可视化与目标相关的不同量度。<ul><li>目标最近激活的区段。 此构件根据所选目标以降序显示最近激活的前五个区段。</li><li>受众规模趋势。 此构件描述一段时间内映射到目标帐户的区段配置文件计数之间的关系。</li><li>按身份列出的未映射区段。 此构件列出给定目标和身份按身份数降序排列的前五个未映射区段。</li><li>按身份映射的区段。 此构件列出了前五个映射区段。 区段会根据它们各自的源ID计数（与从构件的下拉菜单中选择的目标ID相匹配）从高到低排序。</li><li>常见受众。 此小组件提供了在页面顶部选择的目标帐户中激活的前五个区段列表，以及在小组件下拉列表中选定的目标区段的列表。</li></ul> 有关可用标准小组件的更多信息，请参阅[目标仪表板文档。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets) |

有关 [!DNL Dashboards] 的详细信息，请查看 [[!DNL Dashboards] 概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Experience Platform提供了一套技术，可让您收集客户端客户体验数据并将该数据发送到Adobe Experience Platform Edge Network，可在其中丰富和转换数据，并将其分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 改进了数据流配置的UI工作流 | 更新了在数据收集UI中创建新数据流的工作流。 将服务添加到数据流时，只有您有权访问的服务才会包含在选项列表中。 有关详细信息，请参阅[配置数据流](../../datastreams/overview.md)指南。 |
| 为数据收集准备数据 | 如果您使用的是Adobe Experience Platform Web SDK，则现在可以利用数据准备功能将您的数据映射到服务器端的Experience Data Model (XDM)。 有关详细信息，请参阅数据流指南中有关为数据收集准备[数据](../../datastreams/data-prep.md)的部分。 |
| 第一方设备 ID | 在使用Adobe Experience Platform Web Edge Network收集客户数据时，您现在可以将自己的设备ID发送到Experience Platform Web SDK，从而提供针对第三方Cookie有效期的近期浏览器限制问题的解决方法。 有关详细信息，请参阅[第一方设备ID](../../web-sdk/identity/first-party-device-ids.md)上的指南。 |

有关Experience Platform中数据收集的更多信息，请参阅[数据收集概述](../../collection/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ----------- | ----------- |
| (Beta) Destination SDK支持基于文件的目标 | [Destination SDK对基于文件的目标的支持](../../destinations/destination-sdk/functionality/destination-server/server-specs.md)当前为私有测试版，仅向部分合作伙伴和客户提供。 在正式发布之前，功能和相关文档可能会发生更改。<br><br>请联系您的Adobe客户代表了解如何访问该功能。 Adobe内部客户代表应联系Experience Platform目标产品和工程团队以讨论支持的用例。 <br><br>在Destination SDK对基于文件的目标提供支持的测试阶段，测试版合作伙伴和客户可以使用[Experience Platform Destination SDK](../../destinations/destination-sdk/overview.md)构建专用目标以受益于以下功能： <ul><li>通过Amazon S3、SFTP服务器、Azure Blob、Azure Data Lake Storage、Data Landing Zone Storage创建基于文件的（批量）目标。</li><li>配置和设置默认文件导出计划和频率选项。</li><li>配置并设置用于设置导出CSV文件格式的选项（分隔符、转义字符和其他选项）。</li><li>能够设置和编辑自定义文件标头。</li><li>能够接收有关文件和区段导出的事件通知。</li><li>能够导出其他文件类型，如CSV、TSV、JSON、Parquet。</li></ul>  <br>要开始使用新功能，请阅读[(Beta)使用Destination SDK配置基于文件的目标](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)。 <br><br>所有的Experience Platform客户和合作伙伴都可以使用使用Destination SDK创建私有或产品化的&#x200B;*流式传输*&#x200B;目标的功能。 有关详细信息，请参阅有关如何[使用Destination SDK配置流目标](../../destinations/destination-sdk/guides/configure-destination-instructions.md)的指南。 |

## [!DNL Identity Service] {#identity}

提供相关的数字体验要求完全了解您的客户。 当您的客户数据分散在不同的系统中，导致每个客户似乎拥有多个“身份”时，就会更加困难。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| `view-identity-graph`的新权限 | 您现在可以使用`view-identity-graph`权限来控制组织中的用户是否可以查看身份图数据。 将禁止没有此权限的用户在UI中访问身份图形查看器，或在访问返回身份的[!DNL Identity Service] API时访问它们。 有关权限的更多信息，请参阅[访问控制概述](../../access-control/home.md)。 |

有关[!DNL Identity Service]的更多常规信息，请参阅[Identity Service概述](../../identity-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Beta源迁移到GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。