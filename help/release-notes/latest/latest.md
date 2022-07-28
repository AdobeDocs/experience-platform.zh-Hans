---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7cb940019905240b36e96b834b9e5d0166c1324d
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 7 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [数据收集](#collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [体验数据模型(XDM)](#xdm)

<!-- - [Real-time Customer Data Platform B2B Edition](#b2b) -->
- [实时客户个人资料](#profile)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供多个 [!DNL dashboards] 通过查看有关贵组织数据的重要信息（在每日快照期间捕获）。

### 帐户配置文件功能板

“帐户配置文件”功能板显示来自营销渠道中多个来源以及贵组织当前用于存储客户帐户信息的各种系统的统一帐户信息快照。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 按行业小组件划分的帐户总数 | 此小组件以单个量度显示帐户总数，并使用圆环图来说明构成整体数量的行业的计数比例大小。 |
| 帐户配置文件添加小组件 | 此小组件使用颜色编码条形图来说明在给定时间段内添加到帐户的用户档案计数，以及构成这些添加用户档案的不同行业的比例。 |

{style=&quot;table-layout:auto&quot;}

请参阅 [Real-time CDP， B2B Edition概述](../../rtcdp/b2b-overview.md) 要进一步了解可用的B2B功能，或 [端到端教程](../../rtcdp/b2b-tutorial.md) 了解有关如何在B2B工作流中创建帐户配置文件的更多信息。

有关可用于显示帐户配置文件相关量度的小组件的更多信息，请参阅 [帐户配置文件小组件文档](../../dashboards/guides/account-profiles.md#standard-widgets).

### 用户档案功能板

“配置文件”功能板显示贵组织在“配置文件存储”(Profile Store)中Experience Platform的属性（记录）数据的快照。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 映射的受众小组件 | 此小组件显示可激活到从“用户档案”功能板下拉列表中选择的目标的已映射受众总数。 |

有关“用户档案”功能板的更多信息，请参阅 [配置文件功能板概述](../../dashboards/guides/profiles.md).

### 目标功能板

“目标”功能板显示贵组织在Experience Platform中启用的目标的快照。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 受众小组件 | 此小组件根据所选的应用于用户档案数据的合并策略，提供准备激活的区段总数。 |

{style=&quot;table-layout:auto&quot;}

要了解有关目标功能板的更多信息，请参阅 [目标功能板概述](../../dashboards/guides/destinations.md).

## 数据收集 {#collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 通过Adobe Admin Console进行权限管理 | 数据收集功能的访问权限现在通过Adobe Admin Console(位于Adobe Experience Platform数据收集的卡下)进行管理。 请参阅 [数据收集权限](../../collection/permissions.md) 以了解更多信息。<br><br>数据流的权限现在也通过Adobe Experience Platform卡下的Admin Console进行管理，与以前为每个用户手动设置这些权限的方法相比，提高了安全性。 |

{style=&quot;table-layout:auto&quot;}

有关详细信息，请参阅 [数据收集概述](../../collection/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 增强了 [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations现在更聪明，速度更快。 新的验证检查可显着减少最常见的映射错误，进一步缩短了实现值的时间。 |
| 对流设置的分层支持 | 您现在可以使用函数 `upsert_array_append` 和 `upsert_array_replace` 用于在流式更新到Profile时更新数组和对象。 请参阅 [[!DNL Data Prep] 映射函数指南](../../data-prep/functions.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

详细了解 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| [立即导出文件（测试版）](../../destinations/ui/export-file-now.md) | 导出完整文件时不会中断先前计划的区段的当前导出计划。 此导出操作除了之前计划的导出之外，还不会更改区段的导出频率。 <br> 文件导出会立即触发，并会从Experience Platform分段运行中获取最新结果。 <br> <br>请联系您的Adobe代表以获取此功能的访问权限。 |

{style=&quot;table-layout:auto&quot;}

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [Marketo V2](../../destinations/catalog/adobe/marketo-engage.md) | Marketo Engage目标更新允许您通过自动化简化静态列表创建过程，并允许用户在其潜在客户中引入其他字段。 请参阅下面有关Marketo V2中增强功能的更多信息： <br><ul><li>在 **[!UICONTROL 计划区段]** 激活工作流的步骤(在Marketo V1中)，您需要手动添加 **映射ID** 成功将数据导出到Marketo。 Marketo V2不再需要此手动步骤。</li><li>在 **[!UICONTROL 映射]** 在Marketo V1中，您能够将XDM字段仅映射到Marketo中的三个目标字段： `firstName`, `lastName`和 `companyName`. 在Marketo V2版本中，您现在可以将XDM字段映射到Marketo中的更多字段。 有关更多信息，请阅读 [Marketo V2中支持的属性](../../destinations/catalog/adobe/marketo-engage.md#supported-attributes).  </li></ul> |
| [Pega客户决策中心](../../destinations/catalog/personalization/pega.md) | 将Pega客户决策中心Adobe Experience Platform中的配置文件属性和区段成员资格信息用作自适应模型中的预测器，并帮助提供下一最佳行动决策 |
| [(API)SalesforceMarketing Cloud](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) | 此目标允许营销人员将Experience Platform中创建的用户区段导入Snapchat Ads，并使用这些区段定位其广告。 |
| [Salesforce CRM](../../destinations/catalog/crm/salesforce.md) | 使用SalesforceMarketing Cloud中的用户档案和区段信息更新SalesforceExperience Platform中的联系信息 |
| [（测试版） [!DNL Snap Inc.]](../../destinations/catalog/advertising/snap-inc.md) | 此目标允许营销人员将Experience Platform中创建的用户区段导入Snapchat Ads，并使用这些区段定位其广告。 <br><br>此目标当前处于测试阶段。 文档和功能可能会发生更改。 |
| [（测试版） [!DNL Trade Desk] - CRM连接](../../destinations/catalog/advertising/tradedesk-emails.md) | 使用 [!DNL The Trade Desk] 将用户档案激活到的CRM目标 [!DNL Trade Desk] 考虑基于CRM数据的受众定位和抑制。 <br><br>此目标当前处于测试阶段。 文档和功能可能会发生更改。 |

{style=&quot;table-layout:auto&quot;}

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 医疗保健行业数据模型 | 已引入标准的医疗保健数据模型，以支持与增加数字采购、改善计划注册和促进药物信息有关的五个常见行业用例。 请参阅 [医疗保健数据模型](../../xdm/schema/industries/healthcare.md) 以了解有关这些用例以及支持这些用例的标准XDM组件的更多信息。<br><br>在 [!UICONTROL 模式] UI可帮助您在构建自定义模式时浏览与医疗保健相关的组件。 |

{style=&quot;table-layout:auto&quot;}

**新的XDM组件**

>[!WARNING]
>
>下表中列出的新XDM组件是试验性组件，目前正在测试中。 在稳定这些组件之前，预计这些组件会通过中断更改（如果需要）进行更新。 请相应地规划您的发展工作。

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 天气]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | 用于捕获天气数据的基于记录的类。 |
| 字段组 | [[!UICONTROL 当前天气]](https://github.com/adobe/xdm/blob/master/components/classes/weather.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 和 [!UICONTROL 天气] 类，用于捕获邮政编码的当前天气条件。 |
| 字段组 | [[!UICONTROL 预测天气]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 和 [!UICONTROL 天气] 类，用于捕获邮政编码的预测天气条件。 |
| 字段组 | [[!UICONTROL 产品触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 和 [!UICONTROL 天气] 类，用于捕获特定于产品的触发器，这些触发器利用已知的天气条件来驱动消费者行为。 |
| 字段组 | [[!UICONTROL 相对触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 和 [!UICONTROL 天气] 类，用于捕获利用已知天气条件来驱动消费者行为的相对触发器。 |
| 字段组 | [[!UICONTROL 严重触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 和 [!UICONTROL 天气] 类，用于捕获触发器，这些触发器利用已知的恶劣天气条件来驱动消费者行为。 |
| 字段组 | [[!UICONTROL 天气触发器]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/weather-triggers.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 和 [!UICONTROL 天气] 类，用于捕获利用已知天气条件来驱动消费者行为的常规触发器。 |
| 字段组 | [[!UICONTROL MediaCollection交互详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-collection.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 类，可捕获有关媒体交互的详细信息。 |
| 字段组 | [[!UICONTROL 媒体报表互动详细信息]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-reporting.schema.json) | 的字段组 [!UICONTROL XDM ExperienceEvent] 类，可捕获有关与媒体报表交互的详细信息。 |
| 数据类型 | [[!UICONTROL 广告详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 捕获有关广告资产的详细信息。 |
| 数据类型 | [[!UICONTROL 广告面板详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json) | 捕获有关广告面板的详细信息，该面板是在单个广告时间内来回播放的多个广告序列。 |
| 数据类型 | [[!UICONTROL 章节详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json) | 捕获一段视频内容中某个章节或区段的详细信息。 |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 捕获有关视频播放错误的详细信息。 |
| 数据类型 | [[!UICONTROL 播放器事件详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/playereventdetails.schema.json) | 捕获有关视频播放器的事件相关详细信息，包括播放头位置和会话ID。 |
| 数据类型 | [[!UICONTROL 播放器状态数据信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json) | 捕获有关视频播放器的状态相关详细信息。 |
| 数据类型 | [[!UICONTROL Qoe数据详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 捕获有关视频播放事件的体验质量(QoE)详细信息。 |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 捕获有关视频播放事件的会话详细信息。 |

{style=&quot;table-layout:auto&quot;}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

<!-- ## Real-time Customer Data Platform B2B Edition {#b2b}

Built on Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition is purpose-built for marketers operating in a business-to-business service model. It brings together data from multiple sources and combines it into a single view of people and account profiles. This unified data allows marketers to precisely target specific audiences and engage those audiences across all available channels.

| Feature | Description |
| Lead to account matching | Lead to account matching allows you to use Real-time CDP B2B edition to match known person profiles to account profiles so that these profiles can be segmented and targeted with B2B context data like account, opportunity (and add something else like don't use etc. to the description). For more information, see the document on [lead to account matching](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md). For a guide on how to monitor profile enrichment, see the document on [monitoring profile enrichment in the UI](../../dataflows/ui/b2b/monitor-profile-enrichment.md). For instructions on how to use related accounts in segment definitions, see the guide on [Segmentation use cases for Real-time Customer Data Platform B2B Edition](../../rtcdp/segmentation/b2b.md#related-accounts)."|

{style="table-layout:auto"}

To learn more about Real-time CDP B2B Edition, see the [Real-time CDP B2B overview](../../rtcdp/overview.md). -->

## 实时客户个人资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将客户数据整合到统一视图中，为每次客户互动提供一个加盖时间戳的可操作帐户。

| 功能 | 描述 |
| ------- | ----------- |
| 孤立的配置文件边缘属性清理（有限版本） | 如果贵组织有权访问此功能，则用户档案服务现在每天都会删除用户活动区域的剩余边缘属性，以便在系统中更准确地呈现您的用户档案。 在删除给定用户档案的所有配置文件片段后，会进行此清理，这会影响从其中合并的数据集合并用户档案 `com_adobe_aep_profile_region_dataset` 标记为true。 这可能会在许可证使用情况功能板的“可寻址受众”量度中显示一个下降，并且可能在“配置文件”功能板的“配置文件计数”量度中显示一个下降，因为这些量度包含此版本之前剩余的边缘属性片段。 |

{style=&quot;table-layout:auto&quot;}

要了解有关实时客户资料的更多信息，包括有关使用资料数据的教程和最佳实践，请首先阅读 [实时客户资料概述](../../profile/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 全面提供 [!DNL Azure Data Explorer] 来源 | 使用AzureData Explorer源从 [!DNL Azure] 实例Experience Platform。 请参阅 [[!DNL Azure Data Explorer] 源概述](../../sources/connectors/databases/data-explorer.md) 以了解更多信息。 |
| 全面提供 [!DNL Generic OData] 来源 | 使用 [!DNL Generic OData] 来源从支持开放数据协议的系统中将资源Experience Platform。 请参阅 [[!DNL Generic OData] 源概述](../../sources/connectors/protocols/odata.md) 以了解更多信息。 |
| 支持自动检测 [!DNL Data Landing Zone] 在Experience PlatformUI中 | 的 [!DNL Data Landing Zone] 现在，源支持在使用Experience PlatformUI时自动检测文件属性。 请参阅 [创建 [!DNL Data Landing Zone] 源连接](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

要进一步了解源，请参阅 [源概述](../../sources/home.md).
