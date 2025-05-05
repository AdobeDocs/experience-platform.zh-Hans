---
keywords: 体验平台;优化;型;数据科学工作区;热门话题;模型见解
solution: Experience Platform
title: 使用模型见解框架优化模型
type: Tutorial
description: 模型分析框架为数据科学家提供了数据科学Workspace中的工具，以便他们根据实验快速明智地选择最佳机器学习模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1210'
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

目前， Model Insights Framework支持以下运行时：
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

可以在`recipes`下的[experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference)存储库中找到配方代码示例。 在本教程中，将引用此存储库中的特定文件。

### Scala {#scala}

可通过两种方式将量度引入到配方中。 一种是使用SDK提供的默认评估指标，另一种是编写自定义评估指标。

#### Scala的默认评估度量

默认评估作为分类算法的一部分进行计算。 以下是当前实施的赋值器的一些默认值：

| 赋值器类 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| 默认多分类赋值器 | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可以在`recipe`文件夹的[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)文件中的方法中定义该计算器。 启用`DefaultBinaryClassificationEvaluator`的示例代码如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用评估器类后，默认情况下将在培训期间计算一些指标。 通过将以下行添加到`application.properties`，可以显式声明默认度量。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定义该度量，则默认度量将处于活动状态。

可以通过更改`evaluation.metrics.com`的值来启用特定量度。 在以下示例中，启用了F分数量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每个类的默认度量。 用户还可以使用`evaluation.metric`列中的值来启用特定量度。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` |  — 精确度<br> — 召回<br> — 混淆矩阵<br>-F分数<br> — 精确度<br> — 接收器操作特性下的接收器操作特性<br> — 区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | -Precision <br>-Recall <br>-Conflusion Matrix <br>-F-Score <br>-Accuracy <br>-Receiver Operating Characters <br>-Area Under Receiver Operating Characters | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -平均精度 （MAP） <br>-归一化贴现累积增益 <br>-平均倒数排名 <br>-度量 K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala 的自定义评估指标

可通过在`Evaluator.scala`文件中扩展`MLEvaluator.scala`的接口来提供自定义计算器。 在示例[Evaluator.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala)文件中，我们定义了自定义`split()`和`evaluate()`函数。 我们的`split()`函数以8:2的比率随机拆分数据，我们的`evaluate()`函数定义并返回3个度量：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>对于`MLMetric`类，在创建新的`MLMetric`时不要将`"measures"`用于`valueType`，否则度量将不会填充到自定义评估度量表中。
>  
> 执行以下操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


在处方中定义后，下一步是在处方中启用它。 此操作在项目的`resources`文件夹中的[application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties)文件中完成。 此处，`evaluation.class`设置为`Evaluator.scala`中定义的`Evaluator`类

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在[!DNL Data Science Workspace]中，用户将能够在试验页面的“评估指标”选项卡中看到见解。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前，[!DNL Python]或[!DNL Tensorflow]没有默认评估指标。 因此，要获取[!DNL Python]或[!DNL Tensorflow]的评估指标，您需要创建一个自定义评估指标。 可以通过实现`Evaluator`类来完成此操作。

#### [!DNL Python]的自定义评估指标

对于自定义评估指标，需要为评估器实现两种主要方法： `split()` 和 `evaluate()`。

对于 [!DNL Python]，这些方法将在类的 `Evaluator` evaluator.py[&#128279;](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 中定义。[访问 evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 链接以获取 的示例`Evaluator`。

在中创建 [!DNL Python] 评估指标需要用户实现 `evaluate()` 和 `split()` 方法。

该方法`evaluate()`返回度量对象，其中包含属性为 、 `value`和 `valueType`的`name`度量对象数组。

`split()`方法的目的是输入数据并输出训练和测试数据集。 在我们的示例中，该方法 `split()` 使用 `DataSetReader` SDK 输入数据，然后通过删除不相关的列来清理数据。 从那里，利用数据中的现有原始功能创建其他功能。

`split()`方法应返回训练和测试数据流，然后`pipeline()`方法使用该数据流来训练和测试ML模型。

#### Tensorflow的自定义评估指标

对于[!DNL Tensorflow]，与[!DNL Python]类似，需要实现`Evaluator`类中的方法`evaluate()`和`split()`。 对于`evaluate()`，应返回`split()`的量度，同时返回训练数据集和测试数据集。

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

## 使用预构建的量度和可视化图表

[!DNL Sensei Model Insights Framework]将为每种类型的机器学习算法支持一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估指标和可视化图表。

| ML算法类型 | 评估指标 | 可视化 |
| --- | --- | --- |
| 回归 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二元分类 | - 混淆矩阵<br> - 精度召回<br>率 - 准确性- F<br> 分数（特别是 F1 ，F2）<br>- AUC<br> - ROC | ROC 曲线和混淆矩阵 |
| 多类分类 |  — 混淆矩阵<br> — 对于每个类： <br> — 精确召回精度<br>- F分数（特别是F1、F2） | ROC曲线和混淆矩阵 |
| 群集（包含基本真实值） | - NMI（归一化互信息分数）、AMI（经调整的互信息分数）<br>- RI（兰德指数）、ARI（经调整的兰德指数）<br> — 一致性分数、完整性分数和V-measure<br>- FMI（福克斯 — 马洛指数）<br> — 纯度<br>- Jaccard指数 | 显示反映落于簇内的数据点的相对簇大小的簇和质心的簇图 |
| 群集（不含地面真实值） |  — 惯性<br> — 剪影系数<br>-CHI（Calinski-Harabaz指数）<br>-DBI（Davies-Bouldin指数）<br>-Dunn指数 | 显示反映落于簇内的数据点的相对簇大小的簇和质心的簇图 |
| 推荐 | -Mean Average Precision (MAP) <br> — 规范化的贴现累积增益<br>-Mean Reciprocal Rank <br>-Metric K | 待定 |
| TensorFlow用例 | TensorFlow 模型分析 （TFMA） | 深度比较神经网络模型比较/可视化 |
| 其他/错误捕获机制 | 模型作者定义的自定义指标逻辑（以及相应的评估图表）。 在模板不匹配的情况下妥善处理错误 | 具有用于评估度量的键值对的表 |
