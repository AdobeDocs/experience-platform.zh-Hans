---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年3月11日
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 5%

---


# Adobe Experience Platform 发行说明

**发行日期：2020 年 3 月 11 日**

Adobe Experience Platform现有功能更新：

* [[!DNL数据管理]](#governance)
* [[!DNL数据摄取]](#ingestion)
* [[!DNL目标]](#destinations)
* [[!DNL标识服务]](#identity)
* [[!DNL源]](#sources)

## [!DNL Data Governance] {#governance}

[!DNL Experience Platform] 允许公司将来自多个企业系统的数据整合在一起，从而更好地允许营销人员识别、理解和吸引客户。 [!DNL Experience Platform] 包括端对端数据治理基础架构，确保在系统内和系统之间 [!DNL Platform] 正确使用数据。

Adobe Experience Platform [!DNL Data Governance] 是用于管理客户数据并确保遵守适用于数据使用的法规、限制和政策的一系列战略和技术。 它在各个层次中都起 [!DNL Experience Platform] 着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和访问控制营销行动的数据。

**新增功能**

>[!NOTE]
>
>以下一些新增功能当前处于测试版中，并非所有用户都可使用。 测试版功能可能会发生变化。

| 功能 | 描述 |
| ------- | ----------- |
| 自动执行 [!DNL Real-time Customer Data Platform] | 数据使用策略现在在将数据激活到目标的工作流中实施。 [!DNL Data Governance] 在进行影响现有激活的更改（如对数据集标签、合并策略、段定义等）时，也会嵌入并强制执行。 |
| 用于强制实施的数据世系 | 当实时CDP中违反数据使用策略时，UI会显示一条通知，其中包含数据谱系信息，以帮助用户了解违反策略的原因以及他们可以采取哪些措施来解决违规。 |


**已知问题**

* None

有关详细信息， [!DNL Data Governance]请参阅“ [数据治理”概述](../../data-governance/home.md)。

## 数据获取 {#ingestion}

Adobe Experience Platform提供丰富的功能集，可采集任何类型和延迟的数据。 Adobe Experience Platform [!DNL Data Ingestion] 提供了多种数据替代方法，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience PlatformUI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批摄取 | 部分批量摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功将其所有正确数据引入Adobe Experience Platform，同时单独分批其所有错误数据。 详细信息会添加到不成功的批中，以解释它们为何未通过验证。 有关部分批摄取的详细信息，请参阅部分 [批摄取文档](../../ingestion/batch-ingestion/partial.md)。 |

**已知问题**

* None

要进一步了解如何将数据引入平台，请访 [问数据获取文档](../../ingestion/home.md)。


## 目标 {#destinations}

在 [Adobe实时数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台集成，以无缝方式向这些合作伙伴激活数据。

**新目标**

您可以在新的目的地激活Adobe Experience Platform数据。 有关详细信息，请参阅以下内容：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | Adobe实时CDP现在可以将细分作为数据文件提供到您或SFTP [!DNL Amazon S3] 云存储位置。 这使您能够通过CSV或制表符分隔的文件，将受众及其用户档案属性发送到您的内部系统。 |
| 广告目标 | 目 [!DNL Google] 标卡现在分为三个目标卡，用于Adobe实时 [!DNL Google] CDP中当前支持的三个不同平台： [!DNL Google Ads]、 [!DNL Google Ad Manager]显示 [!DNL Google] 和视频360。 |

要了解更多信息，请访问目 [标概述](../../rtcdp/destinations/destinations-overview.md)

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解客户。 当客户数据在不同的系统中分散，导致每个客户似乎具有多个“身份”时，这就变得更加困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统连接身份，帮助您更好地视图客户及其行为，从而实时提供有影响力的个性化数字体验。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的专用图 | 专用图形功能已得到增强，可减少图形生成延迟，从每周批处理流程缩短为每日更新的图形，使 [!DNL Identity Service] 客户能够访问更多最新的标识图形和链接。 |

**已知问题**

* None

有关详细信息， [!DNL Identity Service]请参阅Identity [Service概述](../../identity-service/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用服务来构建、标记和增强该 [!DNL Platform] 数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

[!DNL Experience Platform] 提供REST风格的API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager连接器已弃用信号 | 不再发送受众管理器中的信号级数据。 请注意，“特征”和“区段”的区段成员资格仍将包含在内。 由于此更改，将不再生成入站数据集。 |
| 重命名的数据集 | 由受众管理器连接器生成的数据集将具有更新的名称和说明。 |
| 启用 [!DNL Profile] 在受众管理器中切换 | [!DNL Profile] 可启用或禁用切换以将数据集提升到 [!DNL Real-time Customer Profile]。 默认情况下将启用切换。 |
| 云存储系统的UI支持 | UI中新的 [!DNL Azure Data Lake Storage Gen2] 源连接器。 |
| CRM系统的UI支持 | UI中、、 [!DNL HubSpot]和 [!DNL Salesforce Service Cloud]新 [!DNL ServiceNow] 的源连接器。 |
| 数据库系统的UI支持 | UI中、、、 [!DNL AWS Redshift]和 [!DNL Google BigQuery]的新 [!DNL MariaDB]源连接 [!DNL Microsoft SQL Server][!DNL MySQL] 器。 |

**已知问题**

* None

要进一步了解源，请参阅 [源概述](../../sources/home.md)。