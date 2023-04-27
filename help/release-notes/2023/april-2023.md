---
title: Adobe Experience Platform发行说明2023年4月
description: 2023年4月的Adobe Experience Platform发行说明。
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: efd69011f1ba81ece0a1c270cc71b9706ab7b88f
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 4 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [实时客户资料](#profile)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供了多个功能板，您可以通过这些功能板查看有关组织数据的重要分析（在每日快照中捕获）。

**新增功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 用户定义的功能板 | 您现在可以 **过滤历史数据** ，并使用近期数据或自定义分析时段。<br>您现在也可以 **复制现有小组件**. 通过自定义副本并编辑其属性，可避免在创建新的独特小组件时从头开始重新启动。 |

{style="table-layout:auto"}

有关功能板的更多信息（包括如何授予访问权限和创建自定义小组件），请首先阅读 [功能板概述](../../dashboards/home.md).

## 数据准备 {#data-prep}

数据准备允许数据工程师映射、转换和验证来自体验数据模型(XDM)的数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 更新了非生产沙箱中Adobe Analytics的回填期 | 非生产沙箱中Adobe Analytics的回填期已缩短为三个月。 生产沙箱的回填在13个月内保持不变。 此更改仅适用于新流量，不会影响现有流量。 有关更多信息，请阅读 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 用于将FPID字符串转换为ECID的新映射器函数 | 使用 `fpid_to_ecid` 函数将FPID字符串转换为ECID，以用于Experience Platform和Experience Cloud应用程序。 有关更多信息，请阅读 [数据准备功能指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有关数据准备的更多信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 数据流的IP地址模糊处理 | 现在，您可以在 [数据流配置UI](../../edge/datastreams/configure.md). <br><br>数据流级别的IP模糊设置优先于在Adobe Target和Audience Manager中配置的任何IP模糊处理。 <br><br>发送到Adobe Analytics的数据不受数据流级别的影响 [!UICONTROL IP模糊处理] 设置。 Adobe Analytics当前接收未模糊处理的IP地址。 要使Analytics接收模糊处理的IP地址，您必须在Adobe Analytics中单独配置IP模糊处理。 此行为将在未来版本中更新。<br><br> 有关IP模糊处理及其配置说明的更多详细信息，请参阅 [数据流配置文档](../../edge/datastreams/configure.md#advanced-options). |
| [数据流配置覆盖](../../edge/datastreams/overrides.md) | 您现在可以为数据流定义其他配置选项，以用于覆盖特定设置，例如事件数据集、Target属性令牌、ID同步容器和Analytics报表包。 <br><br>覆盖数据流配置是两步流程： <ol><li>首先，您必须在 [“数据流配置”页](../../edge/datastreams/configure.md).</li><li>然后，您必须通过Web SDK命令或使用Web SDK将覆盖发送到边缘网络 [标记扩展](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新目标** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 连接](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用SalesforceMarketing Cloud客户参与（以前称为Pardot）目标捕获、跟踪、评分和评分潜在客户。 此目的地适用于涉及多个部门和决策者的B2B用例，这些部门和决策者需要较长的销售和决策周期。 |

{style="table-layout:auto"}

**新增功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 的数据流监控 [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目标 | <p> 您现在可以在 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 和 [具有属性的自定义个性化](../../destinations/catalog/personalization/custom-personalization.md) 连接。 </p> <p>![Adobe Commerce图像](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce量度"){width="100" zoomable="yes"}</p>  请参阅 [在目标工作区中监控数据流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 以了解更多详细信息。 |
| 新建 **[!UICONTROL 将区段ID附加到区段名称]** 字段 [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目标 | <p>您现在可以在 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 从Experience Platform中包含区段ID，如下所示： `Segment Name (Segment ID)`.</p><p>![附加区段ID图像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "新增了“将区段ID附加到区段名称”字段 "){width="100" zoomable="yes"}</p> |

{style="table-layout:auto"}

<!--

| New **[!UICONTROL Append segment ID to segment name]** field for the [!DNL Google Ad Manager] and [!DNL Google Ad Manager 360] destinations | You can now have the segment name in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) and [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) include the segment ID from Experience Platform, like this: `Segment Name (Segment ID)`. |
| Scheduled audience backfills | <p>For the [!DNL Google Display & Video 360] destination, the activation of audience backfills to the destination is scheduled to occur 24-48 hours after a segment is first mapped to a destination connection. This update is in response to Google's policy to wait 24 hours until ingesting data and will improve match rates between Real-time CDP and [!DNL Google Display & Video 360].</p> <p>Note that this is a backend configuration applicable to this destination only and that is unrelated to any customer-configurable scheduling options in the UI.</p> |

-->


**修复和增强功能** {#destinations-fixes-and-enhancements}

- 我们修复了 **排除的身份** 用于基于文件的目标导出的报告量度。 客户会按预期从激活的导出中接收所有导出的ID。 但是， **排除的身份** 由于错误地计数从未导出的身份，UI中的报表量度无法正确显示大量已排除的身份。 (PLAT-149774)
- 我们修复了 **计划** 激活工作流的步骤。 对于需要映射ID的目标，客户无法为添加到现有目标连接的区段添加映射ID。 (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 显示名称切换 | 模式编辑器现在提供了一个切换开关，用于在原始字段名称和更易读的显示名称之间进行更改。 这种灵活性可改进字段发现和编辑架构。 标准字段组的显示名称是系统生成的，但也可以根据需要通过UI进行自定义。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请阅读 [XDM系统概述](../../xdm/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 利用用户档案，可将客户数据整合到统一视图中，为每次客户互动提供一个加盖时间戳的可操作帐户。

**更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 匿名用户档案数据到期 | 现在，通常可以使用假名用户档案数据到期！ 此版本将在启用后，从您的Experience Platform实例中持续删除旧用户档案。 要了解有关此功能和假名用户档案的更多信息，请阅读 [匿名用户档案数据过期指南](../../profile/pseudonymous-profiles.md). |

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，并允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持过滤Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud的行级数据的API | 使用逻辑和比较运算符过滤Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud源的行级数据。 阅读 [使用API过滤源的数据](../../sources/tutorials/api/filter.md) 以了解更多信息。 |
| Shopify Streaming的测试版可用性 | 的 [Shopify流源](../../sources/connectors/ecommerce/shopify-streaming.md) 现已在测试版中提供。 使用Shopify流源从Shopify合作伙伴帐户流式传输数据以Experience Platform。 |
| OneTrust集成的一般可用性 | 的 [OneTrust集成源](../../sources/connectors/consent-and-preferences/onetrust.md) 现在为GA。 使用OneTrust集成源将OneTrust集成帐户中的同意和首选项数据Experience Platform。 |
| oracle服务云的正式发布 | 的 [Oracle服务云源](../../sources/connectors/customer-success/oracle-service-cloud.md) 现在为GA。 使用Oracle服务云源将Oracle服务云数据引入Experience Platform。 |

{style="table-layout:auto"}

要进一步了解来源，请阅读 [源概述](../../sources/home.md).
