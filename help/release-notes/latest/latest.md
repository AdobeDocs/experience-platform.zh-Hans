---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 366656346c25cd5206b36c7ff2b9942c5027de17
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 3%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 3 月 7 日**

>[!NOTE]
>
>此版本已从2月23日的原始日期改为3月7日。

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多个 [!DNL dashboards] 通过查看有关贵组织数据的重要分析（在每日快照中捕获）。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 新的标准目标小组件 | 通过以下标准小组件，您可以显示与目标相关的不同量度。<ul><li>最近按目标激活的区段。 此小组件会根据所选目标以降序方式显示前五个最近激活的区段。</li><li>受众大小趋势。 此小组件描述已映射到该目标帐户的区段在一段时间内的用户档案计数之间的关系。</li><li>按身份未映射的区段。 此小组件列出了前五个未映射区段，这些区段按给定目标和身份的降序身份计数排名。</li><li>按身份映射区段。 此小组件列出了前五个映射的区段。 区段会根据与从小组件下拉菜单中选择的目标ID匹配的源ID的相应计数，从高到低进行排序。</li><li>常见受众。 此小组件提供了在页面顶部选择的目标帐户中激活的前五个区段的列表，以及在小组件下拉菜单中选择的目标。</li></ul> 有关可用标准小组件的更多信息，请参阅 [目标仪表板文档。](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html?lang=en#standard-widgets). |

有关 [!DNL Dashboards]，请参阅 [[!DNL Dashboards] 概述](../../dashboards/home.md).

## 数据收集 {#data-collection}

Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 改进了数据流配置的UI工作流 | 更新了在数据收集UI中创建新数据流的工作流。 向数据流添加服务时，选项列表中将仅包含您有权访问的服务。 请参阅 [配置数据流](../../edge/fundamentals/datastreams.md) 以了解更多信息。 |
| 为数据收集准备数据 | 如果您使用的是Adobe Experience Platform Web SDK，您现在可以利用数据准备功能将数据映射到服务器端的Experience Data Model(XDM)。 请参阅 [为数据收集准备数据](../../edge/fundamentals/datastreams.md#data-prep) （详细信息）。 |
| 第一方设备ID | 现在，在使用Platform Web SDK收集客户数据时，您可以将自己的设备ID发送到Adobe Experience Platform Edge Network，这为最近对第三方Cookie生命周期的浏览器限制提供了解决方法。 请参阅 [第一方设备ID](../../edge/identity/first-party-device-ids.md) 以了解更多信息。 |

有关Platform中数据收集的更多信息，请参阅 [数据收集概述](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| （测试版）Destination SDK对基于文件的目标的支持 | [Destination SDK对基于文件的目标的支持](../../destinations/destination-sdk/file-based-destination-configuration.md) 目前为私有测试版，仅适用于数量有限的合作伙伴和客户。 在正式发布之前，功能和相关文档可能会发生更改。<br><br>请联系您的Adobe客户代表以了解如何访问该功能。 Adobe内部客户代表应联系Experience Platform目标产品和工程团队，讨论受支持的用例。 <br><br> 在Destination SDK对基于文件的目标的支持测试阶段，测试合作伙伴和客户可以使用 [Experience PlatformDestination SDK](/help/destinations/destination-sdk/overview.md) 要构建专用目标以从以下功能中受益，请执行以下操作： <ul><li>通过Amazon S3、SFTP服务器、Azure Blob、Azure数据湖存储、数据登陆区存储，创建基于文件的（批处理）目标。</li><li>配置和设置默认文件导出计划和频率选项。</li><li>配置和设置选项，以设置导出的CSV文件的格式（分隔符、转义字符和其他选项）。</li><li>能够设置和编辑自定义文件头。</li><li>能够接收有关文件和区段导出的事件通知。</li><li>能够导出其他文件类型，如CSV、TSV、JSON、Parquet。</li></ul>  <br>要开始使用新功能，请阅读 [（测试版）使用Destination SDK配置基于文件的目标](../../destinations/destination-sdk/file-based-destination-configuration.md). <br><br> 用于创建专用或产品化的功能 *流* 使用Destination SDK的目标已经可供所有Experience Platform客户和合作伙伴使用。 阅读有关如何 [使用Destination SDK配置流目标](/help/destinations/destination-sdk/configure-destination-instructions.md) 以了解详细信息。 |

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 的新权限 `view-identity-graph` | 您现在可以使用 `view-identity-graph` 控制组织中的用户是否能够查看身份图数据的权限。 将禁止没有此权限的用户访问UI中的身份图查看器，或者在访问 [!DNL Identity Service] 返回身份的API。 请参阅 [访问控制概述](../../access-control/home.md) 以了解有关权限的更多信息。 |

有关 [!DNL Identity Service]，请参阅 [Identity Service概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 测试版源迁移至GA | 以下来源已从测试版提升为正式发布： <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
