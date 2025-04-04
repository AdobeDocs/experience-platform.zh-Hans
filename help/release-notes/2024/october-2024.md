---
title: Adobe Experience Platform 发行说明（2024 年 10 月）
description: Adobe Experience Platform 的 2024 年 10 月发行说明。
exl-id: 5e2112b8-2a0a-4c1e-af3e-b00d8cc4f4cf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 97%

---

# Adobe Experience Platform 发行说明

**发行日期：2024 年 10 月 29 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [仪表板](#dashboards)
- [数据收集](#data-collection-)
- [目标](#destinations)
- [Segmentation Service](#segmentation-service)
- [沙盒](#sandboxes)
- [源](#sources)

## 仪表板 {#dashboards}

Experience Platform 提供了多个仪表板，您可以通过这些仪表板查看在每日快照中摄取的有关您组织数据的重要洞察。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 数据蒸馏器模板 | 浏览多个模板以获得对受众数据的结构化洞察。使用&#x200B;**高级[!UICONTROL 受众重叠]**、**[!UICONTROL 受众比较]**、**[!UICONTROL 受众趋势]**&#x200B;和&#x200B;**[!UICONTROL 受众身份标识重叠]**&#x200B;等仪表板，做出数据驱动的决策，优化细分并增强参与策略。如需了解更多详细信息，请参阅[数据蒸馏器模板指南](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)。 |
| 高级受众重叠 | 快速分析特定受众交集或查看所有重叠部分，发现整个受众群体的宝贵洞察。利用这些洞察来优化细分、减少冗余消息并创建更有针对性的营销活动，从而提高营销效率。请参阅[高级受众重叠指南](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md)了解更多详情。 |
| 受众比较增强功能 | 使用&#x200B;**受众比较**&#x200B;仪表板查看不同受众群体之间关键量度的并排比较。通过此仪表板，您可以选择特定的时间范围和 KPI（如受众规模和身份标识构成），从而就受众细分和目标市场选择策略做出更明智的决策。请阅读[受众比较指南](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md)，获取更多信息。 |
| 受众趋势可视化图表 | 使用&#x200B;**[!UICONTROL 受众趋势]**&#x200B;仪表板分析随时间变化的受众量度。可视化受众规模、身份标识数量和单一身份标识轮廓数量的趋势，帮助您监测受众演变、衡量增长情况并完善参与策略。请参阅[受众趋势指南](../../dashboards/sql-insights-query-pro-mode/templates/trends.md)，获取更多详细信息。 |
| 身份标识重叠分析 | 使用&#x200B;**[!UICONTROL 受众身份标识重叠]**&#x200B;仪表板分析选定受众的身份标识重叠情况。查看身份标识趋势和细分，了解不同身份标识类型在受众中的关系，加强身份标识拼接，提高客户细分的准确性。请参阅[受众身份标识重叠指南](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md)，获取更多详细信息。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 标记和扩展 | Adobe Analytics JSON 视图 | 现在，您可以使用 Adobe Analytics 标记扩展，以 JSON 查看 eVars、props 和事件设置，这些内容现在可以包含在 Web SDK 扩展中并导出以供编辑。您还可以上传或复制该数据并将其存储在您的设备上。有关详细信息，请阅读 [Adobe Analytics 扩展文档](../../tags/extensions/client/analytics/overview.md)。 |

{style="table-layout:auto"}

有关更多信息，请参阅[数据收藏概述](../../collection/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| [数组导出支持已全面推出](../../destinations/ui/export-arrays-maps-objects.md) | 现在，所有客户在将受众激活到&#x200B;*基于文件的目标*&#x200B;时，都可以使用&#x200B;**[!UICONTROL 添加计算字段]**&#x200B;选项来导出整个数组或数组的元素。请注意，您仍然需要使用 `array_to_string` 函数将数组精简为目标文件中的字符串。<br> ![使用函数和字段添加计算字段选择。](../2024/assets/october/array-export.gif "通过选择 array_to_string 函数和组织数组来添加计算字段。"){width="250" align="center" zoomable="yes"} |
| [增强流式处理目标的报告准确性](/help/destinations/ui/export-datasets.md) | 从 2024 年 10 月开始，Adobe 将推出更新，以提高流式处理目标的报告准确性。这一增强功能可确保 Experience Platform 和目标平台报告之间更好地协调。<br> 在此更新之前， **[!UICONTROL 身份标识信息失败]**&#x200B;包括所有激活重试。此次更新后，总计数中仅包含最后一次激活重试。<br>此增强功能目前适用于 [Google 目标客户匹配功能](../../destinations/catalog/advertising/google-customer-match.md)，但将逐步推广到其他 Experience Platform 流式处理目标。随着增强功能的实施，[Google 目标客户匹配功能](../../destinations/catalog/advertising/google-customer-match.md)用户的&#x200B;**[!UICONTROL 身份标识信息失败]**&#x200B;次数可能会减少。 |
| 灵活的受众评估对[批量受众激活的影响](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | 如果您对已设置为在区段评估后激活的受众运行[灵活受众评估](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)，则无论之前有任何每日激活作业，这些受众都会在灵活受众评估作业完成后立即激活。<br>根据您的操作，这可能会导致每天多次导出受众。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!BADGE 有限发布版 ]{type=Informative} 灵活的受众评估 | 灵活的受众评估让您可以根据时间敏感的通信需求快速创建新的受众。有关此新功能的更多信息，请参阅 [Audience Portal 文档](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的更多信息，请参阅[分段概述](../../segmentation/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足此需求，Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具包共享 | 现在，您可以使用沙盒工具轻松地在不同组织的沙盒之间导出和导入沙盒配置。目前有两类共享包可用：<br><ul><li>**[专用包](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages)：**&#x200B;与已批准源组织共享请求的组织使用专用包共享。</li><li>**[公共包](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages)：**&#x200B;公共包无需额外审批即可共享，并且可以使用包的有效负载轻松导入。</li></ul><br>有关这些功能的更多信息，请阅读[跨组织共享包](../../sandboxes/ui/sharing-packages-across-orgs.md)指南。 |
| 沙盒工具 API 中的[包共享](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking)  | 使用沙盒工具 API 向两个新端点发出请求，`/handshake`并用于`/transfer`跨组织共享、获取和创建包共享请求。已向 `/packages` 端点添加附加请求以检索包的有效负载。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持在 [!DNL Marketo Engage] 中筛选标准活动实体 | 您可以使用 [!DNL Flow Service] API 从 [!DNL Marketo Engage] 源引入数据时筛选标准活动实体。请阅读[筛选 [!DNL Marketo] 标准活动数据](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)指南以了解更多信息。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
