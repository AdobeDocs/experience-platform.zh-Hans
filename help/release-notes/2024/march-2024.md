---
title: Adobe Experience Platform 发行说明（2024 年 3 月）
description: Adobe Experience Platform 的 2024 年 3 月发行说明。
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 97%

---

# Adobe Experience Platform 发行说明

**发布日期：2024 年 3 月19 日**

>[!TIP]
>
>使用 [Adobe Experience Platform 词汇表](/help/landing/glossary.md)，熟悉 Real-time Customer Data Platform 和 Adobe Experience Platform 中使用的术语。如果您找不到所需的特定术语，请使用页面上的反馈选项请求将新术语添加到词汇表中。

Experience Platform 中现有功能的更新：

- [目录服务](#catalog-service)
- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 目录服务 {#catalog-service}

目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录保存这些文件和目录的元数据和描述以供查找和监控目的。

| 功能 | 描述 |
| --- | --- |
| 更多操作 | 为了使操作更加灵活并帮助您管理数据，您现在可以使用详细信息视图中的“更多操作”功能对数据集执行其他任务。您可以从所选数据集的详细信息页面删除数据集，也可以启用它以与实时客户配置文件一起使用。<br>**注意：** 如果启用数据集以进行轮廓提取，则数据集的架构必须与实时客户轮廓兼容。<br>![数据集工作区，其中 [!UICONTROL ...更多] 下拉菜单突出显示。](../2024/assets/march/more-actions.png "数据集工作区，其中突出显示了更多下拉菜单。"){width="100" zoomable="yes"}。<br>参阅[数据集用户指南](../../catalog/datasets/user-guide.md)文档以获取更多信息。 |

{style="table-layout:auto"}

有关目录服务的详细信息，请参阅[目录服务概述](../../catalog/home.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics 的新映射器功能 | 您现在可以使用以下函数从 Adobe Analytics 中提取事件数据： <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> 有关这些函数的更多信息，请参阅[数据准备函数指南](../../data-prep/functions.md#analytics-functions)。 |

{style="table-layout:auto"}

有关数据准备的详细信息，请参阅[数据准备概述](../../data-prep/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 扩展 | [!DNL Merkury] 标记扩展 | [[!DNL Merkury]  标记扩展](https://exchange.adobe.com/apps/ec/600027/merkury-tag)为 [!DNL Merkury] ID 的匿名网站访问者提供了业界领先的匹配率。品牌可以利用 [!DNL Merkury] 标签和 Adobe 的强大功能来提供实时个性化的网站体验。此外，[!DNL Merkury] 标签还可以促进第一方数字数据以及线上和线下客户资料的增长。 |

{style="table-layout:auto"}

要详细了解数据收集，请阅读[数据收集概述](../../tags/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增和更新的目标**{#new-updated-destinations}

| 目标 | 类型 | 描述 |
| ----------- | --------- | ----------- |
| [（Beta）Acxiom Data Enhancement 连接](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | 新增 | 使用此连接器将第一方配置文件从 Real-Time CDP 激活到 Acxiom，以丰富数据并跨营销渠道使用。然后，您可以使用 Acxiom 源导入具有增强数据的配置文件，并在 Real-Time CDP 中使用它们。 |
| [（Beta）Acxiom Prospect Suppression 连接](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | 新增 | 将您的第一方受众导出到 Acxiom 目标，以允许 Acxiom 抑制已知或转换的客户。然后，使用 [Acxiom 潜在客户数据导入](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md)源连接器从 Acxiom 提取并激活潜在客户列表，并删除已知或已转换的客户。 |
| [Amazon Ads 连接](../../destinations/catalog/advertising/amazon-ads.md) | 更新 | 将数据导出到 Amazon Ads 目标时，您现在可以将数据路由到 Amazon DSP 或 Amazon Marketing Cloud（新）。 |
| [LiveRamp Onboarding 连接](../../destinations/catalog/advertising/liveramp-onboarding.md) | 更新 | LiveRamp Onboarding 目标现在支持向欧洲和澳大利亚 [!DNL LiveRamp] [!DNL SFTP] 实例进行传递。最大导出文件大小也增加到 1,000 万行（之前为 500 万行）。 |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

有关目标的更多一般信息，请参阅[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| Experience Platform UI 映射数据类型支持 | 通过在Experience Platform UI中定义映射字段，进一步自定义您的Experience Data Model (XDM)数据结构。 您现在可以在 Schema Editor 中创建映射字段来建模灵活的数据结构或有效地存储键值对。定义新字段时，从类型下拉菜单中选择“映射”来配置子字段并将其分配给字段组。支持的映射值类型是字符串和整数。<br>![Schemas Editor 中类型和映射值类型字段突出显示。](../2024/assets/march/maps.png "Schemas Editor 中类型和映射值类型字段突出显示。"){width="100" zoomable="yes"}<br> 了解如何[在 UI 中定义映射字段](../../xdm/ui/fields/map.md)，请参阅 UI 指南。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Experience Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 批量操作 | 受众库存现在支持批量操作。使用批量操作，您可以快速选择多个受众将其移动到文件夹、应用标签、应用访问标签或删除。<br> ![受众 UI 工作区中的批量操作。](../2024/assets/march/bulk-actions.png "受众 UI 工作区中的批量操作。"){width="100" zoomable="yes"} <br>有关此功能的更多信息，请阅读[受众门户概述](../../segmentation/ui/audience-portal.md#bulk-actions)。 |

{style="table-layout:auto"}

要了解有关区段服务的更多信息，请阅读[区段服务概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新的和更新的来源**

| 功能 | 类型 | 描述 |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | 新增 | 使用 [[!DNL Acxiom Data Ingestion] 来源](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) 摄取 [!DNL Acxiom] 数据纳入 Real-time Customer Data Platform 并丰富第一方资料。然后，您可以使用您的 [!DNL Acxiom]- 丰富第一方资料，以扩大受众群体并激活整个营销渠道。 <br> ![Acxiom 数据提取源。](../2024/assets/march/acxiom-data-ingestion.png "新的Acxiom 数据提取源。"){width="100" zoomable="yes"} <br>参阅 [[!DNL Acxiom Data Ingestion] 概述](../../sources/connectors/data-partners/acxiom-data-ingestion.md)，了解如何开始的信息。 |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | 新增 | 使用 [[!DNL Stripe] 来源](../../sources/connectors/payments/stripe.md)将客户在购买流程中捕获的数据导入 Experience Platform。一旦获取，您就可以使用这些数据来创建个性化服务并解锁更丰富的商业洞察力。 <br> ![Stripe 来源。](../2024/assets/march/stripe.png "新的 Stripe 源。"){width="100" zoomable="yes"} <br>参阅 [[!DNL Stripe] 概述](../../sources/connectors/payments/stripe.md)，了解如何开始的信息。 |
| UI 支持 [!DNL Snowflake Streaming] | 新增 | 您现在可以使用 Experience Platform UI 中的 [[!DNL Snowflake Streaming]  源](../../sources/tutorials/ui/create/databases/snowflake-streaming.md)从 [!DNL Snowflake] 数据库<br>流式传输数据。 ![Snowflake Streaming 源。](../2024/assets/march/snowflake-streaming.png "新的雪花条纹源。"){width="100" zoomable="yes"} <br>参阅 [[!DNL Snowflake Streaming] 概述](../../sources/connectors/databases/snowflake-streaming.md)，了解如何开始的信息。 |

{style="table-layout:auto"}

请参阅[源概述](../../sources/home.md)，了解有关源的更多信息。
