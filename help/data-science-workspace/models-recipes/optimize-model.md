---
keywords: Experience Platform；优化；模型；数据科学工作区；热门主题；模型分析
solution: Experience Platform
title: 使用模型分析框架优化模型
type: Tutorial
description: 模型分析框架在数据科学工作区中为数据科学家提供了各种工具，以便快速、明智地选择基于实验的最佳机器学习模型。
exl-id: f989a3f1-6322-47c6-b7d6-6a828766053f
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 使用模型分析框架优化模型

模型分析框架为数据科学家提供了 [!DNL Data Science Workspace] 在实验的基础上，快速、灵活地选择最优的机器学习模型。 该框架将提高机器学习工作流的速度和有效性，并提高数据科学家的易用性。 这是通过为每个机器学习算法类型提供默认模板来协助模型调整来完成的。 最终结果使数据科学家和公民数据科学家能够为其最终客户做出更好的模型优化决策。

## 什么是量度？

在实施和训练模型之后，数据科学家下一步要做的就是找到模型的性能。 可使用各种量度来查找与其他量度相比，模型的效果如何。 使用的量度示例包括：
- 分类准确性
- 曲线下的区域
- 混淆矩阵
- 分类报表

## 配置方法代码

目前，模型分析框架支持以下运行时：
- [斯卡拉](#scala)
- [Python/Tensorflow](#pythontensorflow)
- [R](#r)

方法的示例代码可在 [experience-platform-dsw-reference](https://github.com/adobe/experience-platform-dsw-reference) 存储库 `recipes`. 在本教程中将引用此存储库中的特定文件。

### 斯卡拉 {#scala}

可通过两种方式将量度引入方法。 一种是使用SDK提供的默认评估量度，另一种是编写自定义评估量度。

#### Scala的默认评估量度

默认评估将作为分类算法的一部分进行计算。 以下是当前实施的计算器的一些默认值：

| 计算器类 | `evaluation.class` |
|--- | ---|
| DefaultBinaryClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator` |
| DefaultMultiClassificationEvaluator | `com.adobe.platform.ml.impl.DefaultMultiClassificationEvaluator` |
| RecommendationsEvaluator | `com.adobe.platform.ml.impl.RecommendationsEvaluator` |

计算器可在的方法中定义 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 文件 `recipe` 文件夹。 启用 `DefaultBinaryClassificationEvaluator` 如下所示：

```scala
evaluation.class=com.adobe.platform.ml.impl.DefaultBinaryClassificationEvaluator
evaluation.labelColumn=label
evaluation.predictionColumn=prediction
training.evaluate=true
```

启用计算器类后，在培训期间会默认计算许多量度。 可通过将以下行添加到 `application.properties`.

```scala
evaluation.metrics.com=com.adobe.platform.ml.impl.Constants.DEFAULT
```

>[!NOTE]
>
>如果未定义量度，则默认量度将处于活动状态。

可通过更改 `evaluation.metrics.com`. 在以下示例中，启用了F分数量度。

```scala
evaluation.metrics=com.adobe.platform.ml.impl.Constants.FSCORE
```

下表说明了每个类的默认量度。 用户还可以在 `evaluation.metric` 列来启用特定量度。

| `evaluator.class` | 默认指标 | `evaluation.metric` |
| --- | --- | --- |
| `DefaultBinaryClassificationEvaluator` |  — 精度 <br> — 召回 <br> — 混淆矩阵 <br>-F分数 <br> — 准确度 <br>接收器操作特性 <br>接收器工作特性下的区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `DefaultMultiClassificationEvaluator` |  — 精度 <br> — 召回 <br> — 混淆矩阵 <br>-F分数 <br> — 准确度 <br>接收器操作特性 <br>接收器工作特性下的区域 | -`PRECISION` <br>-`RECALL` <br>-`CONFUSION_MATRIX` <br>-`FSCORE` <br>-`ACCURACY` <br>-`ROC` <br>-`AUROC` |
| `RecommendationsEvaluator` |  — 平均精度(MAP) <br> — 标准化折扣累计收益 <br> — 平均倒数排名 <br> — 量度K | -`MEAN_AVERAGE_PRECISION` <br>-`NDCG` <br>-`MRR` <br>-`METRIC_K` |


#### Scala的自定义评估量度

通过扩展的接口，可以提供自定义计算器 `MLEvaluator.scala` 在 `Evaluator.scala` 文件。 在示例中 [计算器.scala](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/scala/com/adobe/platform/ml/Evaluator.scala) 文件，我们定义自定义 `split()` 和 `evaluate()` 函数。 我们的 `split()` 函数会随机拆分我们的数据，其比率为8:2，而 `evaluate()` 函数定义并返回3个量度：MAPE， MAE和RMSE。

>[!IMPORTANT]
>
>对于 `MLMetric` 类，不使用 `"measures"` 表示 `valueType` 创建新 `MLMetric` 否则，自定义评估量度表中将不会填充该量度。
>  
> 执行此操作： `metrics.add(new MLMetric("MAPE", mape, "double"))`\
> 不是： `metrics.add(new MLMetric("MAPE", mape, "measures"))`


在方法中定义后，下一步是在方法中启用它。 此操作在 [application.properties](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/scala/src/main/resources/application.properties) 文件 `resources` 文件夹。 此处 `evaluation.class` 设置为 `Evaluator` 在 `Evaluator.scala`

```scala
evaluation.class=com.adobe.platform.ml.Evaluator
```

在 [!DNL Data Science Workspace]，则用户将能够在实验页面的“评估量度”选项卡中看到分析。

### [!DNL Python/Tensorflow] {#pythontensorflow}

截至目前， [!DNL Python] 或 [!DNL Tensorflow]. 因此，要获取 [!DNL Python] 或 [!DNL Tensorflow]，则需要创建自定义评估量度。 这可以通过实施 `Evaluator` 类。

#### 的自定义评估量度 [!DNL Python]

对于自定义评估量度，需要为评估器实施以下两种主要方法： `split()` 和 `evaluate()`.

对于 [!DNL Python]，这些方法将在 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 对于 `Evaluator` 类。 关注 [evaluator.py](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/python/retail/retail/evaluator.py) 链接，以查看 `Evaluator`.

在中创建评估量度 [!DNL Python] 需要用户实施 `evaluate()` 和 `split()` 方法。

的 `evaluate()` 方法返回包含属性为 `name`, `value`和 `valueType`.

的目的 `split()` 方法是输入数据并输出训练和测试数据集。 在本例中， `split()` 方法使用 `DataSetReader` SDK，然后通过删除不相关的列来清理数据。 从此处，将根据数据中的现有原始功能创建其他功能。

的 `split()` 方法应返回训练和测试数据帧，然后数据帧将被使用 `pipeline()` ML模型的训练和测试方法。

#### Tensorflow的自定义评估量度

对于 [!DNL Tensorflow]，类似于 [!DNL Python]，方法 `evaluate()` 和 `split()` 在 `Evaluator` 需要实施类。 对于 `evaluate()`，则应返回量度 `split()` 返回训练和测试数据集。

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

目前，R没有默认的评估量度。因此，要获取R的评估量度，您需要定义 `applicationEvaluator` 类。

#### R的自定义评估量度

的主要目的 `applicationEvaluator` 是返回包含量度键值对的JSON对象。

此 [applicationEvaluator.R](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/R/applicationEvaluator.R) 例子。 在本例中， `applicationEvaluator` 分为三个熟悉的部分：
- 加载数据
- 数据准备/特征工程
- 检索保存的模型并评估

数据首先从源加载到数据集(如 [retail.config.json](https://github.com/adobe/experience-platform-dsw-reference/blob/master/recipes/R/Retail%20-%20GradientBoosting/retail.config.json). 从那里，将清理并设计数据以适合机器学习模型。 最后，利用模型进行预测，根据预测值和实际值计算量度。 在这种情况下，定义MAPE、MAE和RMSE，并在 `metrics` 对象。

## 使用预建量度和可视化图表

的 [!DNL Sensei Model Insights Framework] 将为每种类型的机器学习算法支持一个默认模板。 下表显示了常见的高级机器学习算法类以及相应的评估量度和可视化图表。

| ML算法类型 | 评估量度 | 可视化图表 |
| --- | --- | --- |
| 回归 | - RMSE<br>- MAPE<br>- MASE<br>- MAE | 预测值与实际值叠加曲线 |
| 二进制分类 |  — 混淆矩阵<br>- Precision-recall<br> — 准确性<br>- F分数（特别是F1、F2）<br>- AUC<br> — 中华民国 | ROC曲线与混淆矩阵 |
| 多类分类 |  — 混淆矩阵 <br> — 对于每个类： <br> — 精度查全率 <br>- F分数（特别是F1、F2） | ROC曲线与混淆矩阵 |
| 聚类（含地面真值） | - NMI（标准化互信分数）、AMI（调整后互信分数）<br>- RI（兰德指数）、ARI（调整后兰德指数）<br> — 同质性分数、完整性分数和V度量<br>- FMI（福尔克斯 — 马洛斯指数）<br> — 纯度<br>- Jaccard索引 | 具有相对簇大小的簇和中心的簇图反映位于簇内的数据点 |
| 聚类（不含地面真值） |  — 惯性<br> — 侧面影像系数<br>- CHI（卡林斯基 — 哈拉巴斯指数）<br>- DBI（Davies-Bouldin指数）<br>- Dunnindex | 具有相对簇大小的簇和中心的簇图反映位于簇内的数据点 |
| 推荐 |  — 平均精度(MAP) <br> — 标准化折扣累计收益 <br> — 平均倒数排名 <br> — 量度K | 待定 |
| TensorFlow用例 | 张量流模型分析(TFMA) | 深度比较神经网络模型比较/可视化 |
| 其他/错误捕获机制 | 由模型作者定义的自定义量度逻辑（和相应的评估图）。 模板不匹配时的正常错误处理 | 包含评估量度键值对的表 |
