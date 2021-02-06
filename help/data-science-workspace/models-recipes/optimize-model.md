---
keywords: Experience Platform；优化；模型；数据科学工作区；热门主题；模型洞察
solution: Experience Platform
title: 使用模型洞察框架优化模型
topic: tutorial
type: Tutorial
description: 模型洞察框架为数据科学家提供数据科学工作区中的工具，以便快速、明智地选择基于实验的最优机器学习模型。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---


# 使用模型洞察框架优化模型

模型洞察框架为数据科学家提供[!DNL Data Science Workspace]中的工具，以便快速、明智地选择基于实验的最佳机器学习模型。 该框架将提高机器学习工作流程的速度和效率，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供一个默认模板来辅助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为最终客户做出更好的模型优化决策。

## 什么是指标？

在实施和培训模型之后，数据科学家下一步要做的就是找出模型的性能。 各种指标被用来找出模型与其他模型相比的效果。 使用的一些指标示例包括：
- 分类准确性
- 曲线下的区域
- 混淆矩阵
- 分类报告

## 配置菜谱代码

目前，Model Insights Framework支持以下运行时：
- [斯卡拉](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

菜谱的示例代码位于`recipes`下的[experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference)存储库中。 本教程将引用此存储库中的特定文件。

### Scala {#scala}

有两种方法可将指标引入菜谱。 一种是使用SDK提供的默认评估指标，另一种是编写自定义评估指标。

#### Scala的默认评估指标

默认评估作为分类算法的一部分进行计算。 以下是当前实现的计算器的一些默认值：

| 计算器类 | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

计算器可在`recipe`文件夹[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)文件的菜谱中定义。 启用`DefaultBinaryClassificationEvaluator`的示例代码如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用评估器类后，默认情况下，在培训期间将计算许多度量。 可通过向`application.properties`添加以下行显式声明默认度量。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定义度量，则默认度量将处于活动状态。

可通过更改`evaluation.metrics.com`的值来启用特定度量。 在以下示例中，启用了F-Score量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每个类的默认度量。 用户还可以使用`evaluation.metric`列中的值来启用特定度量。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | -Precision <br>-Recall <br>-Dussing Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Features <br>-Area Under Receiver Operating Features | -`PRECISION`<br>-`RECALL`<br>-`CONFUSION_MATRIX`<br>-`FSCORE`<br>-`ACCURACY`<br>-`ROC`<br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Dussing Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Features <br>-Area Under Receiver Operating Features | -`PRECISION`<br>-`RECALL`<br>-`CONFUSION_MATRIX`<br>-`FSCORE`<br>-`ACCURACY`<br>-`ROC`<br>-`AUROC` |
| `RecommendationsEvaluator` | -平均平均精度(MAP)<br>-归一化折扣积分<br>-平均倒数秩<br>-度量K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定义评估指标

可通过扩展`Evaluator.scala`文件中`MLEvaluator.scala`的接口来提供自定义计算器。 在示例[Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)文件中，我们定义自定义`split()`和`evaluate()`函数。 我们的`split()`函数以8:2的比率随机拆分我们的数据，而我们的`evaluate()`函数定义并返回3个度量：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>对于`MLMetric`类，在创建新的`MLMetric`时，不要将`"measures"`用于`valueType`，否则该度量将不填充到自定义评估度量表中。
>  
> 执行以下操作：`metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是：`metrics.add(new MLMetric("MAPE", mape, "measures"))`


在菜谱中定义后，下一步是在菜谱中启用它。 这是在项目`resources`文件夹中的[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)文件中完成的。 这里，`evaluation.class`设置为`Evaluator.scala`中定义的`Evaluator`类

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在[!DNL Data Science Workspace]中，用户将能够在实验页的“评估指标”选项卡中查看洞察。

### [!DNL Python/Tensorflow] {#pythontensorflow}

目前，[!DNL Python]或[!DNL Tensorflow]没有默认的评估指标。 因此，要获取[!DNL Python]或[!DNL Tensorflow]的评估指标，您需要创建自定义的评估指标。 这可以通过实现`Evaluator`类来实现。

#### [!DNL Python]的自定义评估指标

对于自定义评估指标，需要为评估器实现两种主要方法：`split()`和`evaluate()`。

对于[!DNL Python]，这些方法将在`Evaluator`类的[求值器。py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)中定义。 有关`Evaluator`的示例，请按照[求值器。py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)链接操作。

在[!DNL Python]中创建评估度量要求用户实现`evaluate()`和`split()`方法。

`evaluate()`方法返回包含属性为`name`、`value`和`valueType`的度量对象数组的度量对象。

`split()`方法的目的是输入数据并输出培训和测试数据集。 在我们的示例中，`split()`方法使用`DataSetReader` SDK输入数据，然后通过删除不相关列来清除数据。 从此处，数据中的现有原始功能将创建更多功能。

`split()`方法应返回培训和测试数据帧，然后由`pipeline()`方法使用该数据帧来训练和测试ML模型。

#### Tensorflow的自定义评估指标

对于[!DNL Tensorflow]，与[!DNL Python]类似，`Evaluator`类中的`evaluate()`和`split()`方法需要实现。 对于`evaluate()`，应返回度量，而`split()`返回培训和测试数据集。

```PYTHON
from ml.runtime.python.Interfaces.AbstractEvaluator import AbstractEvaluator

class Evaluator(AbstractEvaluator):
    def __init__(self):
       print ("initiate")

    def evaluate(self, data=[], model={}, config={}):

        return metrics

    def split(self, config={}):

       return 'train', 'test'
```

### R {#r}

目前，R没有默认的评估指标。因此，要获得R的评估指标，您需要将`applicationEvaluator`类定义为菜谱的一部分。

#### R的自定义评估指标

`applicationEvaluator`的主要用途是返回一个JSON对象，其中包含度量的键值对。

此[applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R)可以用作示例。 在本例中，`applicationEvaluator`分为三个熟悉的部分：
- 加载数据
- 数据准备／功能工程
- 检索保存的模型并评估

数据首先从[retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)中定义的源加载到数据集。 从此处，数据被清理并设计为适合机器学习模型。 最后，利用数据集进行预测，并根据预测值和实际值计算指标。 在这种情况下，在`metrics`对象中定义并返回MAPE、MAE和RMSE。

## 使用预建指标和可视化图表

[!DNL Sensei Model Insights Framework]将支持每种机器学习算法的一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估指标和可视化。

| ML算法类型 | 评估指标 | 可视化图表 |
--- | --- | ---
| 回归 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二进制分类 | -混淆矩阵<br>- Precision-recall<br>- Accuracy<br>- F-score（特别是F1,F2）<br>- AUC<br>- ROC | ROC曲线与混淆矩阵 |
| 多类分类 | -混淆矩阵<br>-对于每个类：<br>- precision-recall准确度<br>- F-score（特别是F1、F2） | ROC曲线与混淆矩阵 |
| 聚类（含地面真度） | - NMI（标准化互信息得分）、AMI（调整互信息得分）<br>- RI（Rand指数）、ARI（调整后兰德指数）<br>-同质得分、完整性得分和V-measure<br>- FMI（Fowlkes-Mallows指数）<br>-纯度<br>- Jacccaccccccccepsard指数 | 具有相对簇大小的簇和中心线的簇图反映位于簇内的数据点 |
| 聚类（无地面真度） | -惯性<br>-侧影系数<br>- CHI（Calinski-Harabaz指数）<br>- DBI（Davies-Bouldin指数）<br>- Dunnindex | 具有相对簇大小的簇和中心线的簇图反映位于簇内的数据点 |
| 推荐 | -平均平均精度(MAP)<br>-归一化折扣积分<br>-平均倒数秩<br>-度量K | 待定 |
| TensorFlow用例 | 张量流模型分析(TFMA) | 深度比较神经网络模型比较／可视化 |
| 其他／错误捕获机制 | 由模型作者定义的自定义度量逻辑（和相应的评估图表）。 模板不匹配时的适当错误处理 | 具有评估指标的键值对的表 |
