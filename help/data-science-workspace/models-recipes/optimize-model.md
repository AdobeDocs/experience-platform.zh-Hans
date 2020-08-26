---
keywords: Experience Platform;optimize;model;Data Science Workspace;popular topics
solution: Experience Platform
title: 优化模型
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 0%

---


# 使用模型洞察框架优化模型

模型洞察框架为数据科学家提供了各种工具， [!DNL Data Science Workspace] 以便快速、明智地选择基于实验的最优机器学习模型。 该框架将提高机器学习工作流程的速度和效率，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供一个默认模板来辅助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为最终客户做出更好的模型优化决策。

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

菜谱的示例代码位于 [experience-platform-dsw-reference存储库](https://github.com/adobe/experience-platform-dsw-reference) 的 `recipes`。 本教程将引用此存储库中的特定文件。

### 斯卡拉 {#scala}

有两种方法可将指标引入菜谱。 一种是使用SDK提供的默认评估指标，另一种是编写自定义评估指标。

#### Scala的默认评估指标

默认评估作为分类算法的一部分进行计算。 以下是当前实现的计算器的一些默认值：

| 计算器类 | `evaluation.class` |
--- | ---
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

计算器可以在文件夹中application. [properties文件的菜谱](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 中定义 `recipe` 计算器。 启用该功能的示 `DefaultBinaryClassificationEvaluator` 例代码如下：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用评估器类后，默认情况下，在培训期间将计算许多度量。 可通过向您添加以下行来显式声明默认量 `application.properties`度。

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定义度量，则默认度量将处于活动状态。

可通过更改的值来启用特定度量 `evaluation.metrics.com`。 在以下示例中，启用了F-Score量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表列出了每个类的默认度量。 用户还可以使用列中的 `evaluation.metric` 值来启用特定度量。

| `evaluator.class` | 默认量度 | `evaluation.metric` |
--- | --- | ---
| `DefaultBinaryClassificationEvaluator` | 接收机 <br>工作特 <br>性下的——精度——召回- <br>混淆矩阵-F- <br>得分——精度- <br>接收机工作特 <br>性区域——精确——召回——混淆矩阵 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` | 接收机 <br>工作特 <br>性下的——精度——召回- <br>混淆矩阵-F- <br>得分——精度- <br>接收机工作特 <br>性区域——精确——召回——混淆矩阵 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` | -平均精度(MAP)- <br>归一化积分——平均 <br>倒数秩- <br>度量K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定义评估指标

可通过扩展文件中的接口来提供自 `MLEvaluator.scala` 定义计 `Evaluator.scala` 算器。 在示例Evaluator [.scala文件中](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) ，我们定义自 `split()` 定义和 `evaluate()` 函数。 我们 `split()` 的函数以8:2的比率随机拆分我们的数据，我们的函数 `evaluate()` 定义并返回3个度量：MAPE、MAE和RMSE。

>[!IMPORTANT]
>
>对于类 `MLMetric` ，创建新 `"measures"` 度量 `valueType` 时不要使用，否则 `MLMetric` 该度量不会填充到自定义评估度量表中。
>  
> 执行以下操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


在菜谱中定义后，下一步是在菜谱中启用它。 这是在项目文 [件夹中](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) application.properties文件中完 `resources` 成的。 此处 `evaluation.class` 设置为中定 `Evaluator` 义的类 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在中， [!DNL Data Science Workspace]用户将能够在实验页面的“评估指标”选项卡中查看洞察。

### [!DNL Python/Tensorflow] {#pythontensorflow}

到目前为止，没有或的默认评估 [!DNL Python] 指标 [!DNL Tensorflow]。 因此，要获得或的评估 [!DNL Python] 指标， [!DNL Tensorflow]您需要创建自定义的评估指标。 这可以通过实现类来 `Evaluator` 实现。

#### 自定义评估指标 [!DNL Python]

对于自定义评估指标，需要为评估器实现两种主要方法： `split()` 和 `evaluate()`。

对 [!DNL Python]于，这些方法将在类 [的evaluator](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) .py中定 `Evaluator` 义。 请按照 [evaluator](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) .py链接查看示例 `Evaluator`。

在中创建评 [!DNL Python] 估指标需要用户实施 `evaluate()` 和 `split()` 方法。

该方 `evaluate()` 法返回包含属性为、和的度量对象数组 `name`的度 `value`量对象 `valueType`。

该方法的目 `split()` 的是输入数据并输出训练和测试数据集。 在我们的示例中，该 `split()` 方法使用SDK输入 `DataSetReader` 数据，然后通过删除不相关列来清除数据。 从此处，数据中的现有原始功能将创建更多功能。

该 `split()` 方法应返回训练和测试数据帧，然后用 `pipeline()` 于训练和测试ML模型。

#### Tensorflow的自定义评估指标

因 [!DNL Tensorflow]为，类 [!DNL Python]似地，需要实 `evaluate()` 现方 `split()` 法和类 `Evaluator` 中的方法。 例 `evaluate()`如，在返回培训和测试 `split()` 数据集时应返回度量。

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

其主要目的 `applicationEvaluator` 是返回一个JSON对象，其中包含关键值对的度量。

此 [applicationEvaluator](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) .R可用作示例。 在本例中，将 `applicationEvaluator` 分为三个熟悉的部分：
- 加载数据
- 数据准备／功能工程
- 检索保存的模型并评估

数据首先从retail.config.json中定义的源 [加载到数据集](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json)。 从此处，数据被清理并设计为适合机器学习模型。 最后，利用数据集进行预测，并根据预测值和实际值计算指标。 在这种情况下，在对象中定义并返回MAPE、MAE和 `metrics` RMSE。

## 使用预建指标和可视化图表

该模 [!DNL Sensei Model Insights Framework] 板将支持每种机器学习算法的一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估指标和可视化。

| ML算法类型 | 评估指标 | 可视化图表 |
--- | --- | ---
| 回归 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二进制分类 | -混淆矩阵<br>-精确召回<br>-准确性<br>- F-得分（特别是F1,F2）<br>- AUC<br>- ROC | ROC曲线与混淆矩阵 |
| 多类分类 | -混淆矩 <br>阵——对于每个类： <br>-精确调查准 <br>确性- F得分（特别是F1、F2） | ROC曲线与混淆矩阵 |
| 聚类（含地面真度） | - NMI（标准化互信息得分）、AMI（调整互信息得分）<br>- RI（Rand指数）、ARI（调整后兰德指数）<br>-同质性得分、完整性得分和V-measure<br>- FMI（Fowlkes-Mallows指数）<br>- Preciety<br>- Jacard指数 | 具有相对簇大小的簇和中心线的簇图反映位于簇内的数据点 |
| 聚类（无地面真度） | -惯性<br>-侧面影像系数<br>- CHI（Calinski-Harabaz指数）<br>- DBI（Davies-Bouldin指数）<br>- Dunnindex | 具有相对簇大小的簇和中心线的簇图反映位于簇内的数据点 |
| 推荐 | -平均精度(MAP)- <br>归一化积分——平均 <br>倒数秩- <br>度量K | TBD |
| TensorFlow用例 | 张量流模型分析(TFMA) | 深度比较神经网络模型比较／可视化 |
| 其他／错误捕获机制 | 由模型作者定义的自定义度量逻辑（和相应的评估图表）。 模板不匹配时的适当错误处理 | 具有评估指标的键值对的表 |
