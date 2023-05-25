---
keywords: Experience Platform；产品购买方法；Data Science Workspace；热门主题；方法；预构建方法
solution: Experience Platform
title: 产品购买预测方法
description: 产品购买预测方法使您能够预测特定类型的客户购买事件（例如，产品购买）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 产品购买预测方法

产品购买预测方法使您能够预测特定类型的客户购买事件（例如，产品购买）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下文档将回答以下问题：
* 这个配方是为谁设计的？
* 这道菜有什么用？

## 这个配方是为谁设计的？

您的品牌寻求通过针对客户的有效促销活动来提高产品线的季度销售量。 不过，并非所有客户都一样，你希望自己的钱值得。 你瞄准谁？ 您的哪些客户最有可能作出响应而不会发现您的促销活动造成干扰？ 如何针对每位客户自定义促销活动？ 您应依赖哪些渠道以及何时应发送促销活动？

## 这道菜有什么用？

“产品购买预测”方法利用机器学习来预测客户购买行为。 它通过应用自定义的随机林分类器和双层体验数据模型(XDM)来预测购买事件的概率来实现这一点。 该模型利用包含客户个人资料信息和过去购买历史记录的输入数据，并默认为由我们的数据科学家确定的预先确定的配置参数，以提高预测准确性。

## 数据架构

此方法使用 [XDM架构](../../xdm/home.md) 为数据建模。 用于此方法的架构如下所示：

| 字段名称 | 类型 |
| --- | --- |
| userId | 字符串 |
| genderRatio | 数值 |
| ageY | 数值 |
| ageM | 数值 |
| optinEmail | 布尔值 |
| optinMobile | 布尔值 |
| optinAddress | 布尔值 |
| 已创建 | 整数 |
| totalOrders | 数值 |
| totalitems | 数值 |
| orderDate1 | 数值 |
| shippingDate1 | 数值 |
| totalPrice1 | 数值 |
| tax1 | 数值 |
| orderDate2 | 数值 |
| shippingDate2 | 数值 |
| totalPrice2 | 数值 |


## 算法

首先，训练数据集位于 *ProductPrediction* 架构已加载。 在此处，模型使用进行训练 [随机森林分类器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). 随机森林分类器是一种集成算法，它是指将多种算法组合起来以获得更好的预测性能的算法。 该算法的基本思想是随机森林分类器构建多个决策树，并将它们合并，以创建更准确、更稳定的预测。

此过程从创建一组决策树开始，决策树用于随机选择训练数据的子集。 然后，对每个决策树的结果进行平均。
