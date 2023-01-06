---
keywords: Experience Platform；产品购买方法；Data Science Workspace；热门主题；方法；预构建方法
solution: Experience Platform
title: 产品采购预测方法
description: “产品购买预测”方法允许您预测特定类型的客户购买事件（例如产品购买）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---

# 产品购买预测方法

“产品购买预测”方法允许您预测特定类型的客户购买事件（例如产品购买）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下文档将回答以下问题：
* 这食谱是为谁准备的？
* 这食谱是做什么的？

## 这食谱是为谁准备的？

您的品牌通过向客户进行有效且有针对性的促销，来寻求提升您产品线的季度销售。 但是，并非所有客户都是一样的，你希望自己的钱值钱。 你瞄准谁？ 哪些客户在发现促销活动影响不大的情况下最有可能做出响应？ 如何为每个客户自定义促销活动？ 您应该依赖哪些渠道，应何时发出促销活动？

## 这食谱是做什么的？

产品购买预测方法利用机器学习来预测客户购买行为。 它通过应用自定义的随机林分类器和两层体验数据模型(XDM)来预测购买事件的概率来实现这一点。 该模型利用输入数据，包括客户资料信息和过去的购买历史，并默认为由我们的数据科学家确定的预定配置参数，以提高预测准确性。

## 数据模式

此方法使用 [XDM模式](../../xdm/home.md) 来建模数据。 此方法使用的架构如下所示：

| 字段名称 | 类型 |
| --- | --- |
| userId | 字符串 |
| genderRatio | 数值 |
| ageY | 数值 |
| ageM | 数值 |
| optinEmail | 布尔型 |
| optinMobile | 布尔型 |
| optinAddress | 布尔型 |
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

首先， *产品预测* 架构已加载。 在此，模型使用 [随机林分类器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). 随机林分类器是一种集成算法，它指一种将多种算法组合在一起以获得改进的预测性能的算法。 该算法的思想是随机林分类器构建多个决策树并将它们合并，以创建更准确、更稳定的预测。

此过程首先创建一组决策树，该决策树随机选择训练数据的子集。 然后，对每个决策树的结果进行平均。
