---
title: Adobe Experience Platform发行说明2024年10月
description: Adobe Experience Platform 的 2024 年 10 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 35%

---

# Adobe Experience Platform 发行说明

**发行日期： 2024年10月29日**

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
| 数据Distiller模板 | 探索多个模板以获得对受众数据的结构化见解。 使用诸如&#x200B;**高级[!UICONTROL 受众重叠]**、**[!UICONTROL 受众比较]**、**[!UICONTROL 受众趋势]**&#x200B;和&#x200B;**[!UICONTROL 受众身份重叠]**&#x200B;等功能板制定数据驱动型决策、优化分段并增强参与策略。 有关更多详细信息，请参阅[Data Distiller模板指南](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)。 |
| 高级受众重叠 | 快速分析特定受众的受众交叉点或查看所有重叠，以揭示整个受众集中的宝贵见解。 利用这些见解优化细分、减少冗余消息传送，并创建更有针对性的促销活动以提高营销效率。 有关详细信息，请参阅[高级受众重叠指南](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md)。 |
| 受众比较增强功能 | 使用&#x200B;**受众比较**&#x200B;仪表板查看不同受众组之间关键量度的并排比较。 利用此功能板，您可以选择特定时间范围和KPI（如受众规模和身份构成），以针对受众分段和定位策略做出更明智的决策。 有关详细信息，请阅读[受众比较指南](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md)。 |
| 受众趋势可视化 | 使用&#x200B;**[!UICONTROL 受众趋势]**&#x200B;仪表板分析一段时间内的受众量度。 可视化受众规模、身份数和单一身份配置文件数的趋势，以帮助您监控受众演变、衡量增长并优化参与策略。 有关详细信息，请参阅[受众趋势指南](../../dashboards/sql-insights-query-pro-mode/templates/trends.md)。 |
| 身份重叠分析 | 使用&#x200B;**[!UICONTROL 受众身份重叠]**&#x200B;仪表板分析选定受众中的身份重叠。 查看身份趋势和细分，以了解受众中不同身份类型的关系，从而增强身份拼接并提高客户分段准确性。 有关更多详细信息，请参阅[受众标识重叠指南](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md)。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义构件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 标记和扩展 | Adobe Analytics JSON视图 | 您现在可以使用Adobe Analytics标记扩展来检查JSON格式的eVar、prop和事件设置，JSON现在可以包含在Web SDK扩展中并导出以进行编辑。 您还可以上传或复制此数据，并将其存储在您的设备上。 有关详细信息，请阅读[Adobe Analytics扩展文档](../../tags/extensions/client/analytics/overview.md)。 |

{style="table-layout:auto"}

有关更多信息，请参阅[数据收藏概述](../../collection/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| [阵列导出支持一般可用](../../destinations/ui/export-arrays-calculated-fields.md) | 在将受众&#x200B;*激活到基于文件的目标*&#x200B;时，所有客户现在都可以使用&#x200B;**[!UICONTROL 添加计算字段]**&#x200B;选项来导出整个数组或数组的元素。 请注意，您仍需要使用`array_to_string`函数将数组拼合到目标文件中的字符串中。<br> ![添加包含函数和字段的计算字段选择。](../2024/assets/october/array-export.gif "添加计算字段，选择了array_to_string函数和组织数组。"){width="250" align="center" zoomable="yes"} |
| [流目标的报表准确性增强](/help/destinations/ui/export-datasets.md) | 从2024年10月开始，Adobe将推出一项更新，以提高流目标的报表准确性。 此增强功能可确保Experience Platform和目标平台报表之间更好地保持一致。 <br>在此更新之前，**[!UICONTROL 标识失败]**&#x200B;包括所有激活重试。 进行此更新后，总计数中仅包含上次激活重试。 <br>此增强功能当前适用于[Google客户匹配目标](../../destinations/catalog/advertising/google-customer-match.md)，但将逐步推广到其他Experience Platform流目标。 进行此增强后，[Google客户匹配目标](../../destinations/catalog/advertising/google-customer-match.md)的用户可能会看到其&#x200B;**[!UICONTROL 身份失败]**&#x200B;计数中预期的下降。 |
| 灵活的受众评估对[批量受众激活](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)的影响 | 如果您对已设置为在区段评估后激活的受众运行[灵活受众评估](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)，则无论之前执行过任何每日激活作业，灵活受众评估作业完成后都将立即激活受众。 <br>这可能会导致根据您的操作，每天多次导出受众。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的配置文件子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| [!BADGE 有限可用性]{type=Informative}灵活的受众评估 | 灵活的受众评估允许您根据对时间敏感型通信的需求，快速创建新受众。 有关此新功能的详细信息，请参阅[受众门户文档](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)。 |

{style="table-layout:auto"}

有关 [!DNL Segmentation Service] 的更多信息，请参阅[分段概述](../../segmentation/home.md)。

## 沙盒 {#sandboxes}

Adobe Experience Platform 旨在丰富全球范围内的数字体验应用。企业通常会同时运行多个数字体验应用程序，并且需要满足这些应用程序的开发、测试和部署要求，同时确保运营合规性。为了满足这一需求，Experience Platform 提供了可将单个 Platform 实例划分为多个单独的虚拟环境的沙盒，以帮助开发和改进数字体验应用程序。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 沙盒工具包共享 | 您现在可以使用沙盒工具轻松地在不同组织的沙盒之间导出和导入沙盒配置。 现在有两种可用的共享包：<br><ul><li>**[私有包](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages)：**&#x200B;与已批准来自源组织的共享请求的组织使用私有包共享。</li><li>**[公共包](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages)：**&#x200B;无需额外批准即可共享公共包，并可使用该包的有效负荷轻松导入公共包。</li></ul><br>有关这些功能的详细信息，请阅读有关[跨组织共享包](../../sandboxes/ui/sharing-packages-across-orgs.md)的指南。 |
| 沙盒工具API中的[包共享](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) | 使用沙盒工具API向两个新端点`/handshake`和`/transfer`发出请求，以便在组织间共享、获取和创建包共享请求。 已向`/packages`端点添加了其他请求以检索包的有效负载。 |

{style="table-layout:auto"}

有关沙盒的更多信息，请阅读[沙盒概述](../../sandboxes/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持筛选[!DNL Marketo Engage]中的标准活动实体 | 从[!DNL Marketo Engage]源摄取数据时，可以使用[!DNL Flow Service] API筛选标准活动实体。 有关详细信息，请阅读有关[筛选 [!DNL Marketo] 标准活动数据](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)的指南。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。