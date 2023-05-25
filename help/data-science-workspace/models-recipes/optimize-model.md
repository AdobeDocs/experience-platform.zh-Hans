---
keywords: Experience Platform；优化；模型；Data Science Workspace；热门主题；模型分析
solution: Experience Platform
title: 使用模型分析框架优化模型
type: Tutorial
description: 模型洞察框架为数据科学家提供了数据科学工作区中的工具，以便他们根据实验对最佳机器学习模型做出快速、明智的选择。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 使用模型分析框架优化模型

模型分析框架为数据科学家提供了以下工具： [!DNL Data Science Workspace] 通过实验对最优的机器学习模型进行快速明智的选择。 该框架将提高机器学习工作流的速度和效率，并改善数据科学家的易用性。 这是通过为每个机器学习算法类型提供默认模板来协助模型调整来完成的。 最终结果允许数据科学家和公民数据科学家为其最终客户做出更好的模型优化决策。

## 什么是量度？

在实施和培训模型后，数据科学家的下一步工作是确定模型表现如何。 可使用各种量度来了解模型与其他模型相比的有效性。 使用的一些量度示例包括：
- 分类准确性
- 曲线下的区域
- 混淆矩阵
- 分类报告

## 配置方法代码

目前，模型分析框架支持以下运行时：
- [Scala](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

可在以下位置找到方法的示例代码： [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) 存储库位于 `recipes`. 在本教程中，将引用此存储库中的特定文件。

### Scala {#scala}

可通过两种方式将量度引入配方。 一种是使用SDK提供的默认评估指标，另一种是编写自定义评估指标。

#### Scala的默认评估指标

默认评估作为分类算法的一部分计算。 以下是当前实施的评估器的一些默认值：

| 计算器类 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可在的方法中定义评估器 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 中的文件 `recipe` 文件夹。 示例代码启用 `DefaultBinaryClassificationEvaluator` 如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用计算器类后，默认情况下将在训练期间计算多个量度。 通过将以下行添加到 `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定义该量度，则默认量度将处于活动状态。

可以通过更改的值来启用特定量度 `evaluation.metrics.com`. 在以下示例中，启用了F分数量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每个类的默认度量。 用户还可以使用 `evaluation.metric` 列来启用特定量度。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` |  — 精度 <br>-Recall <br> — 混淆矩阵 <br>-F分数 <br> — 精度 <br> — 接收器工作特性 <br> — 接收器下的区域工作特性 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` |  — 精度 <br>-Recall <br> — 混淆矩阵 <br>-F分数 <br> — 精度 <br> — 接收器工作特性 <br> — 接收器下的区域工作特性 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` |  — 平均平均精度(MAP) <br> — 标准化折现累积收益 <br> — 平均倒数排名 <br> — 量度K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定义评估指标

通过扩展以下项的界面，可提供自定义求值器： `MLEvaluator.scala` 在您的 `Evaluator.scala` 文件。 在本例中 [Evaluator.scale](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 文件，我们定义自定义 `split()` 和 `evaluate()` 函数。 我们的 `split()` 函数以8:2的比率随机拆分我们的数据，并且 `evaluate()` 函数定义和返回3个量度：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>对于 `MLMetric` 类，请勿使用 `"measures"` 对象 `valueType` 创建新时 `MLMetric` 否则该量度将不会填充到自定义评估量度表中。
>  
> 执行此操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是这样： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


一旦在方法中定义了，下一步就是要在方法中启用它。 此操作可在 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 项目中的文件 `resources` 文件夹。 此处 `evaluation.class` 设置为 `Evaluator` 中定义的类 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在 [!DNL Data Science Workspace]，用户将能够在实验页面的“评估量度”选项卡中查看见解。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前，还没有针对以下项的默认评估指标 [!DNL Python] 或 [!DNL Tensorflow]. 因此，要获得以下项的评估指标 [!DNL Python] 或 [!DNL Tensorflow]，您需要创建一个自定义评估指标。 这可以通过实施 `Evaluator` 类。

#### 自定义评估指标 [!DNL Python]

对于自定义评估量度，需要为评估器实施以下两种主要方法： `split()` 和 `evaluate()`.

对象 [!DNL Python]，这些方法将定义在 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 对于 `Evaluator` 类。 请遵循 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 链接中的示例 `Evaluator`.

在中创建评估指标 [!DNL Python] 要求用户实施 `evaluate()` 和 `split()` 方法。

此 `evaluate()` 方法返回指标对象，该指标对象包含指标对象的数组，其属性为 `name`， `value`、和 `valueType`.

目的 `split()` 方法是输入数据，输出训练数据集和测试数据集。 在我们的示例中， `split()` 方法输入数据时，使用 `DataSetReader` SDK，然后通过删除不相关的列来清理数据。 从那里，使用数据中的现有原始功能创建其他功能。

此 `split()` 方法应返回训练和测试数据流，然后由使用 `pipeline()` 用于训练和测试ML模型的方法。

#### Tensorflow的自定义评估指标

对象 [!DNL Tensorflow]，类似于 [!DNL Python]，方法 `evaluate()` 和 `split()` 在 `Evaluator` 类需要实现。 对象 `evaluate()`，则返回的量度应为 `split()` 返回训练数据集和测试数据集。

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

截至目前，R没有默认的评估指标。因此，要获得R的评估指标，您需要定义 `applicationEvaluator` 分类作为配方的一部分。

#### R的自定义评估指标

的主要目的 `applicationEvaluator` 是返回包含量度键值对的JSON对象。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 可用作示例。 在此示例中， `applicationEvaluator` 分为三个常见部分：
- 加载数据
- 数据准备/功能工程
- 检索已保存的模型并评估

数据首先从源加载到数据集，如中所定义 [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). 从那里，数据被清理和工程化以适合机器学习模型。 最后，利用该模型对数据集进行预测，根据预测值和实际值计算指标。 在这种情况下，MAPE、MAE和RMSE定义并返回 `metrics` 对象。

## 使用预建量度和可视化图表

此 [!DNL Sensei Model Insights Framework] 将为每种类型的机器学习算法支持一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估指标和可视化图表。

| ML算法类型 | 评估指标 | 可视化图表 |
| --- | --- | --- |
| 回归 | - RMSE<br>- MAPI<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二进制分类 |  — 混淆矩阵<br> — 精确回调<br> — 准确性<br>- F分数（尤其是F1、F2）<br>- AUC<br>- ROC | ROC曲线和混淆矩阵 |
| 多类分类 |  — 混淆矩阵 <br> — 对于每个类： <br> — 查准率 <br>- F分数（尤其是F1、F2） | ROC曲线和混淆矩阵 |
| 聚类（包含基本事实） | - NMI（归一化互信息分数）、AMI（调整后的互信息分数）<br>- RI（兰德指数）、ARI（调整后兰德指数）<br> — 同质性分数、完整性分数和V-measure<br>- FMI（Fowlkes-Mallows指数）<br> — 纯度<br>- Jaccard索引 | 簇图显示簇和反映簇内数据点的相对簇大小的质心 |
| 群集（不含地面真实值） |  — 惯性<br> — 侧面影像系数<br>- CHI （Calinski-Harabaz指数）<br>- DBI（Davies-Bouldin索引）<br>- Dunn索引 | 簇图显示簇和反映簇内数据点的相对簇大小的质心 |
| 推荐 |  — 平均平均精度(MAP) <br> — 标准化折现累积收益 <br> — 平均倒数排名 <br> — 量度K | 待定 |
| TensorFlow用例 | 张量流模型分析(TFMA) | 深度比较神经网络模型比较/可视化 |
| 其他/错误捕获机制 | 模型作者定义的自定义量度逻辑（以及相应的评估图表）。 在模板不匹配的情况下正常处理错误 | 具有评估量度的键值对的表 |
