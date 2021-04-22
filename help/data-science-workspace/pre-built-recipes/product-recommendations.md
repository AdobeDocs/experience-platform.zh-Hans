---
keywords: Experience Platform；产品推荐菜谱；数据科学工作区；热门主题；菜谱；预构建菜谱
solution: Experience Platform
title: 产品推荐方法
topic-legacy: overview
description: 产品Recommendations菜谱使您能够根据客户的需求和兴趣提供个性化的产品推荐。 借助准确的预测模型，客户的购买历史记录可以为您提供关于他们可能感兴趣的产品的洞察。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
translation-type: tm+mt
source-git-commit: 441d7822f287fabf1b06cdf3f6982f9c910387a8
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 2%

---

# 产品推荐方法

产品Recommendations菜谱使您能够根据客户的需求和兴趣提供个性化的产品推荐。 借助准确的预测模型，客户的购买历史记录可以为您提供关于他们可能感兴趣的产品的洞察。

## 这个菜谱是谁做的？

在现代，零售商可以优惠大量产品，为客户提供大量选择，这也会妨碍客户搜索。 由于时间和精力的限制，客户可能找不到他们想要的产品，从而导致购买时存在高度的认知失调或根本没有购买。

## 这个菜谱是做什么的？

产品Recommendations菜谱使用机器学习来分析客户过去与产品的交互，并快速、轻松地生成个性化的产品推荐列表。 这将优化产品发现过程，并消除对客户的长期、低效、不相关的搜索。 因此，产品Recommendations菜谱可改善客户的整体购买体验，从而提高参与度和品牌忠诚度。

## 如何开始？

您可以按照Adobe Experience Platform Lab教程（请参阅下面的Lab链接）入门。 本教程将向您介绍如何在Jupyter Notebook中创建产品Recommendations菜谱，方法是按照[笔记本到菜谱](../jupyterlab/create-a-recipe.md)工作流，并在[!DNL Experience Platform] [!DNL Data Science Workspace]中实施菜谱。

* [实验：使用数据科学工作区预测未来](https://expleague.azureedge.net/labs/L777/index.html)
* [实验室资源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 数据模式

此菜谱使用自定义[XDM模式](../../xdm/schema/field-dictionary.md)来模拟输入和输出数据：

### 输入数据模式

| 字段名称 | 类型 |
| --- | --- |
| itemId | 字符串 |
| interactionType | 字符串 |
| timestamp | 字符串 |
| userId | 字符串 |

### 输出数据模式

| 字段名称 | 类型 |
| --- | --- |
| 建议 | 字符串 |
| userId | 整数 |

## 算法

产品Recommendations菜谱利用协作过滤为客户生成产品推荐的个性化列表。 与基于内容的方法不同，协作过滤不需要有关特定产品的信息，而是利用客户对一组产品的历史偏好。 这一强大的推荐技术使用了两个简单的假设：
* 有些客户兴趣相似，可以通过比较其购买和浏览行为对他们进行分组。
* 客户更有可能对基于相似客户的购买和浏览行为的推荐感兴趣。

此过程分为两个主要步骤。 首先，定义相似客户的子集。 然后，在这一集合中，确定这些客户之间的类似功能，以便为目标客户返回推荐。
