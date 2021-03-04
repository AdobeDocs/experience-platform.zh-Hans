---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年3月11日
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 发行说明;
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 3 月 11 日**

Adobe Experience Platform 现有功能的更新包括：

* [[!DNL Data Governance]](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] 允许公司将来自多个企业系统的数据整合在一起，从而使营销人员能够更好地识别、理解和吸引客户。[!DNL Experience Platform] 包括端到端的数据治理基础架构，以确保在系统内和系统之间共享 [!DNL Platform] 数据时正确使用数据。

Adobe Experience Platform [!DNL Data Governance]是用于管理客户数据并确保符合适用于数据使用的法规、限制和政策的一系列战略和技术。 它在[!DNL Experience Platform]的不同级别中起关键作用，包括编目、数据传承、数据使用标签、数据访问策略和营销操作的访问控制数据。

**新增功能**

>[!NOTE]
>
>以下一些新增功能目前处于测试阶段，并非所有用户都可用。 测试版功能可能会发生变化。

| 功能 | 描述 |
| ------- | ----------- |
| 自动执行[!DNL Real-time Customer Data Platform]的数据使用策略 | 数据使用策略现在在将数据激活到目标的工作流中实施。 [!DNL Data Governance] 在进行影响现有激活的更改（如对数据集标签、合并策略、区段定义等）时，也会嵌入并强制执行。 |
| 用于实施的数据世系 | 在实时CDP中违反数据使用策略时，UI会显示一条通知，其中包含数据谱系信息，以帮助用户了解违反策略的原因以及他们可以采取什么措施来解决违规。 |


**已知问题**

* None

有关[!DNL Data Governance]的详细信息，请参阅[数据治理概述](../../data-governance/home.md)。

## 数据获取 {#ingestion}

Adobe Experience Platform提供了一套丰富的功能，用于摄取任何类型的数据和延迟。 Adobe Experience Platform [!DNL Data Ingestion]为获取数据提供了多种替代方法，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批摄取 | 部分批摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功将其所有正确数据收录到Adobe Experience Platform中，同时将其所有不正确的数据分别进行批量处理。 详细信息会添加到不成功的批中，以解释它们未通过验证的原因。 有关部分批摄取的详细信息，请参阅[部分批摄取文档](../../ingestion/batch-ingestion/partial.md)。 |

**已知问题**

* 无

要了解有关将数据引入平台的更多信息，请访问[数据摄取文档](../../ingestion/home.md)。


## 目标 {#destinations}

在[实时客户数据平台](../../rtcdp/overview.md)中，目标是预建的与目标平台集成，这些平台可以无缝地向这些合作伙伴激活数据。

**新目标**

您可以从中激活Adobe Experience Platform数据，新目标可用。 有关详细信息，请参阅以下内容：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | 实时CDP现在可以将区段作为数据文件传送到您的[!DNL Amazon S3]或SFTP云存储位置。 这使您能够通过CSV或制表符分隔的文件将受众及其用户档案属性发送到内部系统。 |
| 广告目的地 | [!DNL Google]目标卡现在分为三个目标卡，用于实时CDP中当前支持的三种不同的[!DNL Google]平台：[!DNL Google Ads]、[!DNL Google Ad Manager]、[!DNL Google]显示和视频360。 |

要了解更多信息，请访问[目标概述](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解客户。 当客户数据在不同系统之间碎片化，导致每个客户似乎具有多个“身份”时，这就变得更加困难。

Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统连接身份，帮助您获得对客户及其行为的更好视图，从而使您能够实时提供有影响力的个性化数字体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的专用图 | 专用图功能已得到增强，可减少图形生成延迟，从每周批处理流程缩短为每天更新的图形，使[!DNL Identity Service]客户能够访问更多最新标识图形和链接。 |

**已知问题**

* 无

有关[!DNL Identity Service]的详细信息，请参阅[Identity Service概述](../../identity-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 已弃用的Adobe Audience Manager连接器信号 | 将不再发送来自受众管理器的信号级数据。 请注意，“特征”和“区段”的区段成员资格仍将包括在内。 由于此更改，将不再生成入站数据集。 |
| 重命名的数据集 | 由受众 Manger连接器生成的数据集将具有更新的名称和说明。 |
| 启用[!DNL Profile]在受众管理器中切换 | [!DNL Profile] 可以启用或禁用切换，以将数据集提升到 [!DNL Real-time Customer Profile]。默认情况下将启用切换。 |
| 云存储系统的UI支持 | UI中[!DNL Azure Data Lake Storage Gen2]的新源连接器。 |
| CRM系统的UI支持 | UI中[!DNL HubSpot]、[!DNL Salesforce Service Cloud]和[!DNL ServiceNow]的新源连接器。 |
| 数据库系统的UI支持 | UI中[!DNL AWS Redshift]、[!DNL Google BigQuery]、[!DNL MariaDB]、[!DNL Microsoft SQL Server]和[!DNL MySQL]的新源连接器。 |

**已知问题**

* 无

要了解有关源的详细信息，请参阅[源概述](../../sources/home.md)。