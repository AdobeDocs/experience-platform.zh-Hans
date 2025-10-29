---
keywords: Experience Platform；优化；模型；数据科学Workspace；热门主题；模型见解
solution: Experience Platform
title: 使用模型分析框架优化模型
type: Tutorial
description: 模型分析框架为数据科学家提供了数据科学Workspace中的工具，以便他们根据实验快速明智地选择最佳机器学习模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# 使用模型分析框架优化模型

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

模型分析框架为[!DNL Data Science Workspace]中的数据科学家提供了工具，以便根据实验快速明智地选择最佳机器学习模型。 该框架将提高机器学习工作流的速度和有效性，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供默认模板来协助模型调整来实现的。 最终结果允许数据科学家和公民数据科学家为其最终客户做出更好的模型优化决策。

## 什么是量度？

在实施和培训模型后，数据科学家的下一步工作是了解模型表现如何。 可使用各种量度来确定模型与其他量度相比的有效性。 使用的一些量度示例包括：

- 分类准确性
- 曲线下的区域
- 混淆矩阵
- 分类报告

## 配置方法代码

目前，模型分析框架支持以下运行时：

- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

可以在[下的](https://github.com/adobe/experience-platform-dsw-reference)experience-platform-dsw-reference`recipes`存储库中找到配方代码示例。 在本教程中，将引用此存储库中的特定文件。

### Scala {#scala}

可通过两种方式将量度引入到配方中。 一种是使用SDK提供的默认评估指标，另一种是编写自定义评估指标。

#### Scala的默认评估指标

默认评估作为分类算法的一部分进行计算。 以下是当前实施的评估器的一些默认值：

| 计算器类 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可以在[文件夹的](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)application.properties`recipe`文件中的方法中定义计算器。 启用`DefaultBinaryClassificationEvaluator`的示例代码如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用计算器类后，默认情况下将在训练期间计算多个量度。 通过将以下行添加到`application.properties`，可以显式声明默认量度。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定义该量度，则默认量度将处于活动状态。

可以通过更改`evaluation.metrics.com`的值来启用特定量度。 在以下示例中，启用了F分数量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每个类的默认度量。 用户还可以使用`evaluation.metric`列中的值来启用特定量度。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` |  — 精确度<br> — 召回<br> — 混淆矩阵<br>-F分数<br> — 精确度<br> — 接收器操作特性下的接收器操作特性<br> — 区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` |  — 精确度<br> — 召回<br> — 混淆矩阵<br>-F分数<br> — 精确度<br> — 接收器操作特性下的接收器操作特性<br> — 区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -Mean Average Precision (MAP) <br> — 规范化的贴现累积增益<br>-Mean Reciprocal Rank <br>-Metric K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定义评估指标

可通过在`MLEvaluator.scala`文件中扩展`Evaluator.scala`的接口来提供自定义计算器。 在示例[Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)文件中，我们定义了自定义`split()`和`evaluate()`函数。 我们的`split()`函数以8:2的比率随机拆分数据，我们的`evaluate()`函数定义和返回3个量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>对于`MLMetric`类，创建新`"measures"`时不要对`valueType`使用`MLMetric`，否则自定义评估指标表中不会填充该指标。
>  
> 执行操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


一旦在方法中定义了，下一步就是在方法中启用它。 此操作在项目的[文件夹中的](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)application.properties`resources`文件中完成。 此处，`evaluation.class`设置为`Evaluator`中定义的`Evaluator.scala`类

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在[!DNL Data Science Workspace]中，用户将能够在试验页面的“评估指标”选项卡中看到见解。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前，[!DNL Python]或[!DNL Tensorflow]没有默认评估指标。 因此，要获取[!DNL Python]或[!DNL Tensorflow]的评估指标，您需要创建一个自定义评估指标。 可以通过实现`Evaluator`类来完成此操作。

#### [!DNL Python]的自定义评估指标

对于自定义评估量度，需要为评估器实施两种主要方法： `split()`和`evaluate()`。

对于[!DNL Python]，将在[类的](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)evaluator.py`Evaluator`中定义这些方法。 按照[evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)链接查看`Evaluator`的示例。

在[!DNL Python]中创建评估量度需要用户实施`evaluate()`和`split()`方法。

`evaluate()`方法返回度量对象，该度量对象包含属性为`name`、`value`和`valueType`的度量对象的数组。

`split()`方法的目的是输入数据并输出训练和测试数据集。 在我们的示例中，`split()`方法使用`DataSetReader` SDK输入数据，然后通过删除不相关的列来清理数据。 从那里，利用数据中的现有原始功能创建其他功能。

`split()`方法应返回训练和测试数据流，然后`pipeline()`方法使用该数据流来训练和测试ML模型。

#### Tensorflow的自定义评估指标

对于[!DNL Tensorflow]，与[!DNL Python]类似，需要实现`evaluate()`类中的方法`split()`和`Evaluator`。 对于`evaluate()`，应返回`split()`的量度，同时返回训练数据集和测试数据集。

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

截至目前，R没有默认的评估指标。因此，要获取R的评估指标，您需要将`applicationEvaluator`类定义为方法的一部分。

#### R的自定义评估指标

`applicationEvaluator`的主要用途是返回包含量度的键值对的JSON对象。

此[applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R)可以用作示例。 在此示例中，`applicationEvaluator`被拆分为三个熟悉的部分：

- 加载数据
- 数据准备/功能工程
- 检索已保存的模型并评估

首先从[retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)中定义的源将数据加载到数据集。 从那里，数据被清理和工程化以适合机器学习模型。 最后，利用该模型对数据集进行预测，根据预测值和实际值计算指标。 在这种情况下，在`metrics`对象中定义和返回MAPE、MAE和RMSE。

## 使用预建量度和可视化图表

[!DNL Sensei Model Insights Framework]将为每种类型的机器学习算法支持一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估指标和可视化图表。

| ML算法类型 | 评估指标 | 可视化 |
| --- | --- | --- |
| 回归 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二进制分类 |  — 混淆矩阵<br> — 精确召回率<br> — 精确度<br>-F分数（具体为F1，F2）<br>- AUC<br>- ROC | ROC曲线和混淆矩阵 |
| 多类分类 |  — 混淆矩阵<br> — 对于每个类： <br> — 精确召回率<br>- F分数（具体为F1、F2） | ROC曲线和混淆矩阵 |
| 群集（包含基本真实值） | - NMI（归一化互信息分数）、AMI（经调整的互信息分数）<br>- RI（兰德指数）、ARI（经调整的兰德指数）<br> — 一致性分数、完整性分数和V-measure<br>- FMI（福克斯 — 马洛指数）<br> — 纯度<br>- Jaccard指数 | 显示反映落于簇内的数据点的相对簇大小的簇和质心的簇图 |
| 群集（不含地面真实值） |  — 惯性<br> — 剪影系数<br>-CHI（Calinski-Harabaz指数）<br>-DBI（Davies-Bouldin指数）<br>-Dunn指数 | 显示反映落于簇内的数据点的相对簇大小的簇和质心的簇图 |
| 推荐 | -Mean Average Precision (MAP) <br> — 规范化的贴现累积增益<br>-Mean Reciprocal Rank <br>-Metric K | 待定 |
| TensorFlow用例 | 张量流模型分析(TFMA) | 深度比较神经网络模型比较/可视化 |
| 其他/错误捕获机制 | 模型作者定义的自定义量度逻辑（以及相应的评估图表）。 在模板不匹配的情况下正常处理错误 | 具有评估量度的键值对的表 |
