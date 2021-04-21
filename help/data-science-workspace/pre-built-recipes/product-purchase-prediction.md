---
keywords: Experience Platform；产品购买菜谱；数据科学工作区；热门主题；菜谱；预构建菜谱
solution: Experience Platform
title: 产品采购预测方法
topic-legacy: overview
description: “产品购买预测”方法使您能够预测某类客户购买事件（例如产品购买）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 产品购买预测方法

“产品购买预测”方法使您能够预测某类客户购买事件（例如产品购买）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下文档将回答以下问题：
* 这个菜谱是谁做的？
* 这个菜谱是做什么的？

## 这个菜谱是谁做的？

您的品牌寻求通过有效和有针对性的客户促销来提升您产品线的季度销售。 但是，并非所有客户都是一样的，而且您希望获得价值。 你目标谁？ 您的哪些客户在不发现您的促销活动打扰您的情况下，最有可能做出回应？ 如何为每位客户定制促销活动？ 您应依赖哪些渠道，何时发送促销？

## 这个菜谱是做什么的？

“产品购买预测”方法利用机器学习来预测客户购买行为。 它通过应用定制的随机森林分类器和两层体验数据模型(XDM)来预测购买事件的概率来实现这一目的。 该模型利用输入数据，包括客户用户档案信息和过去购买历史以及默认为由我们的数据科学家确定的预定配置参数，以提高预测准确性。

## 数据模式

此菜谱使用[XDM模式](../../xdm/home.md)来模拟数据。 用于此菜谱的模式如下所示：

| 字段名称 | 类型 |
--- | ---
| userId | 字符串 |
| 性别比 | 数值 |
| ageY | 数值 |
| ageM | 数值 |
| optinEmail | 布尔值 |
| optinMobile | 布尔值 |
| optinAddress | 布尔值 |
| 已创建 | 整数 |
| totalOrders | 数值 |
| totalItems | 数值 |
| orderDate1 | 数值 |
| shippingDate1 | 数值 |
| totalPrice1 | 数值 |
| tax1 | 数值 |
| orderDate2 | 数值 |
| shippingDate2 | 数值 |
| totalPrice2 | 数值 |


## 算法

首先，加载&#x200B;*ProductPrediction*&#x200B;模式中的培训数据集。 在此，使用[随机森林分类器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)训练模型。 随机森林分类器是一种集成算法，它指的是一种结合多种算法的算法，以获得改进的预测性能。 算法的思想是随机森林分类器构建多个决策树并合并它们，以创建更准确、更稳定的预测。

该过程开始于创建一组随机选择训练数据子集的决策树。 然后，对每个决策树的结果进行平均。
