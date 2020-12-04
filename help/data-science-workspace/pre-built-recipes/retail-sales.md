---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics;recipes;pre build recipe
solution: Experience Platform
title: 零售销售处方
topic: overview
description: “零售销售”菜谱允许您预测特定时间段内系统初始的所有商店的销售预测。 通过准确的预测模型，零售商将能够找到需求与定价策略之间的关系并做出优化的定价决策，以最大化销售和收入。
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 2%

---


# 零售销售处方

“零售销售”菜谱允许您预测特定时间段内系统初始的所有商店的销售预测。 通过准确的预测模型，零售商将能够找到需求与定价策略之间的关系并做出优化的定价决策，以最大化销售和收入。

以下文档将回答以下问题：
* 这个菜谱是给谁做的？
* 这个菜谱是做什么的？
* 如何开始？

## 这个菜谱是给谁做的？

在当前市场中，零售商要保持竞争力，面临着许多挑战。 您的品牌寻求提升零售品牌的年销售额，但需要做出许多决策以最大限度地降低运营成本。 供应过多会增加库存成本，而供应过少则会增加客户流失到其他品牌的风险。 你需要在未来几个月订购更多供应吗？ 您如何确定产品的最佳定价以保持每周销售目标？

## 这个菜谱是做什么的？

零售销售预测菜谱使用机器学习来预测销售趋势。 这种方法是利用大量历史零售数据和定制梯度提升回归或机器学习算法，提前一周预测销售额。 该模型利用过去的购买历史并默认为由我们的数据科学家确定的预先确定的配置参数，以增强预测准确性。

## 如何开始？

您可以按照本教程开始 [学习](../jupyterlab/create-a-recipe.md)。

本教程将在Jupyter笔记本中创建零售销售菜谱，并使用笔记本制作菜谱工作流程在Adobe Experience Platform创建菜谱。

## 数据模式

此菜谱使 [用XDM模式](../../xdm/schema/field-dictionary.md) ，对数据进行建模。 此菜谱使用的模式如下所示：

| 字段名称 | 类型 |
--- | ---
| 日期 | 字符串 |
| 商店 | 整数 |
| storeType | 字符串 |
| weeklySales | 数值 |
| storeSize | 整数 |
| 温度 | 数值 |
| regionalFuelPrice | 数值 |
| 标记 | 数值 |
| 消费 | 数值 |
| 失业 | 数值 |
| isHoliday | 布尔值 |


## 算法

首先，加载DSWRetailSales模式 *中的培训* 数据集。 在此基础上，采用梯度推进回归 [算法对模型进行训练](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html)。 渐变提升使用的思想是弱学习者（至少比随机机会略好）可以形成一系列侧重于改善前一个学习者弱点的学习者。 总之，它们可用于创建强大的预测模型。

该过程涉及三个元素：损失函数、弱学习者和加性模型。

损失函数是指预测模型在能够预测预期结果方面的良好程度的度量——最小二乘回归在此配方中被使用。

在渐变提升中，决策树用作弱学习者。 通常，具有受限数量的层、节点和拆分的树用于确保学员保持弱。

最后，采用了加性模型。 在用损失函数计算损失后，选择减少损失的树并加权，以改进对较难观测的建模。 然后，将加权树的输出添加到现有的树序列中，以改进模型的最终输出——未来销售的数量。