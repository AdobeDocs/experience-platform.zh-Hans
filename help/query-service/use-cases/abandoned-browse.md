---
keywords: Experience Platform；查询服务；查询服务
title: Adobe Experience Platform查询服务的示例用例
description: 一个端到端示例，用于演示Adobe Experience Platform查询服务的通用性和优势。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---

# Adobe Experience Platform的示例用例 [!DNL Query Service]

此文档和随附的视频演示文稿提供了一个高级别的端到端工作流程，用于演示Adobe Experience Platform的工作原理 [!DNL Query Service] 使贵组织的战略性业务洞察力大有裨益。 本指南以浏览放弃用例为例，说明了以下关键概念：

* 数据处理对于最大限度地发挥Adobe Experience Platform的潜力至关重要。
* 基于现有数据架构构建查询的方法。
* 确保满足您需求的数据质量，以及减少任何不足的方法。
* 安排查询以设定的频率运行的进程，以便在区段和个性化的目标中使用下游。
* 营销人员可以轻松地将派生属性包含在其区段中，方法是使用 [!DNL Query Service].

## 目标 {#objectives}

此工作流演示依赖于多个Adobe Experience Platform服务。 如果您希望跟进，建议您很好地了解以下功能和服务：

* 此 [体验数据模型(XDM)架构组合基础](../../xdm/schema/composition.md)
* 操作方法 [创建数据集并摄取数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* 操作方法 [使用Adobe Analytics源连接器引入数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html)
* [区段](../../segmentation/home.md)
* [目标](../../destinations/home.md)

浏览放弃示例以使用Adobe为中心 [!DNL Analytics] 数据，用于创建特定可操作的受众。 优化受众，使其包含过去四天浏览网站但未购买的每位客户。 然后，受众中的每个用户档案都将定位为因客户行为模式而产生的最高价格SKU。

查询本身具有非常强的说明性，并且只包含符合区段定义用例标准的数据。 这可以通过最大限度地减少 [!DNL Analytics] 正在处理数据。 它还按从高到低的价格对数据排序，并选择用户浏览的定价最高的SKU。

在演示文稿中使用的查询如下所示：

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

下面看到的视频演示为您的重点介绍的Experience Platform数据提供了一个全面、真实的用例 [!DNL Query Service] 和Adobe分析集成。

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## 的好处 [!DNL Query Service] {#benefits}

提供的功能 [!DNL Query Service] 有许多用途。 您可以使用它来适应复杂的分段逻辑、计算各种个性化属性以供下游使用，或者大大简化构建区段的方式。

[!DNL Query Service] 允许在查询中包含限制以简化区段构建过程。 这通过确保正确的数据符合区段资格并创建更准确的受众而提高了数据质量。 保持查询质量可生成准确的受众，并有助于提高数据的可靠性。 您还可以通过基于从查询派生的属性创建架构和自定义表来保存受众。 可以为配置文件启用自定义表，并且您可以使用这些数据点进行分段和个性化。 此功能可帮助希望创建明确受众人群的营销人员。

此外，通过在查询中包含满足任何循环或静态条件的逻辑， [!DNL Query Service] 提取精细分段的负担。

Adobe Experience Platform提供了一个数据存储库和必要的工具，以高效、可靠的方式激活您的数据。 通过将数据保留在Platform中，它允许您在运行其他流程时派生属性，并且无需将数据导出到第三方工具进行操作和处理。 在处理数百个属性或营销策划时，此类处理开销会极大地影响项目时间表。 这为营销人员提供了访问其数据和构建营销活动的单一位置，以及对其消息进行分段和个性化的非常动态的方式。

## 后续步骤

通过阅读本文档，您现在应该了解如何 [!DNL Query Service] 不仅影响数据质量和区段的便利性，还会影响它在数据架构中对于整个端到端工作流程的重要性。 有关将Adobe Analytics与结合使用的更适用的SQL示例 [!DNL Query Service]，请参见 [Adobe Analytics促销变量用例](./merchandising-variables.md).

其他文档展示了 [!DNL Query Service] 对于贵组织的战略业务洞察，应当 [机器人过滤用例](./bot-filtering.md) 示例。

或者，这些文档有助于您了解 [!DNL Query Service] 功能：

* [查询执行指南](../best-practices/writing-queries.md)
* [数据资产组织指南](../best-practices/organize-data-assets.md).


