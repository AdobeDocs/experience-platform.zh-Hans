---
title: Adobe Experience Platform 发行说明（2024 年 2 月）
description: Adobe Experience Platform 的 2024 年 2 月发行说明。
exl-id: 7e4b76b7-4027-4890-b869-1dbb79670c3e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1248'
ht-degree: 91%

---

# Adobe Experience Platform 发行说明

**发行日期：2024 年 2 月 21 日**

Experience Platform 中现有功能的更新：

- [警报](#alerts)
- [数据收集](#data-collection)
- [目标](#destinations)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 警报 {#alerts}

通过Experience Platform，您可以为各种Experience Platform活动订阅基于事件的警报。 您可以通过Experience Platform用户界面中的[!UICONTROL 警报]选项卡订阅不同的警报规则，还可以选择在UI中或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 警报历史记录选项卡 | 作为 Experience Platform 管理员，您可以使用管理警报订阅者功能将警报分配给 Adobe 用户 ID、外部电子邮件地址或电子邮件组列表。有关更多信息，请参阅[警报 UI 文档](../../observability/alerts/ui.md)，以获取有关历史记录选项卡的更多信息。 |

{style="table-layout:auto"}

若要了解有关警报的更多信息，请阅读 [[!DNL Observability Insights] 概述](../../observability/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [Web SDK 中的 Web 应用内消息传递支持](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK 现在支持 Adobe Journey Optimizer 活动的 Web 应用内消息传递配置。 |

{style="table-layout:auto"}

要详细了解数据收集，请阅读[数据收集概述](../../tags/home.md)。

<!-- ## Data Prep {#data-prep}

Data Prep allows data engineers to map, transform, and validate data to and from Experience Data Model (XDM).

**New or updated features**

| Feature | Description |
| --- | --- |
| New mapper functions for Adobe Analytics | You can now use the following functions to extract event data from Adobe Analytics: <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> For more information on these functions, read the [Data Prep functions guide](../../data-prep/functions.md) |

{style="table-layout:auto"}

For more information on Data Prep, read the [Data Prep overview](../../data-prep/home.md). -->

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**{#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [Gainsight PX 连接](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX 是一个产品体验平台，使产品团队能够了解用户如何使用他们的产品、收集反馈并创建应用内互动（如产品演示）以推动用户入职和产品采用。 |
| [Mailchimp Tags 连接](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp 是一个流行的营销自动化平台和电子邮件营销服务。您可以使用 Mailchimp Tags 连接器来构造、标记或分类您的联系人。 |
| [SAP Commerce 连接](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce 是面向 B2B 和 B2C 企业的基于云的电子商务平台解决方案，作为 SAP 客户体验产品组合的一部分提供。您可以使用此目标从现有 Experience Platform 受众更新 SAP Commerce 中的客户详细信息。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 激活帐户受众普遍可用 | 现在，购买 Real-time Customer Data Platform [企业对企业](/help/rtcdp/overview.md#rtcdp-b2b)和[企业对个人](/help/rtcdp/overview.md#rtcdp-b2p)版本的公司通常都可以使用激活帐户受众到特定目标的功能。阅读有关[激活帐户受众](/help/destinations/ui/activate-account-audiences.md)的教程，获取完整信息，包括支持的目标。 |
| Google 目标的数字市场法案同意执行工具 | Google 正在发布对 [Google Ads API](https://developers.google.com/google-ads/api/docs/start)、[客户匹配](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)和 [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 的变更，以支持欧盟[数字市场法案](https://digital-markets-act.ec.europa.eu/index_en)（DMA）规定的合规性和同意相关要求（[欧盟用户同意政策](https://www.google.com/about/company/user-consent-policy/)）。这些同意要求的改变预计将于 2024 年 3 月 6 日开始生效。<br/><br/> 为了遵守欧盟用户同意政策并继续为欧洲经济区 (EEA) 的用户创建受众列表，广告商和合作伙伴必须确保在上传受众数据时获得最终用户的同意。作为 Google 合作伙伴，Adobe 为您提供必要的工具，以遵守欧盟 DMA 下的这些同意要求。<br/><br/>已购买 Adobe Privacy &amp; Security Shield 并配置了[同意政策](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)以过滤掉未经同意的配置文件的客户无需采取任何措施。<br/><br/>尚未购买 Adobe Privacy &amp; Security Shield 的客户必须使用 [Segment Builder](../../segmentation/ui/segment-builder.md) 中的[细分定义](../../segmentation/home.md#segment-definitions)功能来过滤掉未经同意的配置文件，以便继续不间断地使用现有的实时 CDP Google 目标。  |
| [!BADGE Beta]{type=Informative} 重新排序批处理目标的映射字段 | 您现在可以通过在[映射](../../destinations/ui/activate-batch-profile-destinations.md#mapping)步骤中拖放映射字段来更改 CSV 导出中列的顺序。UI 中映射字段的顺序反映在导出的 CSV 文件中列的顺序中，从上到下，其中顶行是 CSV 文件中最左边的列。<br/><br/>此功能目前为 Beta 版，仅供 Beta 版客户使用。若要申请访问此项功能，请联系您的 Adobe 代表。 |
| [!BADGE Beta]{type=Informative} 为批量目标预先选定的默认导出计划 | Experience Platform 现在会自动为每个文件导出设置一个默认计划。请参阅有关[安排受众导出](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)的文档，了解如何修改默认时间表。<br/><br/>此功能目前为 Beta 版，仅供 Beta 版客户使用。若要申请访问此项功能，请联系您的 Adobe 代表。 |
| [!BADGE Beta]{type=Informative} 批量修改批处理目标的受众激活时间表 | 您现在可以从[激活数据](../../destinations/ui/destination-details-page.md#bulk-edit-schedule)页面批量编辑多个受众的激活计划。<br/><br/>此功能目前为 Beta 版，仅供 Beta 版客户使用。若要申请访问此项功能，请联系您的 Adobe 代表。 |
| [!BADGE Beta]{type=Informative} 按需批量导出文件至批量目标 | 您现在可以通过[按需导出文件](../../destinations/ui/export-file-now.md)功能将受众批量导出到批量目标。<br/><br/>此功能目前为 Beta 版，仅供 Beta 版客户使用。若要申请访问此项功能，请联系您的 Adobe 代表。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具 | 除了现在支持同意和治理规则的对象类型之外，还可以使用沙盒工具导入未启用统一配置文件的架构，在导入段时检查目标沙盒中缺少的属性，并默认使用现有的合并策略。有关这些功能的更多信息，请参阅[沙盒工具 UI 指南](../../sandboxes/ui/sandbox-tooling.md)。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Experience Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 帐户受众 | 帐户受众现已普遍可用！现在，您可以使用帐户分段功能在Real-time Customer Experience Platform的B2B和B2P版本中从基于人员的受众到基于帐户的受众，轻松而完善地实现营销分段体验。 此版本允许您使用基于人的受众作为基于帐户的受众的谓词，添加搜索功能，支持自定义实体的使用，并符合数据治理。有关此功能的更多信息，请阅读[帐户受众概览](../../segmentation/types/account-audiences.md)。 |

{style="table-layout:auto"}

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom] 源 | 使用 [[!DNL Acxiom Prospecting Data Import] 源](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md)从 [!DNL Acxiom] 潜在客户服务检索数据并将其映射到 Experience Platform。 |

{style="table-layout:auto"}

请参阅[源概述](../../sources/home.md)，了解有关源的更多信息。
