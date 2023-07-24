---
title: Adobe Experience Platform发行说明2022年10月
description: Adobe Experience Platform 2022年10月版发行说明。
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 29%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 10 月 26 日**

- [客户管理的密钥](#cmk)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [查询服务](#query-service)
- [源](#sources-sources)

## 客户管理的密钥 {#cmk}

所有存储在Adobe Experience Platform上的数据都使用系统级别密钥进行静态加密。 如果您使用的是基于Platform构建的应用程序，您现在可以选择使用自己的加密密钥，从而更好地控制数据安全。

请参阅概述，位于 [客户管理的密钥](../../landing/governance-privacy-security/customer-managed-keys.md) 以了解有关该功能的详细信息。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据流的敏感数据处理 | 数据流现在利用多种平台技术适当地处理由诸如健康保险可移植性和责任法案(HIPAA)等法规强制执行的敏感数据。 请参阅以下部分： [处理数据流中的敏感数据](../../datastreams/overview.md#sensitive) 了解更多信息。 |
| [!DNL Splunk] 事件转发的扩展 | 您现在可以将数据发送到 [!DNL Splunk] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Splunk] 扩展概述](../../tags/extensions/server/splunk/overview.md) 了解更多信息。 |
| [!DNL Zendesk] 事件转发的扩展 | 您现在可以将数据发送到 [!DNL Zendesk] 使用 [事件转发](../../tags/ui/event-forwarding/overview.md) 扩展。 请参阅 [[!DNL Zendesk] 扩展概述](../../tags/extensions/server/zendesk/overview.md) 了解更多信息。 |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| (Beta)数据集导出 | 此 [数据集导出测试版功能](/help/destinations/ui/export-datasets.md) 用于导出第一代数据(如 [Real-time Customer Data Platform产品描述](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html))，通过Adobe Experience Platform中的目标用户界面，访问您自己的外部客户系统。 这样，您就可以使用无代码/低代码工作流将数据从Experience Platform中转移到六个云存储目标（如下表中所列），以用于分析和合规性用例。 |
| (Beta)增强的文件导出功能 | 现在，在将文件导出到Experience Platform之外时，您可以受益于增强的自定义功能： <br><ul><li>其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).</li><li>能够通过以下方式设置导出文件中的自定义文件标头： [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> <br> 下表列出的六个新的测试版云存储卡支持此功能。 |

{style="table-layout:auto"}

**新增或更新目标**{#new-or-updated-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line是一个连接人员、服务和信息的流行通信平台，已从聊天应用程序发展为娱乐、社交和日常活动的中心。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365是一个基于云的业务应用程序平台，它将企业资源规划(ERP)、客户关系管理(CRM)与生产力应用程序和AI工具相结合，以实现更加顺畅、受控程度更高的端到端运营、更好的增长潜力和更低的成本。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL (Beta) Adobe Commerce] 目标连接器允许您选择一个或多个要激活到的Real-Time CDP区段 [!DNL Adobe Commerce] 帐户，为购物者提供动态的个性化体验。 范围 [!DNL Adobe Commerce]之后，您可以选择这些Real-Time CDP区段来个性化购物车中的独特优惠，例如“购买2 get 1免费”。 您还可以显示主页横幅，并通过促销优惠修改产品定价，所有这些都可根据Adobe Real-Time CDP区段进行自定义。 |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 创建实时出站连接至 [!DNL Azure Data Lake Storage Gen2] 定期将数据文件从Adobe Experience Platform导出到您自己的存储位置。 这个新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，允许您访问安全的基于云的文件存储设施，以将文件导出到Platform之外。 这个新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 创建实时出站连接至 [!DNL Google Cloud Storage] 定期将数据文件从Adobe Experience Platform导出到您自己的存储桶中。 这个新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta版参与者现在可以看到两项 [!DNL Amazon S3] 在目标目录中并排显示目标卡。 新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta版参与者现在可以看到两项 [!DNL Azure Blob] 在目标目录中并排显示目标卡。 新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta版参与者现在可以看到两项 [!DNL SFTP] 在目标目录中并排显示目标卡。 新的测试版目标提供了增强的文件导出功能，并支持数据集导出。 |

{style="table-layout:auto"}

**新增或更新文档**

| 文档 | 描述 |
| ----------- | ----------- |
| [目标护栏](../../destinations/guardrails.md) | 此页面提供有关激活行为的默认使用量和速率限制。 |

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已更新 `authorized` 字段到字符串。 `season` 和 `episode` 已从整数更改为字符串。 |
| 数据类型 | [[!UICONTROL Advertising 详情信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name` 已重命名为 `friendlyName`、和 `ID` 已重命名为 `name`. |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 已更名为 `name`。 |

{style="table-layout:auto"}

有关 Platform 中 XDM 的详细信息，请查看 [XDM 系统概述](../../xdm/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以从以下位置连接任何数据集 [!DNL Data Lake] 并将查询结果捕获为新数据集，以用于报表、数据科学工作区或将其摄取到实时客户档案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 通过Platform UI监控查询 | 查询服务 [!UICONTROL 计划的查询] 选项卡提高了通过UI查看所有查询作业状态的可见性。 您现在可以从以下位置找到有关查询运行状态的重要信息，包括失败时的错误消息和代码： [!UICONTROL 计划的查询] 选项卡。 您还可以通过UI订阅任何此类查询的警报（根据其状态）。 请参阅 [监控查询文档](../../query-service/ui/monitor-queries.md) 以了解有关此功能的更多信息。 |
| 查询加速报表见解数据模型 | 作为Data Distiller SKU的一部分，查询加速存储允许您减少从数据获得关键见解所需的时间和处理能力。 借助query accelerated store，您可以构建自定义数据模型和/或扩展现有Adobe Real-time Customer Data Platform数据模型，以改进您的报表见解及其可视化效果。 请参阅 [查询加速商店报告分析文档](../../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md) 以了解有关此功能的更多信息。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。Adobe Experience Platform中的新增功能：

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**更新的功能**

| 功能 | 描述 |
| --- | --- | 
| Adobe Workfront源的Beta版本 | 使用 [Adobe Workfront源](../../sources/connectors/adobe-applications/workfront.md) 将您的Workfront数据带入Experience Platform并执行用例，例如将您的工作记录与第三方数据相结合，对工作记录应用历史和时间序列分析，以及使用标准SQL查询工作数据。 有关详细信息，请阅读以下指南： [在UI中创建Workfront源连接](../../sources/tutorials/ui/create/adobe-applications/workfront.md). |

若要了解有关源的更多信息，请阅读[源概述](../../sources/home.md)。
