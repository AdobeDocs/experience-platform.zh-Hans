---
title: Adobe Experience Platform 发行说明（2025 年 3 月）
description: Adobe Experience Platform 的 2025 年 3 月发行说明。
exl-id: 3da1c912-2581-4afa-bd21-0b8303531dcd
source-git-commit: 16056a35624b4a053e9f50acef0ec3f63254a065
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 25%

---

# Adobe Experience Platform 发行说明

**发行日期： 2025年3月26日**

Adobe Experience Platform 中现有功能和文档的更新：

- [Adobe Experience Platform 发行说明](#adobe-experience-platform-release-notes)
   - [仪表板](#dashboards)
   - [目标](#destinations)
   - [Segmentation Service](#segmentation-service)
   - [源](#sources)

## 仪表板 {#dashboards}

Experience Platform 提供了多个仪表板，您可以通过这些仪表板查看在每日快照中摄取的有关您组织数据的重要洞察。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于量度的许可证使用情况仪表板 | 许可证使用情况仪表板现在包含一个简化的UI，带有两个选项卡：**量度**&#x200B;和&#x200B;**产品**。 新的&#x200B;**量度**&#x200B;选项卡提供了跨您购买的产品的所有可跟踪许可证量度的综合视图。 每个量度都包含一个内联信息图标，用于显示描述和相关产品。 用户可以选择“生产”或“开发”沙盒，在交互式图表中查看历史使用趋势，并将特定于沙盒的数据导出为CSV文件。 这些更新可简化许可证跟踪并提供更清晰的洞察。 有关详细信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md)。 |
| 已更新的预测频率 | 许可证使用情况仪表板现在通过更新使用预测&#x200B;**每周**，而不是每月更新，提供了有关预计使用情况的更准确见解。 这些预测显示了基于最近趋势的未来6周内的估计使用量。 此更改允许更快的决策、更早的干预和改进的许可证计划。 有关详细信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md#predicted-usage)。 |
| 更新了UI中的量度描述 | 许可证使用情况仪表板中的量度定义已得到修订，以提高清晰度和一致性。 您现在可以使用&#x200B;**指标**&#x200B;选项卡中每个指标旁边的内联信息图标，直接在仪表板中查看更新的描述。 这些更新更容易了解如何跟踪量度以及量度应用于哪些产品。 有关更多详细信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md#available-metrics)。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Demandbase People connection](/help/destinations/catalog/advertising/demandbase-people.md) | Use the [!DNL Demandbase People] connection to activate profiles for your Demandbase campaigns for audience targeting, personalization, and suppression. |
| [Bombora account connection](/help/destinations/catalog/advertising/bombora.md) | Use the  [!DNL Bombora] connection to activate profiles for your Bombora campaigns for audience targeting, personalization, and suppression, based on [account audiences](/help/segmentation/types/account-audiences.md). |
| [飞艇属性](/help/destinations/catalog/mobile-engagement/airship-attributes.md)升级 | 从2025年3月25日开始，您可以在目标目录中并排看到两个&#x200B;**[!UICONTROL 飞艇属性]**&#x200B;卡片。 这是由于目标服务的内部升级。 现有的&#x200B;**[!UICONTROL 飞艇属性]**&#x200B;目标连接器已重命名为&#x200B;**[!UICONTROL （已弃用）飞艇属性]**，现在您可以使用名为&#x200B;**[!UICONTROL 飞艇属性]**&#x200B;的新信息卡。 <br>使用目录中的&#x200B;**[!UICONTROL 飞艇属性]**&#x200B;连接获取新的激活数据流。 如果您有任何到[!DNL (Deprecated) Airship Attributes]目标的活动数据流，它们会自动更新，因此您无需执行任何操作。 <br>如果您通过[流服务API](https://developer.adobe.com/experience-platform-apis/references/destinations/)创建数据流，则必须将[!DNL flow spec ID]和[!DNL connection spec ID]更新为以下值： <ul><li> 流程规范ID： `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> 连接规范ID： `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [增强流式处理目标的报告准确性](../../dataflows/ui/monitor-destinations.md) | 从2025年3月开始，Adobe将推出一项更新，以提高流目标的报表准确性。 此增强功能可确保Experience Platform中的报表与目标平台之间更好地保持一致。 <br> 在此更新之前， **[!UICONTROL 身份标识信息失败]**&#x200B;包括所有激活重试。此次更新后，总计数中仅包含最后一次激活重试。<br>此增强功能适用于所有流目标。 <br>在此增强功能之后，流式目标用户在其&#x200B;**[!UICONTROL 身份失败]**&#x200B;计数中可能会看到预期的下降。 |
| [针对企业和边缘目标的映射类型字段导出支持](/help/destinations/ui/export-arrays-maps-objects.md) | 将数据导出到[Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)、[HTTP API](/help/destinations/catalog/streaming/http-destination.md)、[Azure事件中心](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)和[Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)目标时，您现在可以在激活工作流的映射步骤中选择要导出的映射类型字段。<br> ![将映射类型字段导出到企业目标。](../2025/assets/march/export-map.png "将映射类型字段导出到企业目标。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

| 功能 | 描述 |
| ------- | ----------- |
| 帐户受众生成器增强功能 | 在Audience Builder中，您现在可以筛选属性以仅显示填充的属性，并查看这些填充属性的摘要数据。 有关这些增强功能的详细信息，请参阅[受众生成器](../../rtcdp/segmentation/audience-builder.md)文档。 |
| 灵活的受众评估正式发布 | 灵活的受众评估功能现已正式推出！ 您可以使用灵活的受众评估在需要时为时效性通信创建新受众。 有关灵活受众评估的详细信息，请参阅[灵活受众评估概述](../../segmentation/methods/flexible-audience-evaluation.md)。 |

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**新来源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Bombora Intent] | [!DNL Bombora Intent]源现在在源目录中可用。 使用此源可以： <ul><li>集成Bombrora公司的Surge Intent数据，以识别积极研究您的产品或服务的客户。</li><li>优先考虑市场内客户，以创建精确的区段并执行超针对性的ABM营销活动，确保您的营销工作将重点放在最有可能转化的客户上。</li><li>利用意图驱动型策略优化广告支出、提高参与度并最大限度地提高ROI。</li></ul> 有关详细信息，请阅读有关[将您的 [!DNL Bombora] 帐户连接到Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md)的指南。 |
| [!DNL Demandbase Intent] | [!DNL Demandbase Intent]¸源现在可在源目录中找到。 使用此源可以： <ul><li>集成Demandbase的帐户意图数据，以根据实时参与情况识别高兴趣帐户。</li><li>通过优先处理最强的意图信号，您可以创建精确的区段并提供超定位促销活动，以确保您的营销工作将重点放在最有可能转化的帐户上。</li><li>激活意图驱动型策略以实现广告支出优化、参与度提高和ROI提高。</li></ul> 有关详细信息，请阅读有关[将您的 [!DNL Demandbase] 帐户连接到Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md)的指南。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 对[!DNL Google Ads]源的增强 | 您现在可以使用[[!DNL Google Ads] 源](../../sources/connectors/advertising/ads.md)来摄取聚合数据。 您可以使用[!DNL Google Ads Query Builder]指定要摄取到Experience Platform的属性、区段和资源。 有关详细信息，请阅读有关[将您的 [!DNL Google Ads] 帐户连接到Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md)的指南。 |
| 对[!DNL Microsoft Dynamics]源的增强 | 在浏览数据的内容和结构时，您现在可以指定给定[!DNL Microsoft Dynamics]表的主键。 使用此功能优化[!DNL Microsoft Dynamics]源的查询。 有关详细信息，请参阅[使用API将 [!DNL Microsoft Dynamics] 源连接到Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md)指南。 |
| 在自助源(批处理SDK)中支持API密钥身份验证 | 现在，在将新源与自助源(批处理SDK)集成时，您可以使用API密钥身份验证作为身份验证类型。 有关详细信息，请阅读[在批处理SDK](../../sources/sources-sdk/config/authspec.md)中配置您的身份验证规范的指南。 |
| 在源中支持基于属性的访问控制 | 您现在可以对源数据流使用基于属性的访问控制函数。 有关详细信息，请阅读以下指南： <ul><li>[使用API将标签应用于源数据流](../../sources/tutorials/api/labels.md)</li><li>[使用UI将标签应用于源数据流](../../sources/tutorials/ui/labels.md)。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
