---
keywords: 体验平台;产品推荐配方;数据科学工作区;热门话题;食谱;预构建配方
solution: Experience Platform
title: 产品推荐配方
description: 通过产品推荐配方，您可以根据客户的需求和兴趣提供个性化的产品推荐。 借助准确的预测模型，客户的购买历史记录可以让您深入了解他们可能对哪些产品感兴趣。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# 产品推荐方法

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

产品Recommendations方法允许您根据客户的需求和兴趣提供量身定制的个性化产品推荐。 借助准确的预测模型，客户的购买历史记录可以让您深入了解他们可能对哪些产品感兴趣。

## 这个配方是为谁设计的？

在现代，零售商可以提供多种产品，为客户提供大量选择，这也会阻碍客户的搜索。 由于时间和工作限制，客户可能无法找到所需的产品，从而导致购买时认知会出现高度不一致性或根本不会购买。

## 这个食谱有什么作用？

产品推荐配方使用机器学习来分析客户过去与产品的互动，并快速轻松地生成个性化的产品推荐列表。 这优化了产品发现过程，并消除了对客户的长时间、非生产性、不相关的搜索。 因此，产品推荐配方可以改善客户的整体购买体验，从而提高参与度和品牌忠诚度。

## 我该如何入门？

您可以按照Adobe Experience Platform实验室教程来开始操作（请参阅下面的实验室链接）。 本教程将向您展示如何在Jupyter Notebook中创建产品Recommendations方法，方法是按照[笔记本到方法](../jupyterlab/create-a-model.md)工作流进行操作，并在[!DNL Experience Platform] [!DNL Data Science Workspace]中实施方法。

* [实验室：使用数据科学Workspace预测未来](https://expleague.azureedge.net/labs/L777/index.html)
* [实验室资源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 数据架构

此方法使用自定义[XDM架构](../../xdm/schema/field-dictionary.md)对输入和输出数据进行建模：

### 输入数据架构

| 字段名称 | 类型 |
| --- | --- |
| itemId | 字符串 |
| interactionType | 字符串 |
| 时间戳 | 字符串 |
| userId | 字符串 |

### 输出数据架构

| 字段名称 | 类型 |
| --- | --- |
| 建议 | 字符串 |
| userId | 整数 |

## 算法

产品Recommendations方法利用协作筛选，为您的客户生成产品推荐的个性化列表。 与基于内容的方法不同，协作过滤不需要关于特定产品的信息，而是利用客户对一组产品的历史偏好。 这种强大的推荐技术使用两个简单的假设：
* 有些客户具有相似的兴趣，可通过比较其购买和浏览行为将其分组。
* 客户更有可能对基于相似客户的购买和浏览行为的推荐感兴趣。

此过程分为两个主要步骤。 首先，定义相似客户的子集。 然后，在该集中，确定这些客户之间的相似功能，以便返回对目标客户的建议。
