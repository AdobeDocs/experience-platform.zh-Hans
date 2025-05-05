---
keywords: Experience Platform；查询服务；查询服务
title: Adobe Experience Platform查询服务的示例用例
description: 一个端到端示例，用于演示Adobe Experience Platform查询服务的通用性和好处。
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Adobe Experience Platform [!DNL Query Service]的示例用例

此文档和随附的视频演示文稿提供了一个高级别的端到端工作流程，演示了Adobe Experience Platform [!DNL Query Service]如何使贵组织的战略业务见解受益。 本指南以浏览放弃用例为例，说明了以下主要概念：

* 数据处理对于最大程度地发挥Adobe Experience Platform的潜力至关重要。
* 基于现有数据架构构建查询的方法。
* 确保满足您需求的数据质量，以及减少任何不足的方法。
* 安排查询以设定的频率运行，以用于分段中的下游和个性化的目标的过程。
* 通过[!DNL Query Service]的强大功能，营销人员可以轻松地将派生数据集包含在其受众中。

## 目标 {#objectives}

此工作流演示依赖于多个Adobe Experience Platform服务。 如果您希望跟进，建议您很好地了解以下功能和服务：

* 体验数据模型(XDM)架构组合的[基础知识](../../xdm/schema/composition.md)
* 如何[创建数据集并摄取数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=zh-Hans)
* 如何使用Adobe Analytics源连接器[摄取数据](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=zh-Hans)
* [区段](../../segmentation/home.md)
* [目标](../../destinations/home.md)

浏览放弃示例的中心内容是使用Adobe [!DNL Analytics]数据创建特定可操作的受众。 优化后的受众包括过去四天浏览网站但未购买的每位客户。 然后，受众中的每个用户档案均会定位到由客户行为模式产生的最高价格SKU。

查询本身具有非常强的规范性并且只包括符合区段定义用例标准的数据。 这通过最大限度地减少正在处理的[!DNL Analytics]数据来提高性能。 它还按价格从高到低对数据排序，并选择用户浏览的最高价格SKU。

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

## 使用adobe analytics的[!DNL Query Service]浏览放弃示例 {#video-example}

下面看到的视频演示提供了围绕[!DNL Query Service]和Adobe Analytics集成的Experience Platform数据的真实整体用例。

>[!VIDEO](https://video.tv.adobe.com/v/3454956?quality=12&learn=on&captions=chi_hans)

## [!DNL Query Service]的优势 {#benefits}

[!DNL Query Service]提供的功能有许多用途。 您可以使用它来适应复杂的分段逻辑、计算各种个性化属性以供下游使用，或极大地简化构建受众的方式。

[!DNL Query Service]允许您在查询中包含约束，以简化受众构建过程。 这可以通过确保适合受众的数据资格来提高数据质量。 保持查询质量可让受众准确无误，并且有助于提高数据的可靠性。 您还可以通过基于从查询派生的属性创建架构和自定义表来保存受众。 可以为配置文件启用自定义表，并且您可以使用这些数据点进行分段和个性化。 此功能可协助希望创建明确受众人群的营销人员。

此外，通过在查询中包含满足任何循环或静态条件的逻辑，[!DNL Query Service]可以减轻精细分段的负担。

Adobe Experience Platform提供了一个数据存储库和必要的工具，用于以高效、可靠的方式激活您的数据。 通过将数据保留在Experience Platform中，它允许您在运行其他流程时派生属性，并且消除将数据导出到第三方工具进行操作和处理的需要。 在处理数百个属性或营销策划时，此类处理间接费用会极大地影响项目时间表。 这为营销人员提供了访问其数据和构建营销活动的单一位置，以及一种非常动态的方式，可用于对消息进行分段和个性化。

## 后续步骤

通过阅读本文档，您现在应该了解[!DNL Query Service]不仅影响数据质量和分段便利性，还影响其在数据架构中对整个端到端工作流程的重要性。 有关将Adobe Analytics与[!DNL Query Service]结合使用的更适用的SQL示例，请参阅[Adobe Analytics促销变量用例](./merchandising-variables.md)。

显示[!DNL Query Service]对贵组织的战略业务见解有益的其他文档是[机器人过滤用例](./bot-filtering.md)示例。

或者，这些文档有助于您了解[!DNL Query Service]功能：

* [查询执行指南](../best-practices/writing-queries.md)
* [数据资产组织指南](../best-practices/organize-data-assets.md)。


