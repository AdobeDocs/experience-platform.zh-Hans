---
keywords: Experience Platform；查询服务；查询服务；查询
title: Adobe Experience Platform查询服务的示例用例
topic-legacy: tutorial
description: 一个端到端示例，用于演示Adobe Experience Platform查询服务的多功能性和优势。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 6f6256b5601ce5c230ef334a9ce71325b43fda45
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Adobe Experience Platform用例示例 [!DNL Query Service]

本文档及随附的视频演示提供了一个高级端到端工作流程，演示了Adobe Experience Platform [!DNL Query Service] 有利于贵组织的战略业务洞察。 本指南以浏览放弃用例为例，说明了以下关键概念：

* 数据处理对最大化Adobe Experience Platform潜力的关键重要性。
* 基于现有数据架构构建查询的方法。
* 确保满足您需求的数据质量，以及缓解任何不足的方法。
* 计划查询以设置频率运行以在下游用于分段和个性化目标的流程。
* 通过 [!DNL Query Service].

## 目标 {#objectives}

此工作流演示依赖于多项Adobe Experience Platform服务。 如果您想要遵循，建议您对以下功能和服务有很好的了解：

* 的 [体验数据模型(XDM)架构组合的基础知识](../../xdm/schema/composition.md)
* 操作方法 [创建数据集和摄取数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 操作方法 [使用Adobe Analytics源连接器摄取数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=zh-Hans)
* [区段](../../segmentation/home.md)
* [目标](../../destinations/home.md)

浏览放弃示例以使用Adobe为中心 [!DNL Analytics] 创建特定可操作受众的数据。 经过优化，可包含过去四天中浏览了网站但未购买的每位客户。 然后，将受众中的每个配置文件都定位到由客户行为模式产生的最高价格SKU。

查询本身非常规范，只包含符合区段定义用例标准的数据。 这样可以最大限度地减少 [!DNL Analytics] 正在处理的数据。 它还会按从高到低的价格对数据进行订购，并选择用户正在浏览的最高价格SKU。

演示文稿中使用的查询如下所示：

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] 使用adobe analytics浏览放弃示例 {#video-example}

以下视频演示为您重点关注的Experience Platform数据提供了一个全面的真实用例 [!DNL Query Service] 和Adobe分析集成。

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## 优势 [!DNL Query Service] {#benefits}

提供的功能 [!DNL Query Service] 有多种用途。 您可以使用它来适应复杂的分段逻辑、计算用于下游使用的各种个性化属性，或大大简化区段构建的方式。

[!DNL Query Service] 允许您在查询中包含约束，以简化区段构建过程。 这可确保正确的数据符合区段的条件并创建更准确的受众，从而提高数据质量。 维护查询质量可获得准确的受众，并有助于提高数据可靠性。 您还可以通过基于从查询派生的属性创建架构和自定义表来保存受众。 可以为用户档案启用自定义表，并且可以使用这些数据点进行分段和个性化。 此功能可帮助希望创建清晰受众的营销人员。

此外，通过在查询中包含满足任何循环或静态条件的逻辑， [!DNL Query Service] 提取复杂细分的负担。

Adobe Experience Platform提供了一个数据存储库和必要的工具，以便以高效、可靠的方式激活您的数据。 通过将数据保留在Platform中，您可以在运行其他流程时派生属性，而无需将数据导出到第三方工具进行操作和处理。 在处理数百个属性或营销活动时，此类处理间接费用可能会对项目时间表产生重大影响。 这为营销人员提供了一个访问数据和构建营销活动的位置，以及一种非常动态的消息分段和个性化方法。

## 后续步骤

通过阅读本文档，您现在应该了解 [!DNL Query Service] 不仅会影响数据的质量和分段的方便性，而且会影响数据架构对整个端到端工作流程的重要性。 有关将Adobe Analytics与 [!DNL Query Service]，请参阅 [Adobe Analytics示例查询文档](../sample-queries/adobe-analytics.md).

其他文档，这些文档说明了 [!DNL Query Service] 对贵组织的战略业务洞察是 [机器人过滤用例](./bot-filtering.md) 示例。

或者，这些文档将有助于您了解 [!DNL Query Service] 功能：

* [查询执行的指导](../best-practices/writing-queries.md)
* [数据资产组织指南](../best-practices/organize-data-assets.md).


