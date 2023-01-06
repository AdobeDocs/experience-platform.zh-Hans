---
keywords: Experience Platform；产品推荐方法；Data Science Workspace；热门主题；方法；预构建方法
solution: Experience Platform
title: 产品推荐方法
description: 通过产品Recommendations方法，您可以根据客户的需求和兴趣提供个性化的产品推荐。 借助准确的预测模型，客户的购买历史记录可以为您提供关于他们可能感兴趣的产品的洞察信息。
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 3%

---

# 产品推荐方法

通过产品Recommendations方法，您可以根据客户的需求和兴趣提供个性化的产品推荐。 借助准确的预测模型，客户的购买历史记录可以为您提供关于他们可能感兴趣的产品的洞察信息。

## 这食谱是为谁准备的？

在现代，零售商可以提供多种产品，为客户提供大量选择，这也会阻碍客户搜索。 由于时间和精力的限制，客户可能找不到他们想要的产品，从而导致购买时认知不协调，或根本不购买。

## 这食谱是做什么的？

产品Recommendations方法使用机器学习来分析客户过去与产品的交互，并快速轻松地生成产品推荐的个性化列表。 这可以优化产品发现过程，并消除对客户的长时间、低效、不相关的搜索。 因此，产品Recommendations方法可以改善客户的整体购买体验，从而提高参与度和品牌忠诚度。

## 如何开始操作？

您可以按照Adobe Experience Platform Lab教程（请参阅下面的Lab链接）来入门。 本教程将向您展示如何通过以下操作在Jupyter Notebook中创建产品Recommendations方法： [笔记本至配方](../jupyterlab/create-a-model.md) 工作流，并在中实施方法 [!DNL Experience Platform] [!DNL Data Science Workspace].

* [实验：使用数据科学工作区预测未来](https://expleague.azureedge.net/labs/L777/index.html)
* [实验室资源](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## 数据模式

此方法使用自定义 [XDM模式](../../xdm/schema/field-dictionary.md) 要为输入和输出数据建模，请执行以下操作：

### 输入数据架构

| 字段名称 | 类型 |
| --- | --- |
| itemId | 字符串 |
| interactionType | 字符串 |
| timestamp | 字符串 |
| userId | 字符串 |

### 输出数据架构

| 字段名称 | 类型 |
| --- | --- |
| 推荐 | 字符串 |
| userId | 整数 |

## 算法

“产品Recommendations”方法利用协作筛选，为您的客户生成产品推荐的个性化列表。 协作过滤与基于内容的方法不同，它不需要有关特定产品的信息，而是利用客户对一组产品的历史偏好。 这种功能强大的推荐技术使用了两个简单的假设：
* 有些客户具有相似的兴趣，可以通过比较他们的购买和浏览行为来对他们进行分组。
* 客户在购买和浏览行为方面更有可能感兴趣的是基于相似客户的推荐。

此过程分为两个主要步骤。 首先，定义相似客户的子集。 然后，在该集内，确定这些客户之间的类似功能，以便返回目标客户的推荐。
