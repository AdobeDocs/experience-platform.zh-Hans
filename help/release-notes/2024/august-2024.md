---
title: Adobe Experience Platform 发行说明（2024 年 8 月）
description: Adobe Experience Platform 的 2024 年 8 月发行说明。
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 95%

---

# Adobe Experience Platform 发行说明

**发行日期：2024 年 8 月 20 日**

>[!TIP]
>
>查看[示例用例文档概述](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/rtcdp/use-cases/overview)，了解您的组织可以使用 Real-Time CDP 实现的各种用例，例如勘探、采集等。

Experience Platform 中现有功能和文档的更新：

- [基于属性的访问控制](#abac)
- [数据引入](#data-ingestion)
- [目标](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [身份标识服务](#identity-service)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 基于属性的访问控制 {#abac}

基于属性的访问控制是 Adobe Experience Platform 的一项功能，它为注重隐私的品牌在管理用户访问权限方面提供了更大的灵活性。可以将架构字段和区段等单个对象分配给用户角色。通过此功能，您可以授予或撤销组织中特定Experience Platform用户访问单个对象的权限。

通过基于属性的访问控制，贵组织的管理员可以控制用户在所有Experience Platform工作流和资源中对敏感个人数据(SPD)、个人身份信息(PII)和其他自定义类型数据的访问。 管理员可以定义只能访问特定字段以及与这些字段对应的数据的用户角色。

**新增功能**

| 功能更新 | 描述 |
| --- | --- |
| 新的权限管理器功能 | 您现在可以利用[权限管理器](../../access-control/abac/permission-manager/overview.md)使用简单的查询生成报告，这可以帮助您了解访问管理的情况，并节省在多个工作流和粒度级别验证访问权限的时间。有关为用户和角色创建报告的更多信息，请参阅[权限管理器使用指南](../../access-control/abac/permission-manager/permissions.md)。![Experience Platform 用户界面图像，其中左侧导航中突出显示权限管理器](assets/august/permission-manager-rn.png "用户界面中的权限管理器。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

有关基于属性的访问控制的详细信息，请参阅[基于属性的访问控制概述](../../access-control/abac/overview.md)。有关基于属性的访问控制工作流的综合指南，请阅读[基于属性的访问控制端到端指南](../../access-control/abac/end-to-end-guide.md)。

## 数据摄取（8 月 23 日更新） {#data-ingestion}

Adobe Experience Platform 提供了一组丰富的功能，以摄取任何类型和任何延迟的数据。您可以使用批处理或流式 API、Adobe 构建的源、数据集成合作伙伴或 Adobe Experience Platform UI 摄取数据。

**更新批量数据摄取中的日期格式处理方式**

此版本解决了批量数据摄取中&#x200B;*日期格式处理*&#x200B;方面的问题。以前，系统会将客户插入的日期字段 `Date` 转换为 `DateTime` 格式。这意味着时区会自动添加到字段中，而这给偏好或需要使用 `Date` 时区格式的用户带来了困难。今后，时区将不会自动添加到 `Date` 类型的字段中。此更新可确保导出的数据格式与客户要求的该字段轮廓上显示的格式相匹配。

发布前的 `Date` 字段：`"birthDate": "2018-01-12T00:00:00Z"`
发布后的 `Date` 字段：`"birthDate": "2018-01-12"`

阅读有关[批量引入](/help/ingestion/batch-ingestion/overview.md)的更多内容。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] 管理其仪表板和 REST 端点的多个不同实例。[!UICONTROL Braze] 客户应该根据所配置的实例使用正确的 REST 端点。此版本添加了一个新的 US-07 端点，您可以在连接到 [!UICONTROL Braze] 时选择该端点。 |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 现在通常可以按需将文件导出到批量目标。 | 现在，所有客户都可以选择按需将文件导出到批量目标。请参阅[专用文档](../../destinations/ui/export-file-now.md)，以了解更多详情。 |
| 在[计划步骤](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中编辑多个导出受众的导出计划。 | 现在，所有客户都可以直接从 Audience Activation 工作流程的计划步骤中编辑多个导出受众的导出计划。![突出显示计划步骤中的编辑计划选项的 Experience Platform 用户界面图像。](assets/august/edit-schedule.png "计划步骤中的编辑计划选项。"){width="250" align="center" zoomable="yes"} |
| 在[计划步骤](../../destinations/ui/activate-batch-profile-destinations.md#scheduling)中编辑多个导出受众的文件名。 | 现在，所有客户都可以直接从 Audience Activation 工作流程的计划步骤中编辑导出受众文件的名称。![突出显示计划步骤中的编辑文件名称选项的 Experience Platform 用户界面图像。](assets/august/edit-file-name.png "计划步骤中的编辑文件名称选项。"){width="250" align="center" zoomable="yes"} |
| 从[目标详细信息](../../destinations/ui/destination-details-page.md#bulk-remove)页面的数据流中删除多个受众。 | 现在，所有客户都可以从&#x200B;**[!UICONTROL 目标详细信息]**&#x200B;页面的现有数据流中删除多个受众。![突出显示目标详细信息页面中的删除受众选项的 Experience Platform 用户界面的图像。](assets/august/bulk-remove-audiences.png "目标详情页面中的移除受众选项。"){width="250" align="center" zoomable="yes"} |
| 从[目标详细信息](../../destinations/ui/destination-details-page.md#bulk-export)页面按需将多个文件导出到批量目标。 | 现在，所有客户都可以从&#x200B;**[!UICONTROL 目标详细信息]**&#x200B;页面按需将多个文件导出到批量目标。![突出显示目标详细信息页面中的立即导出文件选项的 Experience Platform 用户界面的图像。](assets/august/bulk-export-file-now.png "目标详细信息页面中的立即导出文件选项。"){width="250" align="center" zoomable="yes"} |
| 在[目标详细信息](../../destinations/ui/destination-details-page.md#bulk-edit-file-names)页面中编辑多个导出受众的文件名。 | 您现在可以直接在&#x200B;**[!UICONTROL 目标详细信息]**&#x200B;页面中编辑多个导出文件的名称。![突出显示目标详细信息页面中的编辑文件名称选项的 Experience Platform 用户界面的图像。](assets/august/edit-file-name-destination-details.png "目标详细信息页面中的编辑文件名称选项。"){width="250" align="center" zoomable="yes"} |
| 从[目标详细信息](../../destinations/ui/export-datasets.md#remove-dataset)页面的数据流中删除多个数据集。 | 现在所有客户都可以选择从数据流中删除多个数据集。![突出显示目标详细信息页面中的删除数据集选项的 Experience Platform 用户界面的图像。](assets/august/bulk-remove-datasets.png "目标详情页面中的删除数据集选项。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## Experience Data Model (XDM) {#xdm}

XDM 是一种开源规范，可为导入 Adobe Experience Platform 的数据提供通用结构和定义（架构）。通过遵守 XDM 标准，所有客户体验数据都可以合并到一个通用的呈现中，以更快、更加集成的方式提供见解。您可以从客户行为中获得有价值的见解，通过区段定义客户受众，并使用客户属性实现个性化目的。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 由机器学习辅助的架构创建流程 | 使用先进的机器学习算法分析您的样本数据文件，并使用标准和自定义字段自动创建经过优化的架构。<br>主要功能：<br><ul><li>加快架构创建速度：使用由机器学习推荐和生成的 XDM 字段直接从示例数据文件生成架构。</li><li>灵活的架构演变：在生成的架构中轻松添加或更新字段。</li><li>无缝集成：与 Schema UI 中的核心架构创建流程完全集成，确保流畅、一致的用户体验。</li><li>高效的审查和编辑：使用平面视图编辑器快速查看和更新您的架构，使创建过程更加高效易用。</li></ul><br>若要了解更多信息，请阅读[由机器学习辅助的架构创建工作流程指南](../../xdm/ui/ml-assisted-schema-creation.md)。 |

{style="table-layout:auto"}

有关Experience Platform中XDM的更多信息，请参阅[XDM系统概述](../../xdm/home.md)。

## 身份标识服务 {#identity-service}

使用 Adobe Experience Platform 身份标识服务通过跨设备和系统桥接身份标识，全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**文档更新**

| 功能 | 描述 |
| --- | --- |
| 图形配置指南 | 阅读[图形配置指南](../../identity-service/identity-graph-linking-rules/example-configurations.md)，了解在使用身份标识图链接规则和身份标识数据时可能遇到的常见图形场景的信息。图形配置指南提供了从简单的单人图形场景到复杂的分层多人图形场景的示例。您还可以使用本指南查看可在[图形模拟 UI](../../identity-service/identity-graph-linking-rules/graph-simulation.md) 中输入的事件和算法配置示例，以及在某些图形场景下如何选择主要图形的细分信息。 |

{style="table-layout:auto"}

有关身份标识服务的更多信息，请参阅[身份标识服务概述](../../identity-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Experience Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 摄取详细信息 | 对于具有自定义上传来源的受众，您可以在受众详细信息页面中更全面地查看受众引入情况的详细信息。此外，您可以通过选择架构并选择所需的标签属性来将标签应用于有效负载属性。有关引入详情部分的更多信息，请参阅[受众门户指南](../../segmentation/ui/audience-portal.md#ingestion-details)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Adobe Analytics Source Connector 的更新 | 由于 Analytics Source Connector 完全由 Adobe 管理，因此数据集活动页面不会显示有关批次的信息。您可以通过查看与引入的记录相关的量度来监控数据流动的情况。有关更多信息，请阅读关于为 [Analytics 数据](../../sources/tutorials/ui/create/adobe-applications/analytics.md)创建源连接的指南。 |

**文档更新**

| 文档更新 | 描述 |
| --- | --- |
| 扩展了有关更新数据流的文档 | 有关[在 UI 中更新现有源数据流](../../sources/tutorials/ui/update-dataflows.md)的指南已更新，以提供有关您可以对现有数据流进行的各种配置的更多信息。之所以对该指南进行更新还是为了阐明重新启用已禁用的数据流时的预期行为。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
