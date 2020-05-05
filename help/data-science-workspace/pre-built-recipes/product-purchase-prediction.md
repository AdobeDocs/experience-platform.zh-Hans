---
keywords: Experience Platform;product purchase recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: 产品购买处方
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# 产品购买处方

## 概述

“产品购买预测”菜谱使您能够预测特定类型的客户购买事件的可能性，例如产品购买。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下文档将回答以下问题：
* 这个菜谱是给谁做的？
* 这个菜谱是做什么的？

## 这个菜谱是给谁做的？

您的品牌寻求通过有效且有针对性的客户促销来提升您的产品系列的季度销售。 然而，并非所有客户都是一样的，而且您希望获得价值。 你目标谁？ 您的哪些客户在没有发现您的促销打扰的情况下，最有可能做出响应？ 如何为每位客户定制促销活动？ 您应依赖哪些渠道，以及何时发送促销？

## 这个菜谱是做什么的？

产品购买预测配方利用机器学习来预测客户购买行为。 它通过应用自定义随机林分类器和两层体验数据模型(XDM)来预测购买事件的概率来实现这一点。 该模型利用输入数据并入客户用户档案信息和过去购买历史，并默认为由我们的数据科学家确定的预先确定的配置参数，以增强预测准确性。

## 数据模式

此菜谱使 [用XDM模式](../../xdm/home.md) ，对数据进行建模。 此菜谱使用的模式如下所示：

| 字段名称 | 类型 |
--- | ---
| userId | 字符串 |
| 性别比率 | 数值 |
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

首先，加载ProductPrediction模式 *中的培* 训数据集。 从此，利用随机森林分类器对模 [型进行训练](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)。 随机森林分类器是一种集成算法，它指的是一种结合多种算法来获得改进预测性能的算法。 该算法的思想是随机森林分类器构建多个决策树并将它们合并，以创建更准确、更稳定的预测。

该过程开始于创建一组决策树，该决策树随机选择训练数据的子集。 然后，对每个决策树的结果进行平均。