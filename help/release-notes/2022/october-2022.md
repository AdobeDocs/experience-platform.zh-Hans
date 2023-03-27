---
title: Adobe Experience Platform发行说明2022年10月
description: 2022年10月版Adobe Experience Platform发行说明。
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: cd99ccb7b026565814dd6f268b2a92dda34bc7f0
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 3%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 10 月 26 日**

- [客户管理的密钥](#cmk)

Adobe Experience Platform 现有功能的更新包括：

- [Adobe Experience Platform 发行说明](#adobe-experience-platform-release-notes)
   - [客户管理的密钥 {#cmk}](#customer-managed-keys-cmk)
   - [数据收集 {#data-collection}](#data-collection-data-collection)
   - [\[!DNL Destinations\] {#destinations}](#dnl-destinations-destinations)
   - [体验数据模型(XDM) {#xdm}](#experience-data-model-xdm-xdm)
   - [查询服务 {#query-service}](#query-service-query-service)
   - [源 {#sources}](#sources-sources)

## 客户管理的密钥 {#cmk}

存储在Adobe Experience Platform上的所有数据都将使用系统级别密钥在静态时进行加密。 如果您使用的是基于平台构建的应用程序，您现在可以选择使用自己的加密密钥，从而更好地控制数据安全。

请参阅 [客户管理密钥](../../landing/governance-privacy-security/customer-managed-keys.md) 以了解有关该功能的详细信息。

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技术，允许您收集客户端客户体验数据，并将其发送到Adobe Experience Platform边缘网络，以便对其进行扩充、转换和分发到Adobe或非Adobe目标。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 数据流的敏感数据处理 | 数据流现在利用多种平台技术适当地处理受法规(如健康保险流通和责任法案(HIPAA))强制实施的敏感数据。 请参阅 [处理数据流中的敏感数据](../../edge/datastreams/overview.md#sensitive) 以了解更多信息。 |
| [!DNL Splunk] 事件转发扩展 | 您现在可以将数据发送到 [!DNL Splunk] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Splunk] 扩展概述](../../tags/extensions/server/splunk/overview.md) 以了解更多信息。 |
| [!DNL Zendesk] 事件转发扩展 | 您现在可以将数据发送到 [!DNL Zendesk] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Zendesk] 扩展概述](../../tags/extensions/server/zendesk/overview.md) 以了解更多信息。 |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。 您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新增功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| （测试版）数据集导出 | 的 [数据集导出测试版功能](/help/destinations/ui/export-datasets.md) 允许您导出第一代数据(如 [Real-time Customer Data Platform产品说明](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html))从Adobe Experience Platform通过目标用户界面发送到您自己的外部客户系统。 这样，您就可以通过无代码/低代码工作流将数据从Experience Platform中导出到六个云存储目标（如下表中所示），以便进行分析和法规遵从性用例。 |
| （测试版）增强的文件导出功能 | 现在，在导出文件以外时，您可以从增强的自定义功能中受益： <br><ul><li>其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>能够通过 [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> 下表中列出的六个新的测试版云存储卡支持此功能。 |

{style="table-layout:auto"}

**新目标或更新的目标** {#new-or-updated-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line是一个热门的通信平台，可连接人员、服务和信息，并且已经从聊天应用程序发展为娱乐、社交和日常活动的中心。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365是一个基于云的业务应用程序平台，它将企业资源规划(ERP)和客户关系管理(CRM)与生产力应用程序和AI工具结合在一起，从而实现端到端更顺畅、更受控制的操作、更好的增长潜力和降低成本。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | 的 [!DNL (Beta) Adobe Commerce] 目标连接器允许您选择一个或多个要激活到您的Real-Time CDP区段 [!DNL Adobe Commerce] 帐户为购物者提供动态个性化体验。 在 [!DNL Adobe Commerce]，则可以选择这些Real-Time CDP区段以个性化购物车中的独特选件，如“购买2获取1免费”。 您还可以显示主页横幅并通过促销优惠修改产品定价，所有这些优惠均根据Adobe Real-Time CDP区段进行自定义。 |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 创建实时出站连接到 [!DNL Azure Data Lake Storage Gen2] 定期将数据文件从Adobe Experience Platform导出到您自己的存储位置。 这个新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，授予您访问基于云的安全文件存储工具的权限，以便将文件导出到平台之外。 这个新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 创建实时出站连接到 [!DNL Google Cloud Storage] 定期将数据文件从Adobe Experience Platform导出到您自己的存储段中。 这个新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | 测试版参与者现在看到两个 [!DNL Amazon S3] 目标卡片在目标目录中并排显示。 新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | 测试版参与者现在看到两个 [!DNL Azure Blob] 目标卡片在目标目录中并排显示。 新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | 测试版参与者现在看到两个 [!DNL SFTP] 目标卡片在目标目录中并排显示。 新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |

{style="table-layout:auto"}

**新文档或更新的文档**

| 文档 | 描述 |
| ----------- | ----------- |
| [目标护栏](../../destinations/guardrails.md) | 本页提供与激活行为有关的默认使用和费率限制。 |

有关目标的更多常规信息，请参阅 [目标概述](../../destinations/home.md).

## 体验数据模型(XDM) {#xdm}

XDM是一种开源规范，为引入Adobe Experience Platform的数据提供通用结构和定义（架构）。 通过遵循XDM标准，可以将所有客户体验数据纳入到通用的表示形式中，以更快、更集成的方式提供洞察。 您可以从客户操作中获得有价值的分析，通过区段定义客户受众，以及将客户属性用于个性化目的。

**更新了XDM组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 更新了 `authorized` 字段。 `season` 和 `episode` 已从整数更改为字符串。 |
| 数据类型 | [[!UICONTROL 广告详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 已重命名为 `friendlyName`和 `ID` 已重命名为 `name`. |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 已更名为 `name`。 |

{style="table-layout:auto"}

有关Platform中XDM的更多信息，请参阅 [XDM系统概述](../../xdm/home.md).

## 查询服务 {#query-service}

查询服务允许您使用标准SQL在Adobe Experience Platform中查询数据 [!DNL Data Lake]. 您可以连接 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、Data Science Workspace或摄取到实时客户资料。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 通过Platform UI监控查询 | 查询服务 [!UICONTROL 计划查询] 选项卡通过UI改善了所有查询作业状态的可见性。 现在，您可以从 [!UICONTROL 计划查询] 选项卡。 您还可以通过UI，根据任何这些查询的状态订阅警报。 请参阅 [监视查询文档](../../query-service/ui/monitor-queries.md) 以了解有关此功能的更多信息。 |
| 查询加速报告分析数据模型 | 作为Data Distiller SKU的一部分，查询加速存储使您能够减少从数据中获得关键分析所需的时间和处理能力。 通过查询加速存储，您可以构建自定义数据模型和/或扩展现有的Adobe Real-time Customer Data Platform数据模型，以改进报表分析及其可视化图表。 请参阅 [查询加速存储报告分析文档](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) 以了解有关此功能的更多信息。 |

{style="table-layout:auto"}

有关查询服务的更多信息，请参阅 [查询服务概述](../../query-service/home.md).
Adobe Experience Platform的新增功能：

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- | 
| Adobe Workfront源的测试版可用性 | 使用 [Adobe Workfront源](../../sources/connectors/adobe-applications/workfront.md) 将Workfront数据Experience Platform并执行用例，例如将工作记录与第三方数据结合、对工作记录应用历史和时间序列分析，以及使用标准SQL查询工作数据。 有关更多信息，请阅读 [在UI中创建Workfront源连接](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |

要进一步了解来源，请阅读 [源概述](../../sources/home.md).
