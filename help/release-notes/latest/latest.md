---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 的 2023 年 7 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d639b0830b88307b249e7da232b3f48b142ad37b
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 58%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 7 月 26 日**

Adobe Experience Platform 中现有功能的更新：

- [目录服务](#catalog-service)
- [数据收集](#data-collection)
- [数据准备](#data-prep)
- [目标](#destinations)
- [查询服务](#query-service)
- [Segmentation Service](#segmentation)
- [源](#sources)
- [Experience Data Model (XDM)](#xdm)

## 目录服务 {#catalog-service}

目录服务是Adobe Experience Platform中数据位置和谱系的记录系统。 虽然摄取到Experience Platform中的所有数据都作为文件和目录存储在数据湖中，但目录包含这些文件和目录的元数据和描述，以供查找和监控。

| 功能 | 描述 |
| --- | --- |
| 数据集库存管理 | 数据集UI现在提供一系列内联操作，以便更好地管理数据集。 高级数据集管理通过创建文件夹和标记并将其分配给允许过滤并提高可发现性的数据集，提高了您的工作效率。 有关以下内容的更多信息，请参阅文档 [内联操作](../../catalog/datasets/user-guide.md#inline-actions)，如何 [搜索和筛选数据集](../../catalog/datasets/user-guide.md#search-and-filter)、和 [将数据集移动到文件夹](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

有关目录服务的详细信息，请参阅 [目录服务概述](../../catalog/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 标记和事件转发 | 数据收集审核日志 | 现在，您可以跨标记和事件转发查看操作的执行时间和执行者。这有助于产品故障排除、适当治理和内部审核活动。此审核数据通过上下文滑出菜单显示，其中还包括快速操作和资源状态更新。可在标记和事件转发 UI 中的以下屏幕上看到这些数据：<br><ul><li>[属性概述](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[规则](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[数据元素](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[扩展](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[库审查](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[库上次构建和发布](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| 数据流 | [Geo 查找](../../datastreams/configure.md#advanced-options) | 您现在可以为数据流配置地理位置和网络查找以包含以下信息： <ul><li>国家/地区</li><li>邮政编码</li><li>州/省</li><li>DMA</li><li>城市</li><li>纬度 </li><li>经度</li><li>运营商</li><li>域</li><li>ISP</li></ul> 您有责任确保已获得适用法律和法规要求的所有必要的权限、同意、许可和授权，以收集、处理和传输个人数据，包括精确的地理位置信息。<br>您的 IP 地址模糊处理选择不会影响将从 IP 地址派生并发送到您配置的 Adobe 解决方案的地理位置信息的级别。必须单独限制或禁用地理位置查找。<br> 请参阅 [数据流文档](../../datastreams/configure.md#advanced-options) 以了解更多详细信息。 |

{style="table-layout:auto"}

有关数据收集的更多信息，请参阅[数据收集概述](../../tags/home.md)。

## 数据准备 {#data-prep}

通过数据准备，数据工程师可从 Experience Data Model (XDM) 映射数据并将数据映射到它、转换和验证数据。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 新的映射器函数 | 现在，您可以在数据准备中映射对象时使用以下函数： <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> 有关这些函数的更多信息，请参阅[数据准备函数指南](../../data-prep/functions.md#hierarchies---objects)。 |

{style="table-layout:auto"}

有关数据准备的详细信息，请阅读[数据准备概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 新增或已更新 | 描述 |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | 新建 | 将来自Adobe Experience Platform的身份载入 [!DNL LiveRamp Connect] 这样您就可以在移动设备、开放网络、社交和 [!DNL CTV] 平台，使用 [!DNL Ramp ID] 标识符。 |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 新建 | 创建到以下对象的实时出站连接： [!DNL Azure Data Lake Storage Gen2] 将数据文件从Adobe Experience Platform定期导出到您自己的存储位置。 此新目标提供了增强的文件导出功能并支持 [!BADGE 测试版]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | 新建 | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform配置的存储界面，允许您访问安全的基于云的文件存储设施，以将文件导出到Platform之外。 此新目标提供了增强的文件导出功能并支持 [!BADGE 测试版]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 新建 | 创建到以下对象的实时出站连接： [!DNL Google Cloud Storage] 定期将数据文件从Adobe Experience Platform导出到您自己的存储桶中。 此新目标提供了增强的文件导出功能并支持 [!BADGE 测试版]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | 已更新 | 通过此更新，目标提供了增强的文件导出功能并支持 [!BADGE 测试版]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | 已更新 | 通过此更新，目标提供了增强的文件导出功能并支持 [!BADGE 测试版]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | 已更新 | 通过此更新，目标提供了增强的文件导出功能并支持 [!BADGE 测试版]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] 连接](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | 已更新 | 此 [!DNL Adobe Campaign Managed Services] 与Adobe Experience Platform集成现在支持不同的audience sync类型。 使用“选择同步类型”控件可确定是否应将受众导出到Adobe Campaign，还是应将受众及其配置文件属性导出到。 <br> ![新的选择同步类型选择器突出显示。](/help/release-notes/2023/assets/acms-destination-export-type.png "新的选择同步类型选择器突出显示。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**新增或更新功能**{#destinations-new-updated-functionality}

上述六个云存储目标的更新和正式可用性版本提供了以下功能：

- 其他 [文件命名选项](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- 能够通过设置导出文件中的自定义文件标头 [改进的映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- 能够自定义 [导出的CSV数据文件的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[支持数据集导出](/help/destinations/ui/export-datasets.md).


**修复和增强功能** {#destinations-fixes-and-enhancements}

- 我们修复了(API) SalesforceMarketing Cloud目标的问题，即在映射步骤中，未从Salesforce返回所有可用目标属性。 现在有一个 [2000个目标属性的上限](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) Salesforce中显示的区段。
- 我们修复了Microsoft Dynamics 365目标的问题。 现在，目标位置支持通过 [区域选择器](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate)因此，您可以根据贵公司在Microsoft生态系统中配置的区域来路由数据导出。 <br> ![新的区域选择器突出显示。](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "新的区域选择器突出显示。"){width="100" zoomable="yes"}

有关目标的更多一般信息，请参阅[目标概览](../../destinations/home.md)。

## 查询服务 {#query-service}

查询服务允许您使用标准 SQL 查询 Adobe Experience Platform 数据湖中的数据。您可以加入数据湖的任何数据集，并作为新数据集获取查询结果，以用于报表、Data Science Workspace，或将数据摄取到实时客户配置文件。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 增强型查询编辑器切换 | 增强的查询编辑器切换提供了更好的可访问性和多主题支持。 增强的编辑器设置允许您启用深色或浅色主题。 有关详细信息，请参阅[文档](../../query-service/ui/user-guide.md#enhanced-editor-toggle)。 |
| 已计算统计信息的别名 | 现在，您可以提供一个别名，在SQL查询的计算统计信息中描述性地引用结果。 有关COMPUTE STATISTICS命令的此项更新和其他更新的信息，请参阅文档。 有关详细信息，请参阅[文档](../../query-service/essential-concepts/dataset-statistics.md#alias-name)。 |

{style="table-layout:auto"}

有关查询服务的详细信息，请参阅[查询服务概述](../../query-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| Audience Portal | Audience Portal 为在 Adobe Experience Platform 中访问、创建和管理受众提供了全新的浏览体验。在 Audience Portal 中，您可以查看 Platform 生成的受众和外部生成的受众；通过筛选、文件夹和标记提高您的工作效率；创建 Platform 生成的受众；并通过 CSV 文件导入外部生成的受众。有关 Audience Portal 的更多信息，请参阅 [Segmentation Service UI 指南](../../segmentation/ui/overview.md)。 |
| 受众组合 | 受众组合提供了一个易于使用的工作区，以通过用于表示不同操作的块来构建和编辑受众。有关受众组合的更多信息，请参阅[受众组合 UI 指南](../../segmentation/ui/audience-composition.md)。 |

有关 [!DNL Segmentation Service] 的更多信息，请参阅[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | 您现在可以使用[[!DNL SAP Commerce] 源](../../sources/connectors/ecommerce/sap-commerce.md)将订阅账单数据从 [!DNL SAP Commerce] 帐户引入 Experience Platform。 |
| 支持 [!DNL Phoenix] | 您现在可以使用[[!DNL Phoenix] 源](../../sources/connectors/databases/phoenix.md)将数据从 [!DNL Phoenix] 数据库引入 Experience Platform。 |
| 对 [!DNL Salesforce] 和 [!DNL Salesforce Service Cloud] 的验证更新 | 在使用 Experience Platform UI 或 [!DNL Flow Service] API 验证新帐户时，您现在可以指定 API 版本的 [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 和 [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) 源。 |

{style="table-layout:auto"}

有关源的更多信息，请参阅[源概述](../../sources/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新的 XDM 组件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM 单个潜在客户配置文件]](https://github.com/adobe/xdm/pull/1758/files) | 使用此类引入来自数据供应商最顶层的客户获取用例的潜在客户配置文件。 |
| 字段组 | [[!UICONTROL 扩充事件区段详细信息]](https://github.com/adobe/xdm/pull/1754/files) | 在事件收集时配置文件符合条件的受众列表。 |

{style="table-layout:auto"}

**更新的 XDM 组件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL MediaAnalytics 交互详情]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 已由实验更新为 `stable`. |
| 字段组 | [[!UICONTROL 媒体交互详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `stable` 到 `deprecated`. |
| 数据类型 | [[!UICONTROL 会话详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL Qoe 数据详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL 播放器状态数据信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental`到 `stable`. |
| 数据类型 | [[!UICONTROL 媒体事件信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL 媒体详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL 错误详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `stable` 到 `deprecated`. |
| 数据类型 | [[!UICONTROL 自定义元数据详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL 章节详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL Advertising Pod详细信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 数据类型 | [[!UICONTROL Advertising 详情信息]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 到 `stable`. |
| 扩展(客户历程管理) | [[!UICONTROL 域]](https://github.com/adobe/xdm/pull/1756/files) | `Domain` 字段已添加至 [!UICONTROL AdobeCJM ExperienceEvent — 消息配置文件详细信息] 记录收件人电子邮件地址的域。 |
| 扩展(客户历程管理) | [[!UICONTROL 渠道的变量名称]](https://github.com/adobe/xdm/pull/1753/files) | 此字段已添加到 [!UICONTROL AJO实体字段] 表示渠道变体名称。 |
| 扩展(Adobe Analytics) | [[!UICONTROL 上下文值]](https://github.com/adobe/xdm/pull/1761/files) | `Context value` 已添加至 [!UICONTROL `Adobe Analytics ExperienceEvent Full Extension`]. |

{style="table-layout:auto"}

有关 Platform 中 XDM 的详细信息，请查看 [XDM 系统概述](../../xdm/home.md)。

