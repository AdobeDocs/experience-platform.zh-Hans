---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: 优化模型
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 优化模型


本教程将重点介绍：

- 配置菜谱代码
- 定义自定义指标
- 使用预建的评估指标和可视化图表

在本教程结束时，您应该能够配置菜谱代码、定义自定义指标、使用预建的评估指标和默认可视化图表。

## 什么是指标？

在实施和培训模型之后，数据科学家下一步要做的就是找出模型的性能。 使用各种指标来确定模型与其他模型相比的效果。 使用的一些指标示例包括：
- 分类准确性
- 曲线下的区域
- 混淆矩阵
- 分类报告

## 什么是模型洞察框架？

模型洞察框架为数据科学家提供了数据科学工作区中的工具，以便根据实验快速、明智地选择最佳机器学习模型。 该框架将提高机器学习工作流程的速度和效率，并改进数据科学家的易用性。 这是通过为每个机器学习算法类型提供一个默认模板来辅助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为他们的最终客户做出更好的模型优化决策。

## 配置菜谱代码

目前，Model Insights Framework支持以下运行时：
- [斯卡拉](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

菜谱的示例代码位于 [experience-platform-dsw-reference存储库](https://github.com/adobe/experience-platform-dsw-reference) ，位于 `recipes`。 本教程中将引用此存储库中的特定文件。

### 斯卡拉 {#scala}

有两种方法可将指标引入方法。 一种是使用SDK提供的默认评估指标，另一种是编写自定义评估指标。

#### Scala的默认评估指标

默认评估作为分类算法的一部分进行计算。 以下是当前实现的求值器的一些默认值：

| 求值器类 | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

可以在菜谱中的文件夹中的 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 文件中定义计算 `recipe` 器。 启用该功能的示 `DefaultBinaryClassificationEvaluator` 例代码如下：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用评估器类后，默认情况下，在培训期间将计算许多度量。 可通过向您添加以下行来显式声明默认量度 `application.properties`。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE] 如果未定义度量，则默认度量将处于活动状态。

可通过更改的值来启用特定度量 `evaluation.metrics.com`。 在以下示例中，启用了F-Score量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每个类的默认度量。 用户还可以使用列中的值 `evaluation.metric` 来启用特定度量。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | 接收机 <br>工作特 <br>性下的精度——召回——混淆矩阵-F- <br>得分——精 <br>度——接收机工作特 <br><br>性区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | 接收机 <br>工作特 <br>性下的精度——召回——混淆矩阵-F- <br>得分——精 <br>度——接收机工作特 <br><br>性区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -平均精度(MAP) <br>-归一化积分——平均 <br>倒数秩- <br>度量K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定义评估指标

可通过扩展文件中的界面来提供自定 `MLEvaluator.scala` 义求值 `Evaluator.scala` 器。 在示例 [Evaluator.scala文件中](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) ，我们定义自定义 `split()` 和函 `evaluate()` 数。 我们 `split()` 的函数以8:2的比率随机拆分我们的数据，而我们的函数定 `evaluate()` 义并返回3个度量：MAPE、MAE和RMSE。

>[!IMPORTANT] 对于类， `MLMetric` 请勿在创建新 `"measures"` 的 `valueType` 其他时使用，该 `MLMetric` 度量不会填充自定义评估度量表中。
>  
> 执行以下操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是这样： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


在菜谱中定义后，下一步是在菜谱中启用它。 这是在项目文 [件夹中的application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 文件中完成的 `resources` 。 此处， `evaluation.class``Evaluator` 将其设置为在 `Evaluator.scala`

```properties
evaluation.class=com.adobe.platform.ml.Evaluator
```

在数据科学工作区中，用户将能够在实验页面的“评估指标”选项卡中查看洞察。

### Python/Tensorflow {#pythontensorflow}

到目前为止，还没有Python或Tensorflow的默认评估指标。 因此，要获得Python或Tensorflow的评估指标，您需要创建自定义的评估指标。 这可以通过实现类来完 `Evaluator` 成。

#### Python的自定义评估指标

对于自定义评估指标，需要为评估器实现两种主要方法： `split()` 和 `evaluate()`。

对于Python，这些方法将在类的 [evaluator.py中定义](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py)`Evaluator` 。 有关 [示例，请按照](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) evaluator.py链接进行操作 `Evaluator`。

在Python中创建评估指标需要用户实施 `evaluate()` 和方 `split()` 法。

该方 `evaluate()` 法返回度量对象，该对象包含属性为、和的度量对 `name`象 `value`的数组 `valueType`。

该方法的目 `split()` 的是输入数据并输出训练和测试数据集。 在我们的示例中，该方 `split()` 法使用 `DataSetReader` SDK输入数据，然后通过删除不相关的列来清理数据。 从此处，将根据数据中的现有原始功能创建其他功能。

该 `split()` 方法应返回训练和测试数据帧，然后由训练和测 `pipeline()` 试数据帧来训练和测试ML模型。

#### Tensorflow的自定义评估指标

对于Tensorflow，与Python类似，需 `evaluate()` 要实 `split()` 现方 `Evaluator` 法和类中的方法。 对 `evaluate()`于，在返回培训和测试数据集 `split()` 时应返回度量。

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

目前，R没有默认的评估指标。因此，要获得R的评估指标，您需要将类定义 `applicationEvaluator` 为菜谱的一部分。

#### R的自定义评估指标

其主要用途 `applicationEvaluator` 是返回包含关键值对的度量的JSON对象。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 可用作示例。 在此示例中，将 `applicationEvaluator` 分为三个熟悉的部分：
- 加载数据
- 数据准备／功能工程
- 检索保存的模型并评估

数据首先从 [retail.config.json中定义的源加载到数据集](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)。 从那里，数据被清理并设计为适合机器学习模型。 最后，利用数据集进行预测，并根据预测值和实际值计算度量。 在这种情况下，在对象中定义并返回MAPE、MAE和RMSE `metrics` 。

## 使用预建指标和可视化图表

Sensei模型分析框架将支持每种机器学习算法的一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估指标和可视化。

| ML算法类型 | 评估指标 | 可视化图表 |
--- | --- | ---
| 回归 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二进制分类 | -混淆矩阵<br>-精确召回<br>-准确性<br>- F-得分（特别是F1,F2）<br>- AUC<br>- ROC | ROC曲线与混淆矩阵 |
| 多类分类 | -混淆矩阵 <br>-对于每个类：精 <br>度——召回精 <br>度- F得分（具体为F1、F2） | ROC曲线与混淆矩阵 |
| 聚类（含地面真度） | - NMI（归一化互信息得分）、AMI（经调整的互信息得分）<br>- RI（Rand指数）、ARI（经调整的Rand指数）<br>-同质性得分、完整性得分和V-measure<br>- FMI(V-measure<br>- Mallows指数)<br>- Preprity- Jacard指数 | 簇图显示簇和中心，簇大小反映掉在簇内的数据点 |
| 聚类（无地面真度） | -惯性<br>-侧影系数<br>- CHI（Calinski-Harabaz指数）<br>- DBI（Davies-Bouldin指数）<br>- Dunn指数 | 簇图显示簇和中心，簇大小反映掉在簇内的数据点 |
| 推荐 | -平均精度(MAP) <br>-归一化积分——平均 <br>倒数秩- <br>度量K | TBD |
| TensorFlow用例 | 张量流模型分析(TFMA) | 深度比较神经网络模型比较／可视化 |
| 其他／错误捕获机制 | 由模型作者定义的自定义度量逻辑（和相应的评估图表）。 模板不匹配时的正常错误处理 | 具有关键值对的表，用于评估指标 |
