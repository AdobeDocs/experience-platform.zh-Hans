---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 产品推荐菜谱
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 产品推荐菜谱

产品推荐菜谱使您能够根据客户的需求和兴趣提供个性化的产品推荐。 借助准确的预测模型，客户的购买历史可为您提供关于他们可能感兴趣的产品的洞察。

## 这个菜谱是给谁做的？

在现代，零售商可以优惠大量产品，为客户提供大量选择，这也会妨碍客户搜索。 由于时间和精力的限制，客户可能找不到他们想要的产品，从而导致购买时存在高度认知失调或根本不购买。

## 这个菜谱是做什么的？

“产品推荐”菜谱使用机器学习来分析客户过去与产品的交互，并快速、轻松地生成个性化的产品推荐列表。 这可以优化产品发现过程，并消除对客户的长期、非生产性、无关的搜索。 因此，“产品推荐”菜谱可改善客户的整体购买体验，从而提高参与度和品牌忠诚度。

## 如何开始？

您可以通过学习Adobe Experience Platform Lab教程（请参阅下面的实验室链接）开始。 本教程将向您展示如何在Jupyter Notebook中创建“产品推荐”菜谱，方法是按照笔记本到菜谱工作流 [程](../jupyterlab/create-a-recipe.md) ，并在Experience Platform Data Science Workspace中实施菜谱。

* [实验：利用数据科学工作区预测未来](https://expleague.azureedge.net/labs/L777/index.html)
* [实验室资源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 数据模式

此菜谱使用自定 [义XDM模式](../../xdm/schema/field-dictionary.md) ，为输入和输出数据建模：

### 输入数据模式

| 字段名称 | 类型 |
--- | ---
| itemId | 字符串 |
| interactionType | 字符串 |
| timestamp | 字符串 |
| userId | 字符串 |

### 输出数据模式

| 字段名称 | 类型 |
--- | ---
| 建议 | 字符串 |
| userId | 整数 |

## 算法

“产品推荐”菜谱利用协作过滤为客户生成个性化的产品推荐列表。 与基于内容的方法不同，协作过滤不需要关于特定产品的信息，而是利用客户对一组产品的历史偏好。 这一强大的推荐技术使用两个简单的假设：
* 有些客户具有类似的兴趣，可以通过比较其购买和浏览行为对他们进行分组。
* 客户在购买和浏览行为方面更可能对基于类似客户的推荐感兴趣。

该过程分为两个主要步骤。 首先，定义相似客户的子集。 然后，在该集合中确定这些客户之间的相似功能，以便为目标客户返回推荐。