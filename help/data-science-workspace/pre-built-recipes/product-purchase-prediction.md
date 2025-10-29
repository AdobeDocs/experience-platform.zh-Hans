---
keywords: Experience Platform；产品购买方法；数据科学Workspace；热门主题；方法；预构建方法
solution: Experience Platform
title: 产品购买预测方法
description: 产品购买预测方法使您能够预测特定类型的客户购买事件（例如，产品购买）的可能性。
exl-id: 66a45629-33a3-4081-8dbd-b864983b8f57
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 4%

---

# 产品购买预测方法

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

产品购买预测方法使您能够预测特定类型的客户购买事件（例如，产品购买）的可能性。

![](../images/pre-built-recipes/ppp_bigpicture.png)

以下文档将回答类似下面的问题：

* 这个配方是为谁设计的？
* 这个配方有什么用？

## 这个配方是为谁设计的？

您的品牌寻求通过针对客户的有效促销活动来提高产品线的季度销售额。 不过，并不是所有客户都一样，你希望自己的钱值钱。 你瞄准谁？ 您的哪些客户最有可能作出响应，而不会认为您的促销活动会造成干扰？ 如何针对每位客户自定义促销活动？ 您应该依赖哪些渠道？何时应发送促销活动？

## 这个配方有什么用？

产品购买预测方法利用机器学习来预测客户购买行为。 它通过应用自定义的随机林分类器和双层体验数据模型(XDM)来预测购买事件的概率来实现这一点。 该模型利用包含客户个人资料信息和过去购买历史记录的输入数据，并默认为由我们的数据科学家确定的预先确定的配置参数，以提高预测准确性。

## 数据架构

此方法使用[XDM架构](../../xdm/home.md)来建模数据。 用于此方法的架构如下所示：

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
| totalorders | 数值 |
| totalitems | 数值 |
| orderDate1 | 数值 |
| shippingDate1 | 数值 |
| totalPrice1 | 数值 |
| tax1 | 数值 |
| orderDate2 | 数值 |
| shippingDate2 | 数值 |
| totalPrice2 | 数值 |


## 算法

首先，加载&#x200B;*ProductPrediction*&#x200B;架构中的训练数据集。 在此处，使用[随机林分类器](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)训练模型。 随机森林分类器是一种集成算法，它综合了多种算法来提高预测性能。 该算法的基本思想是随机森林分类器构建多个决策树，并将它们合并，以创建更准确、更稳定的预测。

此过程从创建一组决策树开始，决策树用于随机选择训练数据的子集。 然后，对各决策树的结果进行平均。
