---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2020年3月11日
doc-type: release notes
last-update: March 10, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Adobe Experience Platform 发行说明

## 发行日期：2020 年 3 月 11 日

## 数据管理

Experience Platform允许公司将来自多个企业系统的数据整合在一起，从而更好地使营销人员能够识别、理解和吸引客户。 Experience Platform包括端对端数据管理基础架构，包括数据使用标签和强制执行(DULE)，以确保在平台内以及在系统之间共享数据时正确使用数据。

Adobe Experience Platform数据管理是用于管理客户数据并确保符合适用于数据使用的法规、限制和政策的一系列战略和技术。 它在Experience Platform的不同级别中起着关键作用，包括编目、数据谱系、数据使用标签、数据访问策略和营销操作的数据访问控制。

### 新增功能

>[!NOTE]
>以下一些新增功能当前处于测试版中，并非所有用户都可使用。 测试版功能可能会发生变化。

| 功能 | 描述 |
| ------- | ----------- |
| 自动执行实时客户数据平台的数据使用策略 | 数据使用策略现在在将数据激活到目标的工作流中得以实施。 在进行影响现有激活的更改（如对数据集标签、合并策略、区段定义等）时，也会嵌入并强制实施数据管理。 |
| 用于实施的数据世系 | 当实时CDP中违反了数据使用策略时，UI会显示一条通知，其中包含数据谱系信息，以帮助用户了解违反策略的原因以及他们可以采取什么措施来解决该冲突。 |


### 已知问题

* None

有关数据管理的详细信息，请参阅数 [据管理概述](../../data-governance/home.md)。

## 数据摄取

Adobe Experience Platform提供一组丰富的功能，用于摄取任何类型的数据和延迟。 Adobe Experience Platform Data Ingestion为获取数据提供了多种替代方法，包括批量API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

### 新增功能

| 功能 | 描述 |
|------- | -----------|
| 部分批量摄取 | 部分批量摄取是指能够摄取包含错误的数据，最高可达到某个阈值。 借助此功能，用户可以成功地将其所有正确数据引入Adobe Experience Platform，同时单独分批其所有错误数据。 详细信息会添加到不成功的批中，以解释它们为何未通过验证。 有关部分批摄取的更多信息，请参阅部分 [批摄取文档](../../ingestion/batch-ingestion/partial.md)。 |

### 已知问题

* None

要了解有关将数据引入平台的更多信息，请访 [问Data Ingestion文档](../../ingestion/home.md)。


## 目标

在 [Adobe实时客户数据平台中](../../rtcdp/overview.md)，目标是预建的与目标平台的集成，这些平台可以无缝地向这些合作伙伴激活数据。

### 新目标

您可以在新目标中激活Adobe Experience Platform数据。 有关详细信息，请参阅以下内容：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | Adobe实时CDP现在可以将区段作为数据文件传送到Amazon S3或SFTP云存储位置。 这使您能够通过CSV或制表符分隔的文件，将受众及其用户档案属性发送到您的内部系统。 |
| 广告目标 | Google目标卡现在分为三个目标卡，用于Adobe实时CDP中当前支持的三个不同的Google平台：Google Ads,Google广告经理，Google Display &amp; Video 360。 |

要了解更多信息，请访问目 [标概述](../../rtcdp/destinations/destinations-overview.md)

## 标识服务

提供相关数字体验需要全面了解客户。 当客户数据在不同系统之间分散，导致每个客户似乎都具有多个“身份”时，这就变得更加困难。

Adobe Experience Platform Identity Service通过跨设备和系统连接身份帮助您更好地视图客户及其行为，使您能够实时提供有影响力的个性化数字体验。

### 新增功能

| 功能 | 描述 |
| ------- | ----------- |
| 增强的专用图 | 专用图形功能已得到增强，可减少图形生成延迟，从每周批处理流程缩短为每日更新的图形，使Identity Service客户能够访问更多最新标识图形和链接。 |

### 已知问题

* None

有关Identity Service的详细信息，请参阅 [Identity Service概述](../../identity-service/home.md)。

## 来源

Adobe Experience Platform可以从外部源中摄取数据，同时允许您使用平台服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)获取数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，为摄取运行设置时间，以及管理数据摄取吞吐量。

### 新增功能

| 功能 | 描述 |
| ------- | ----------- |
| Adobe受众管理器连接器的已弃用信号 | 将不再发送来自受众管理器的信号级数据。 请注意，“特征”和“区段”的区段成员资格仍将包含在内。 由于此更改，将不再生成入站数据集。 |
| 重命名的数据集 | 由受众管理器连接器生成的数据集将具有更新的名称和说明。 |
| 在用户档案管理器中启用受众切换 | 用户档案切换可启用或禁用，以将数据集提升到实时客户用户档案。 默认情况下将启用切换。 |
| 云存储系统的UI支持 | UI中用于Azure Data Lake存储Gen2的新源连接器。 |
| CRM系统的UI支持 | 在UI中为HubSpot、Salesforce Service Cloud和ServiceNow新增源连接器。 |
| 数据库系统的UI支持 | 在UI中为AWS Redshift、Google BigQuery、MariaDB、Microsoft SQL Server和MySQL提供新的源连接器。 |

### 已知问题

* None

要进一步了解源，请参阅源 [概述](../../source-connectors/home.md)。