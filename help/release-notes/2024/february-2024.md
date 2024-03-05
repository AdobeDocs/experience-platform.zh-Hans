---
title: Adobe Experience Platform 发行说明（2024 年 2 月）
description: Adobe Experience Platform 的 2024 年 2 月发行说明。
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 21%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年2月21日**

对Experience Platform中现有功能的更新：

- [警报](#alerts)
- [数据收集](#data-collection)
- [目标](#destinations)
- [沙盒](#sandboxes)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 警报 {#alerts}

Experience Platform允许您订阅各种Platform活动的基于事件的警报。 您可以通过订阅不同的警报规则 [!UICONTROL 警报] 选项卡中，并且可以选择在UI本身中或通过电子邮件通知接收警报消息。
**新增或更新功能**

| 功能 | 描述 | 
| --- | --- | 
| “警报历史记录”选项卡 | 作为Experience Platform管理员，您可以使用管理警报订阅者功能将警报分配给Adobe用户ID、外部电子邮件地址或电子邮件组列表。 欲了解更多信息，请参见 [警报UI文档](../../observability/alerts/ui.md) 有关“历史记录”选项卡的详细信息。 |

{style="table-layout:auto"}

要了解有关警报的更多信息，请阅读 [[!DNL Observability Insights] 概述](../../observability/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [Web SDK中的Web应用程序内消息传送支持](../../web-sdk/personalization/web-in-app-messaging.md) | Adobe Experience Platform Web SDK现在支持Adobe Journey Optimizer促销活动的Web应用程序内消息传递配置。 |

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
| [Gainsight PX连接](../../destinations/catalog/analytics/gainsight-px.md) | Gainsight PX是一个产品体验平台，它使产品团队能够了解用户如何使用其产品、收集反馈和创建应用程序内参与（如产品演练）以推动用户入门和产品采用。 |
| [Mailchimp标记连接](../../destinations/catalog/email-marketing/mailchimp-tags.md) | Mailchimp是一种流行的营销自动化平台和电子邮件营销服务。 您可以使用Mailchimp标记连接器来构建、标记或分类您的联系人。 |
| [SAP Commerce连接](../../destinations/catalog/ecommerce/sap-commerce.md) | SAP Commerce是一种用于B2B和B2C企业的基于云的电子商务平台解决方案，作为SAP客户体验产品组合的一部分提供。 您可以使用此目标从现有Experience Platform受众更新SAP Commerce中的客户详细信息。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 激活一般可用的帐户受众 | 现在，公司普遍可以使用将帐户受众激活到某些目标的功能， [企业对企业](/help/rtcdp/overview.md#rtcdp-b2b) 和 [企业对个人](/help/rtcdp/overview.md#rtcdp-b2p) Real-time Customer Data Platform各版。 阅读有关的教程 [激活帐户受众](/help/destinations/ui/activate-account-audiences.md) 以获取完整的信息，包括支持的目标。 |
| 适用于Google目标的Digital Markets Act同意执行工具 | Google将发布对 [Google Ads API](https://developers.google.com/google-ads/api/docs/start)， [客户匹配](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)，和 [显示和视频360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) ，以支持 [数字市场法案](https://digital-markets-act.ec.europa.eu/index_en) (DMA)在欧盟([欧盟用户同意政策](https://www.google.com/about/company/user-consent-policy/))。 预计这些对同意要求的更改将从2024年3月6日起生效。 <br/><br/> 为了遵循欧盟用户同意政策并继续为欧洲经济区(EEA)中的用户创建受众列表，广告商和合作伙伴必须确保他们在上传受众数据时获得最终用户同意。 作为Google合作伙伴，Adobe会为您提供在欧洲的DMA中遵守这些同意要求的必要工具。<br/><br/>已购买AdobePrivacy &amp; Security Shield并配置了 [同意政策](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 无需执行任何操作，即可过滤掉未经同意的用户档案。<br/><br/>未购买AdobePrivacy &amp; Security Shield的客户必须使用 [区段定义](../../segmentation/home.md#segment-definitions) 中的功能 [区段生成器](../../segmentation/ui/segment-builder.md) 筛选未经同意的用户档案，以便能够继续使用现有的Real-Time CDP Google目标而不会中断。 |
| [!BADGE 测试版]{type=Informational}对批处理目标的映射字段重新排序 | 现在，您可以通过拖放 [映射](../../destinations/ui/activate-batch-profile-destinations.md#mapping) 步骤。 UI中映射字段的顺序反映了导出CSV文件中列的顺序（从上到下），其中顶行是CSV文件中最左侧的列。 <br/><br/> 此功能为测试版，仅向部分客户提供。 要请求访问此功能，请联系您的Adobe代表。 |
| [!BADGE 测试版]{type=Informational}预先选择的批处理目标默认导出计划 | Experience Platform现在会自动为每个文件导出设置默认计划。 请参阅相关文档 [计划受众导出](../../destinations/ui/activate-batch-profile-destinations.md#scheduling) 了解如何修改默认计划。 <br/><br/> 此功能为测试版，仅向部分客户提供。 要请求访问此功能，请联系您的Adobe代表。 |
| [!BADGE 测试版]{type=Informative}批量编辑批处理目标的受众激活计划 | 您现在可以从批量编辑多个受众的激活计划 [激活数据](../../destinations/ui/destination-details-page.md#bulk-edit-schedule) 页面。 <br/><br/> 此功能为测试版，仅向部分客户提供。 要请求访问此功能，请联系您的Adobe代表。 |
| [!BADGE 测试版]{type=Informative}按需将文件批量导出到批处理目标 | 您现在可以通过，将受众批量导出到批量目标 [按需导出文件](../../destinations/ui/export-file-now.md) 功能。 <br/><br/> 此功能为测试版，仅向部分客户提供。 要请求访问此功能，请联系您的Adobe代表。 |

{style="table-layout:auto"}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform旨在丰富全球范围内的数字体验应用程序。 公司通常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署需要，同时确保操作法规遵从性。 为了满足此需求，Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的沙箱，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具 | 除了现在支持同意和治理规则的对象类型外，使用沙盒工具还会导入未启用统一配置文件的架构，在导入区段时检查目标沙盒中是否缺少属性，默认情况下使用现有合并策略。 有关这些功能的详细信息，请参见 [沙盒工具UI指南](../../sandboxes/ui/sandbox-tooling.md). |

{style="table-layout:auto"}

有关沙箱的详细信息，请阅读 [沙盒概述](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 帐户受众 | 帐户受众现已正式可用！ 现在，您可以使用帐户分段功能在Real-time Customer Platform的B2B和B2P版本中从基于人员的受众到基于帐户的受众，来完全简化和完善营销分段体验。 此版本允许您使用基于人员的受众作为基于帐户的受众的谓词，添加搜索功能，支持使用自定义实体，并且与数据管理兼容。 有关此功能的详细信息，请阅读 [帐户受众概述](../../segmentation/ui/account-audiences.md). |

{style="table-layout:auto"}

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE 测试版]{type=Informational} [!DNL Acxiom] 源 | 使用 [[!DNL Acxiom Prospecting Data Import] 源](../../sources/tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md) 以从中检索和映射数据 [!DNL Acxiom] 目标客户服务到Experience Platform。 |

{style="table-layout:auto"}

欲知关于来源的更多信息，请阅读 [源概述](../../sources/home.md).
