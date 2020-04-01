---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 产品购买方法
topic: overview
translation-type: tm+mt
source-git-commit: f548fb6431b7bc71c205a2b2b7ca3884e57340b1

---


# 产品购买方法

## 概述

“产品购买预测”菜谱使您能够预测特定类型的客户购买事件（例如产品购买）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下文档将回答以下问题：
* 这个菜谱是给谁做的？
* 这个菜谱是做什么的？

## 这个菜谱是给谁做的？

您的品牌寻求通过有效且有针对性的客户促销来提升您的产品线的季度销售。 但是，并非所有客户都是一样的，而且您需要的是价值。 你目标谁？ 您的哪些客户在不打扰您的促销活动的情况下最有可能做出响应？ 如何为每位客户定制促销活动？ 您应依赖哪些渠道，何时发送促销？

## 这个菜谱是做什么的？

“产品购买预测”菜谱利用机器学习来预测客户购买行为。 它通过应用自定义的随机森林分类器和两层体验数据模型(XDM)来预测购买事件的概率来实现这一目的。 该模型利用输入数据，并入客户用户档案信息和过去购买历史以及默认值为由我们的数据科学家确定的预定配置参数，以提高预测准确性。

## 数据模式

此菜谱使用 [XDM模式](../../xdm/home.md) ，以模拟数据。 用于此菜谱的模式如下所示：

| 字段名称 | 类型 |
--- | ---
| userId | 字符串 |
| gederRatio | 数值 |
| ageY | 数值 |
| ageM | 数值 |
| optinEmail | Boolean |
| optinMobile | Boolean |
| optinAddress | Boolean |
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

首先，加载 **ProductPrediction模式中的培** 训数据集。 在此，利用随机森林分类器对模型 [进行训练](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)。 随机森林分类器是一种集成算法，它指的是一种结合多种算法来获得改进预测性能的算法。 该算法的思想是随机森林分类器构建多个决策树并将它们合并，以创建更准确、稳定的预测。

该过程开始于创建一组随机选择训练数据子集的决策树。 然后，对每个决策树的结果进行平均。