---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 的 2024 年 3 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d698bf0b8b0dbdb85909008bb3b60efb0575accc
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 33%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年3月19日**

>[!TIP]
>
>使用 [Adobe Experience Platform术语表](/help/landing/glossary.md) 以熟悉Real-time Customer Data Platform和Adobe Experience Platform中使用的术语。 如果找不到要查找的特定术语，请使用页面上的反馈选项来请求将新术语添加到术语表中。

对Experience Platform中现有功能的更新：

- [目录服务](#catalog-service)
- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然摄取到Experience Platform中的所有数据都作为文件和目录存储在数据湖中，但Catalog包含这些文件和目录的元数据和描述，以用于查找和监控目的。

| 功能 | 描述 |
| --- | --- |
| 更多操作 | 为了使操作更灵活并帮助您管理数据，您现在可以使用详细信息视图中的“更多操作”功能来对数据集执行其他任务。 您可以从所选数据集的详细信息页面中删除该数据集或启用它以用于实时客户个人资料。<br>**注意：** 如果为配置文件摄取启用数据集，则该数据集的架构必须与实时客户配置文件兼容。<br>![具有的数据集工作区 [!UICONTROL ...更多] 下拉菜单突出显示。](../2024/assets/march/more-actions.png "突出显示更多下拉菜单的数据集工作区。"){width="100" zoomable="yes"}。<br>阅读 [数据集用户指南](../../catalog/datasets/user-guide.md) 文档，以了解其他信息。 |

{style="table-layout:auto"}

有关目录服务的详细信息，请参阅[目录服务概述](../../catalog/home.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics的新映射器函数 | 现在，您可以使用以下函数从Adobe Analytics中提取事件数据： <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> 有关这些功能的详细信息，请参阅 [数据准备函数指南](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

有关数据准备的详细信息，请阅读 [数据准备概述](../../data-prep/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Merkury] 标记扩展 | 此 [[!DNL Merkury] 标记扩展](https://exchange.adobe.com/apps/ec/600027/merkury-tag) 为匿名网站访客提供行业领先的匹配率， [!DNL Merkury] 标识。 品牌可以利用 [!DNL Merkury] 标记和Adobe，以提供实时的个性化网站体验。 此外， [!DNL Merkury] tag支持第一方数字数据以及连接的在线和离线客户档案的增长。 |

{style="table-layout:auto"}

要了解有关数据收集的更多信息，请阅读 [数据收集概述](../../tags/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新的和更新的目标** {#new-updated-destinations}

| 目标 | 类型 | 描述 |
| ----------- | --------- | ----------- |
| [(Beta) Acxiom数据增强连接](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | 新增 | 使用此连接器可将第一方配置文件从Real-Time CDP激活到Acxiom，以便跨营销渠道扩充和使用该配置文件。 然后，您可以使用Acxiom源导入具有增强数据的用户档案，并在Real-Time CDP中使用这些用户档案。 |
| [(Beta) Acxiom潜在客户抑制连接](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | 新增 | 将您的第一方受众导出到Acxiom目标，以允许Acxiom抑制已知或转换的客户。 然后，使用 [Acxiom潜在客户数据导入](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) 源连接器，用于从Acxiom中摄取和激活潜在客户列表，并删除您的已知或转换的客户。 |
| [Amazon Ads连接](../../destinations/catalog/advertising/amazon-ads.md) | 更新 | 将数据导出到Amazon广告目标时，您现在可以将数据路由到Amazon DSP或AmazonMarketing Cloud（新）。 |
| [LiveRamp载入连接](../../destinations/catalog/advertising/liveramp-onboarding.md) | 更新 | LiveRamp载入目标现在支持向欧洲和澳大利亚投放 [!DNL LiveRamp] [!DNL SFTP] 实例。 最大导出文件大小也增加到了1000万行（以前是500万行）。 |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Experience PlatformUI映射数据类型支持 | 通过在Platform UI中定义映射字段，进一步自定义您的Experience Data Model (XDM)数据结构。 现在，您可以在架构编辑器中创建映射字段以建模灵活的数据结构或有效地存储键值对。 定义新字段时，从类型下拉列表中选择“映射”，以配置子字段并将它们分配给字段组。 支持的映射值类型为字符串和整数。<br>![模式编辑器，其中高亮显示了“Type”和“Map”值类型字段。](../2024/assets/march/maps.png "模式编辑器，其中高亮显示了“Type”和“Map”值类型字段。"){width="100" zoomable="yes"}<br> 学习如何 [在UI中定义映射字段](../../xdm/ui/fields/map.md)，请参阅UI指南。 |

{style="table-layout:auto"}

有关 Platform 中 XDM 的详细信息，请查看 [XDM 系统概述](../../xdm/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 批量操作 | 受众库现在支持批量操作。 通过使用批量操作，您可以快速选择多个受众以将它们移动到文件夹、应用标记、应用访问标签或删除。 <br> ![受众UI工作区中的批量操作。](../2024/assets/march/bulk-actions.png "受众UI工作区中的批量操作。"){width="100" zoomable="yes"} <br>有关此功能的详细信息，请参阅 [分段服务UI指南](../../segmentation/ui/overview.md#bulk-actions). |

{style="table-layout:auto"}

要了解有关分段服务的更多信息，请阅读 [分段服务概述](../../segmentation/home.md).

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新的和更新的源**

| 功能 | 类型 | 描述 |
| --- | --- | --- |
| [!BADGE 测试版]{type=Informational} [!DNL Acxiom Data Ingestion] | 新增 | 使用 [[!DNL Acxiom Data Ingestion] 源](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) 摄取 [!DNL Acxiom] 将数据导入Real-time Customer Data Platform并丰富第一方配置文件。 然后，您可以使用 [!DNL Acxiom] — 扩充了第一方用户档案，以改进受众并在营销渠道之间激活。 <br> ![Acxiom数据摄取源。](../2024/assets/march/acxiom-data-ingestion.png "新的Acxiom数据摄取源。"){width="100" zoomable="yes"} <br> 阅读 [[!DNL Acxiom Data Ingestion] 概述](../../sources/connectors/data-partners/acxiom-data-ingestion.md) 以获取有关如何开始的信息。 |
| [!BADGE 测试版]{type=Informational} [!DNL Stripe] | 新增 | 使用 [[!DNL Stripe] 源](../../sources/connectors/payments/stripe.md) 将客户在购买流程中捕获的数据摄取到Experience Platform中。 摄取数据后，您即可使用此数据创建个性化优惠并解锁更丰富的业务洞察。 <br> ![Stripe源。](../2024/assets/march/stripe.png "新Stripe源。"){width="100" zoomable="yes"} <br> 阅读 [[!DNL Stripe] 概述](../../sources/connectors/payments/stripe.md) 以获取有关如何开始的信息。 |
| 的UI支持 [!DNL Snowflake Streaming] | 新增 | 您现在可以使用 [[!DNL Snowflake Streaming] 源](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) 在Experience PlatformUI中，用于从 [!DNL Snowflake] 数据库。 <br> ![Snowflake流源。](../2024/assets/march/snowflake-streaming.png "新的Snowflake条纹源。"){width="100" zoomable="yes"} <br> 阅读 [[!DNL Snowflake Streaming] 概述](../../sources/connectors/databases/snowflake-streaming.md) 以获取有关如何开始的信息。 |

{style="table-layout:auto"}

欲知关于来源的更多信息，请阅读 [源概述](../../sources/home.md).
