---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年3月11日
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 5%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 3 月 11 日**

对Adobe Experience Platform中现有功能的更新：

* [数据管理](#governance)
* [数据获取](#ingestion)
* [目标](#destinations)
* [标识服务](#identity)
* [源](#sources)

## 数据管理 {#governance}

Experience Platform使公司能够将多个企业系统中的数据整合在一起，从而使营销人员能够更好地识别、理解和吸引客户。 Experience Platform包括端到端的数据治理基础结构，包括数据使用标签和执行(DULE)，以确保在平台内以及在系统之间共享数据时正确使用数据。

Adobe Experience Platform数据治理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。 它在Experience Platform的各个层次(包括编目、数据谱系、数据使用标签、数据访问策略和访问控制数据以执行营销操作)中起着关键作用。

**新增功能**

>[!NOTE]
>
>以下一些新增功能当前处于测试版中，并非所有用户都可使用。 测试版功能可能会发生变化。

| 功能 | 描述 |
| ------- | ----------- |
| 自动执行实时客户数据平台的数据使用策略 | 数据使用策略现在在将数据激活到目标的工作流中实施。 在进行影响现有激活的更改（如对数据集标签、合并策略、细分定义等）时，也会嵌入并强制实施数据管理。 |
| 用于强制实施的数据世系 | 当实时CDP中违反数据使用策略时，UI会显示一条通知，其中包含数据谱系信息，以帮助用户了解违反策略的原因以及他们可以采取哪些措施来解决违规。 |


**已知问题**

* None

有关数据治理的更多信息，请参 [阅数据治理概述](../../data-governance/home.md)。

## 数据获取 {#ingestion}

Adobe Experience Platform提供了丰富的功能集，用于采集任何类型的数据和延迟。 Adobe Experience Platform数据摄取为数据提供多种替代方法，包括批处理API、流式API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience PlatformUI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批摄取 | 部分批量摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功将其所有正确数据引入Adobe Experience Platform，同时单独对其所有错误数据进行批处理。 详细信息会添加到不成功的批中，以解释它们为何未通过验证。 有关部分批摄取的详细信息，请参阅部分 [批摄取文档](../../ingestion/batch-ingestion/partial.md)。 |

**已知问题**

* None

要进一步了解如何将数据引入平台，请访 [问数据获取文档](../../ingestion/home.md)。


## 目标 {#destinations}

在 [Adobe实时客户数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新目标**

您可以在新目标中激活Adobe Experience Platform数据。 有关详细信息，请参阅以下内容：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | Adobe实时CDP现在可以将您的细分作为数据文件传送到Amazon S3或SFTP云存储位置。 这使您能够通过CSV或制表符分隔的文件，将受众及其用户档案属性发送到您的内部系统。 |
| 广告目标 | Google目标卡现在分为三个目标卡，用于Adobe Real-time CDP中当前支持的三种不同的Google平台： Google Ads、Google Ad Manager、Google Display &amp; Video 360。 |

要了解更多信息，请访问目 [标概述](../../rtcdp/destinations/destinations-overview.md)

## 标识服务 {#identity}

提供相关的数字体验需要全面了解客户。 当客户数据在不同的系统中分散，导致每个客户似乎具有多个“身份”时，这就变得更加困难。

Adobe Experience Platform身份服务通过跨设备和系统连接身份帮助您更好地视图客户及其行为，使您能够实时提供有影响力的个性化数字体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的专用图 | 专用图形功能已得到增强，可减少图形生成延迟，从每周批处理缩短为每日更新的图形，使Identity Service客户能够访问更多最新的标识图形和链接。 |

**已知问题**

* None

有关Identity Service的详细信息，请参阅 [Identity Service概述](../../identity-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务来构建、标记和增强该数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager连接器已弃用信号 | 不再发送受众管理器中的信号级数据。 请注意，“特征”和“区段”的区段成员资格仍将包含在内。 由于此更改，将不再生成入站数据集。 |
| 重命名的数据集 | 由受众管理器连接器生成的数据集将具有更新的名称和说明。 |
| 在用户档案管理器中启用受众切换 | 用户档案切换可以启用或禁用，以将数据集提升为实时客户用户档案。 默认情况下将启用切换。 |
| 云存储系统的UI支持 | UI中Azure Data Lake存储Gen2的新源连接器。 |
| CRM系统的UI支持 | UI中HubSpot、Salesforce Service Cloud和ServiceNow的新源连接器。 |
| 数据库系统的UI支持 | AWS Redshift、Google BigQuery、MariaDB、Microsoft SQL Server和MySQL的新源连接器。 |

**已知问题**

* None

要进一步了解源，请参阅 [源概述](../../sources/home.md)。