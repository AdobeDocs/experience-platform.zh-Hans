---
title: Adobe Experience Platform 发行说明（2022 年 10 月）
description: Adobe Experience Platform 的 2022 年 10 月发行说明。
exl-id: 61ef2472-5e79-433f-9f60-b1245f619b42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 33%

---

# Adobe Experience Platform 发行说明

**发行日期： 2022年10月26日**

- [客户管理的密钥](#cmk)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [查询服务](#query-service)

## 客户管理的密钥 {#cmk}

存储在Adobe Experience Platform上的所有数据都使用系统级别密钥静态加密。 如果您使用的是基于Experience Platform构建的应用程序，则现在可以选择改用您自己的加密密钥，从而使您能够更好地控制数据安全。

有关该功能的详细信息，请参阅[客户管理的密钥](../../landing/governance-privacy-security/customer-managed-keys/overview.md)的概述。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据流的敏感数据处理 | 数据流现在利用多种Experience Platform技术适当处理由健康保险便携性和责任法案(HIPAA)等法规强制执行的敏感数据。 有关详细信息，请参阅[处理数据流中的敏感数据](../../datastreams/overview.md#sensitive)部分。 |
| 用于事件转发的[!DNL Splunk]扩展 | 您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Splunk]。 有关更多信息，请参阅[[!DNL Splunk] 扩展概述](../../tags/extensions/server/splunk/overview.md)。 |
| 用于事件转发的[!DNL Zendesk]扩展 | 您现在可以使用[事件转发](../../tags/ui/event-forwarding/overview.md)扩展将数据发送到[!DNL Zendesk]。 有关更多信息，请参阅[[!DNL Zendesk] 扩展概述](../../tags/extensions/server/zendesk/overview.md)。 |

{style="table-layout:auto"}

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| (Beta)数据集导出 | [数据集导出Beta功能](/help/destinations/ui/export-datasets.md)允许您通过目标用户界面将第一代数据(如[Real-Time Customer Data Platform产品描述](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)中的定义)从Adobe Experience Platform导出到您自己的外部客户系统。 这让您能够借助无代码/低代码工作流将数据从Experience Platform导出到六个云存储目标（如下表中所列），以用于分析和合规性用例。 |
| (Beta)增强的文件导出功能 | 现在，在从Experience Platform导出文件时，您可以受益于增强的自定功能：<br><ul><li>额外的[文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。</li><li>可通过[改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)在您导出的文件中设置自定义文件头。</li><li>[能够自定义导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。</li></ul> <br>下表列出的六个新的Beta版云存储卡支持此功能。 |

{style="table-layout:auto"}

**新增或更新目标**{#new-or-updated-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Line]](../../destinations/catalog/mobile-engagement/line.md) | Line是一个连接人员、服务和信息的流行通信平台，已从聊天应用程序发展为娱乐、社交和日常活动的中心。 |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Microsoft Dynamics 365是一个基于云的业务应用程序平台，它将企业资源规划(ERP)、客户关系管理(CRM)与工作效率应用程序和AI工具相结合，以实现端到端更顺畅、更可控的运营、更好的增长潜力和更低的成本。 |
| [[!DNL (Beta) Adobe Commerce]](../../destinations/catalog/personalization/adobe-commerce.md) | [!DNL (Beta) Adobe Commerce]目标连接器允许您选择一个或多个要激活到[!DNL Adobe Commerce]帐户的Real-Time CDP区段，以便为购物者提供动态的个性化体验。 在[!DNL Adobe Commerce]内，您可以选择这些Real-Time CDP区段来个性化购物车中的独特优惠，例如“购买2 get 1免费”。 您还可以显示主页横幅，并通过促销优惠修改产品定价，所有这些都可根据Adobe Real-Time CDP区段进行自定义。 |
| [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 创建通往 [!DNL Azure Data Lake Storage Gen2] 的实时出站连接以定期将数据文件从 Adobe Experience Platform 导出到您自己的存储位置。这个新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | [!DNL Data Landing Zone]是由Adobe Experience Platform设置的[!DNL Azure Blob]存储接口，它授予您一个安全、基于云的文件存储工具的访问权限，以便将文件导出到Experience Platform中。 这个新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 创建通往 [!DNL Google Cloud Storage] 的实时出站连接以定期将数据文件从 Adobe Experience Platform 导出到您自己的存储桶中。这个新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | Beta参与者现在可以在目标目录中并排看到两个[!DNL Amazon S3]目标卡片。 新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | Beta参与者现在可以在目标目录中并排看到两个[!DNL Azure Blob]目标卡片。 新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |
| [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog) | Beta参与者现在可以在目标目录中并排看到两个[!DNL SFTP]目标卡片。 新的测试版目标提供了增强的文件导出功能并支持数据集导出。 |

{style="table-layout:auto"}

**新增或更新文档**

| 文档 | 描述 |
| ----------- | ----------- |
| [目标护栏](../../destinations/guardrails.md) | 本页提供有关激活行为的默认使用量和速率限制。 |

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**更新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已将`authorized`字段从布尔类型更新为字符串。 `season`和`episode`已从整数更改为字符串。 |
| 数据类型 | [[!UICONTROL Advertising 详情信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `name`已重命名为`friendlyName`，`ID`已重命名为`name`。 |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID`已重命名为`name`。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform [!DNL Data Lake] 中的数据。您可以加入来自 [!DNL Data Lake] 的任何任何数据集，并将查询结果捕获为新数据集，以用于报告、Data Science Workspace，或将数据摄取到实时客户轮廓。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 通过Experience Platform UI监控查询 | 查询服务[!UICONTROL 计划查询]选项卡通过UI提高了所有查询作业状态的可见性。 您现在可以从[!UICONTROL 计划的查询]选项卡中找到有关查询运行状态的重要信息，包括失败时的错误消息和代码。 您还可以通过UI根据这些查询的状态订阅警报。 请参阅[监视器查询文档](../../query-service/ui/monitor-queries.md)以了解有关此功能的详细信息。 |
| 查询加速报表见解数据模型 | 作为Data Distiller SKU的一部分，查询加速存储允许您减少从数据获得关键见解所需的时间和处理能力。 借助查询加速存储，您可以构建自定义数据模型和/或扩展现有Adobe Real-Time Customer Data Platform数据模型，以改进您的报表见解及其可视化效果。 请参阅[query accelerated store reporting insights文档](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md)以了解有关此功能的更多信息。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。
Adobe Experience Platform 的新功能：

