---
title: Adobe Experience Platform 发行说明（2025 年 3 月）
description: Adobe Experience Platform 的 2025 年 3 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f0879683629ba10ed1b799e52f0adf332f079daf
workflow-type: ht
source-wordcount: '1250'
ht-degree: 100%

---

# Adobe Experience Platform 发行说明

**发布日期：2025 年 3 月 26 日**

Adobe Experience Platform 中现有功能和文档的更新：

- [Adobe Experience Platform 发行说明](#adobe-experience-platform-release-notes)

   - [仪表板](#dashboards)
   - [目标](#destinations)
   - [联合受众构成](#federated-audience-composition)
   - [Segmentation Service](#segmentation-service)
   - [源](#sources)

## 仪表板 {#dashboards}

Experience Platform 提供了多个仪表板，您可以通过这些仪表板查看在每日快照中摄取的有关您组织数据的重要洞察。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 基于量度的许可证使用情况仪表板 | 许可证使用情况仪表板现在包含一个简化的 UI，其中有两个选项卡：**量度**&#x200B;和&#x200B;**产品**。新的&#x200B;**量度**&#x200B;选项卡提供了您所购买产品中所有可跟踪许可证量度的综合视图。每个量度都包含一个内联信息图标，显示描述和相关产品。用户可以选择生产或开发沙盒，在交互式图表中查看历史使用趋势，并将沙盒特定数据导出为 CSV 文件。这些更新简化了许可证跟踪，并提供了更清晰的洞察。有关更多详细信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md)。 |
| 更新预测频率 | 许可证使用情况仪表板现在可以&#x200B;**每周**&#x200B;更新使用情况预测（而不是每月更新一次），从而提供更准确地预计使用情况洞察。这些预测根据最近的趋势显示了未来六周的预计使用情况。这一更改有助于加快决策速度、更早干预并改善许可证规划。有关更多详细信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md#predicted-usage)。 |
| 已更新 UI 中的量度描述 | 许可证使用情况仪表板中的量度定义已被修订，提高了清晰度和一致性。您现在可以使用&#x200B;**量度**&#x200B;选项卡中每个量度旁边的内联信息图标，直接在仪表板中查看更新说明。这些更新使您更容易了解如何跟踪量度，以及它们适用于哪些产品。有关更多详细信息，请参阅[许可证使用情况仪表板指南](../../dashboards/guides/license-usage.md#available-metrics)。 |

{style="table-layout:auto"}

有关仪表板的详细信息，包括如何授予访问权限和创建自定义小组件，请首先阅读[仪表板概述](../../dashboards/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新增或更新目标**{#new-updated-destinations}

| 目标 | 描述 |
| --- | --- |
| [Demandbase People 连接](/help/destinations/catalog/advertising/demandbase-people.md) | 使用 [!DNL Demandbase People] 连接激活您的 Demandbase 营销活动轮廓，以实现受众目标市场选择、个性化和禁止。 |
| [Bombora 帐户连接](/help/destinations/catalog/advertising/bombora.md) | 使用 [!DNL Bombora] 连接激活您的 Bombora 营销活动轮廓，以根据[帐户受众](/help/segmentation/types/account-audiences.md)实现受众目标市场选择、个性化和禁止。 |
| [Airship Attributes](/help/destinations/catalog/mobile-engagement/airship-attributes.md) 升级 | 从 2025 年 3 月 25 日开始，您可以在目标目录中并排看到两张 **[!UICONTROL Airship Attributes]** 卡。这是由于目标服务内部升级造成的。现有的 **[!UICONTROL Airship Attributes]** 目标连接器已更名为&#x200B;**[!UICONTROL （已废弃）Airship Attributes]**，您现在可以使用名为 **[!UICONTROL Airship Attributes]** 的新卡片。<br>将目录中的 **[!UICONTROL Airship Attributes]** 连接用于新的激活数据流。如果您有任何连接到 [!DNL (Deprecated) Airship Attributes] 目标的激活数据流，它们将自动更新，因此无需您执行任何操作。<br>如果您通过 [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 创建数据流，则必须将 [!DNL flow spec ID] 和 [!DNL connection spec ID] 更新为以下值： <ul><li> 流量规范 ID：`a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> 连接规范 ID：`594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**新增或更新的功能**{#destinations-new-updated-functionality}

| 功能 | 描述 |
| --- | --- |
| [增强流式处理目标的报告准确性](../../dataflows/ui/monitor-destinations.md) | 从 2025 年 3 月开始，Adobe 将推出一项更新，以提高流式处理目标的报告准确性。这一增强功能可确保 Experience Platform 和目标平台之间更好地协调。<br> 在此更新之前， **[!UICONTROL 身份标识信息失败]**&#x200B;包括所有激活重试。此次更新后，总计数中仅包含最后一次激活重试。<br> 这一增强功能适用于所有流式处理目标。<br>随着这一增强功能的实施，流式处理目标用户的&#x200B;**[!UICONTROL 身份标识信息失败]**&#x200B;次数可能会减少。 |
| [支持企业和边缘目标的 Map-type 字段导出](/help/destinations/ui/export-arrays-maps-objects.md) | 将数据导出到 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)、[HTTP API](/help/destinations/catalog/streaming/http-destination.md)、[Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) 和 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目标时，现在可以在激活工作流的映射步骤中选择导出的 map-type 映射字段。<br> ![将 map-type 字段导出到企业目标。](../2025/assets/march/export-map.png "将 map-type 字段导出到企业目标。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 联合受众构成 {#federated-audience-composition}

有关联合受众构成的最新信息，请阅读此处的[专用发行说明](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/release-notes)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

| 功能 | 描述 |
| ------- | ----------- |
| 帐户受众生成器增强功能 | 在受众生成器中，您现在可以过滤属性，仅显示已填充属性，并查看这些已填充属性的摘要数据。有关这些增强功能的更多信息，请参阅[受众生成器](../../rtcdp/segmentation/audience-builder.md)文档。 |
| 灵活受众评估正式发布 | 灵活受众评估现已正式发布！您可以使用灵活受众评估，按需创建新的受众，以进行时间敏感的通信。有关灵活受众评估的更多信息，请参阅[灵活受众评估概述](../../segmentation/methods/flexible-audience-evaluation.md)。 |

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

使用 Experience Platform 中的源从 Adobe 应用程序或第三方数据源引入数据。

**新来源**

| 功能 | 描述 |
| --- | --- |
| [!DNL Bombora Intent] | [!DNL Bombora Intent] 源现已在源目录中可用。使用此源可以： <ul><li>集成 Bombora 的公司激增意图数据，识别正在积极研究您的产品或服务的帐户。</li><li>优先考虑市场中的帐户，创建精确的区段，并执行超目标 ABM 营销活动，确保您的营销工作集中在最有可能实现转化的帐户上。</li><li>利用意图驱动策略来优化广告支出、提高参与度并最大限度地提高投资回报率。</li></ul> 有关更多信息，请阅读将您的帐户[连接 [!DNL Bombora] 到 Experience Platform](../../sources/tutorials/ui/create/data-partners/bombora.md) 指南。 |
| [!DNL Demandbase Intent] | [!DNL Demandbase Intent] 源现已在源目录中可用。使用此源可以： <ul><li>集成 Demandbase 的帐户意图数据，根据实时参与度识别高兴趣帐户。</li><li>通过优先考虑最强的意图信号，您可以创建精确的区段，并开展超目标营销活动，确保您的营销工作集中在最有可能实现转化的帐户上。</li><li>激活意图驱动策略可优化广告支出、提高参与度并提高投资回报率。</li></ul> 有关更多信息，请阅读将您的帐户[连接 [!DNL Demandbase] 到 Experience Platform](../../sources/tutorials/ui/create/data-partners/demandbase.md) 指南。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| [!DNL Google Ads] 源的增强功能 | 您现在可以使用 [[!DNL Google Ads] 源](../../sources/connectors/advertising/ads.md) 来摄取汇总数据。您可以使用 [!DNL Google Ads Query Builder]，指定要摄取到 Experience Platform 的属性、区段和资源。有关更多信息，请阅读将您的帐户[连接 [!DNL Google Ads] 到 Experience Platform](../../sources/tutorials/ui/create/advertising/ads.md) 指南。 |
| [!DNL Microsoft Dynamics] 源的增强功能 | 您现在可以在探索数据的内容和结构时指定给定 [!DNL Microsoft Dynamics] 表的主键。使用此功能可通过 [!DNL Microsoft Dynamics] 源优化您的查询。有关更多信息，请阅读使用 API 将您的源[连接 [!DNL Microsoft Dynamics] 到 Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md) 指南。 |
| 支持自助服务源（Batch SDK）中的 API 密钥身份验证 | 现在，当将新源与自助服务源（Batch SDK）集成时，您可以使用 API 密钥身份验证作为身份验证类型。有关更多信息，请阅读[在 Batch SDK 中配置您的身份验证规范](../../sources/sources-sdk/config/authspec.md)指南。 |
| 支持源中基于属性的访问控制 | 您现在可以对源数据流使用基于属性的访问控制功能。阅读以下指南以了解更多信息： <ul><li>[使用 API 将标签应用于源数据流](../../sources/tutorials/api/labels.md)</li><li>[使用 UI 将标签应用于源数据流](../../sources/tutorials/ui/labels.md)。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
