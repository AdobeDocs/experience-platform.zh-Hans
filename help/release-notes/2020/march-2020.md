---
title: Adobe Experience Platform 发行说明（2020 年 3 月）
description: Adobe Experience Platform 的 2020 年 3 月发行说明。
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 发行说明；
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 20%

---

# Adobe Experience Platform 发行说明

**发行日期： 2020年3月11日**

Adobe Experience Platform 中现有功能的更新：

* [数据治理](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 数据治理 {#governance}

[!DNL Experience Platform]允许公司将来自多个企业系统的数据汇集在一起，以便更好地让营销人员识别、理解和吸引客户。 [!DNL Experience Platform]包括端到端的数据治理基础结构，以确保在[!DNL Experience Platform]内以及在系统之间共享数据时正确使用数据。

Adobe Experience Platform 数据治理是一系列策略和技术，用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策。它在 Experience Platform 的 [!DNL Experience Platform] 各个层面中发挥着关键作用，包括编目、数据谱系、数据使用标记、数据访问策略和营销操作数据访问控制。

**新增功能**

>[!NOTE]
>
>以下某些新功能目前处于测试阶段，并非对所有用户都可用。 Beta功能可能会发生更改。

| 功能 | 描述 |
| ------- | ----------- |
| 自动强制实施[!DNL Real-Time Customer Data Platform]的数据使用策略 | 现在，在将数据激活到目标的工作流中，强制实施数据使用策略。 在进行影响现有激活的更改时（例如更改数据集标签、合并策略、区段定义等），也会嵌入并强制执行数据管理。 |
| 强制实施的数据谱系 | 在Real-Time CDP中违反数据使用策略时，UI会显示包含数据族系信息的通知，以帮助用户了解违反策略的原因以及他们可采取哪些措施来解决违规。 |


**已知问题**

* None

有关数据管理的更多信息，请参阅[数据管理概述](../../data-governance/home.md)。

## 数据引入 {#ingestion}

Adobe Experience Platform提供了一组丰富的功能，可用于摄取任何类型和延迟的数据。 Adobe Experience Platform [!DNL Data Ingestion]提供了多种方法来摄取数据，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批次摄取 | 部分批量摄取是指在一定阈值内摄取包含错误的数据的能力。 借助此功能，用户可以成功地将其所有正确数据摄取到Adobe Experience Platform中，同时对其所有不正确的数据进行单独批处理。 详细信息将添加到不成功的批次以解释它们未通过验证的原因。 有关部分批次摄取的更多信息，请参阅[部分批次摄取文档](../../ingestion/batch-ingestion/partial.md)。 |

**已知问题**

* None

要了解有关将数据摄取到Experience Platform的更多信息，请访问[数据摄取文档](../../ingestion/home.md)。


## 目标 {#destinations}

在[Real-Time Customer Data Platform](../../rtcdp/overview.md)中，目标是与目标平台预先构建的集成，这些平台以无缝方式向这些合作伙伴激活数据。

**新目标**

提供了一些新目标，您可以在其中激活Adobe Experience Platform数据。 有关详细信息，请参阅下文：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | Real-Time CDP现在可以将区段作为数据文件交付到[!DNL Amazon S3]或SFTP云存储位置。 这使您能够通过CSV或制表符分隔的文件将受众及其配置文件属性发送到内部系统。 |
| Advertising目标 | 对于Real-Time CDP中当前支持的三个不同的[!DNL Google]平台，[!DNL Google]目标卡现在拆分为三个目标卡： [!DNL Google Ads]、[!DNL Google Ad Manager]、[!DNL Google]显示和视频360。 |

要了解更多信息，请访问[目标概述](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相关的数字体验要求完全了解您的客户。 当您的客户数据分散在不同的系统中，导致每个客户似乎拥有多个“身份”时，就会更加困难。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的专用图 | 专用图形功能已得到增强，可减少图形生成延迟，从每周批处理流程缩短为每日更新的图形，从而允许[!DNL Identity Service]客户访问更多最新的标识图形和链接。 |

**已知问题**

* None

有关[!DNL Identity Service]的详细信息，请参阅[Identity Service概述](../../identity-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强该数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

[!DNL Experience Platform]提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager连接器的已弃用信号 | 将不再发送来自Audience Manger的信号级数据。 请注意，特征和区段的区段成员资格仍将被包括在内。 由于此更改，将不再生成集客数据集。 |
| 重命名的数据集 | Audience Manger连接器生成的数据集将具有更新的名称和描述。 |
| 在Audience Manger中启用[!DNL Profile]切换 | 可以启用或禁用[!DNL Profile]切换以将数据集提升到[!DNL Real-Time Customer Profile]。 默认情况下将启用切换功能。 |
| 云存储系统的UI支持 | UI中[!DNL Azure Data Lake Storage Gen2]的新源连接器。 |
| CRM系统的UI支持 | UI中[!DNL HubSpot]、[!DNL Salesforce Service Cloud]和[!DNL ServiceNow]的新源连接器。 |
| 数据库系统的UI支持 | UI中[!DNL AWS Redshift]、[!DNL Google BigQuery]、[!DNL MariaDB]、[!DNL Microsoft SQL Server]和[!DNL MySQL]的新源连接器。 |

**已知问题**

* None

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
