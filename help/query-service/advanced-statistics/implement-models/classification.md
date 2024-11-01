---
title: 分类算法
description: 了解如何使用关键参数、描述和示例代码配置和优化各种分类算法，以帮助您实施高级统计模型。
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 3%

---

# 分类算法 {#classification-algorithms}

本文档概述了各种分类算法，重点介绍了它们的配置、关键参数以及在高级统计模型中的实际使用。 分类算法用于根据输入特征向数据点分配类别。 每个部分都包含参数描述和示例代码，可帮助您为决策树、随机林和朴素贝叶斯分类等任务实施和优化这些算法。

## [!DNL Decision Tree Classifier] {#decision-tree-classifier}

[!DNL Decision Tree Classifier]是一种用于统计信息、数据挖掘和机器学习的监督学习方法。 该方法使用决策树作为分类任务的预测模型，从一组观测值中得出结论。

**参数**

下表概述了用于配置和优化[!DNL Decision Tree Classifier]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------|
| `MAX_BINS` | 最大桶数确定如何将连续特征划分为离散间隔。 这会影响特征在每个决策树节点上的分割方式。 更多的二进制文件提供了更高的粒度。 | 32 | 必须至少为2，并且至少等于任何分类特征中的类别数。 |
| `CACHE_NODE_IDS` | 如果`false`，则算法将树传递到执行器以将实例与节点进行匹配。 如果`true`，则算法会缓存每个实例的节点ID，从而加快深度树的训练。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 例如，`10`表示每10次迭代就检查一次缓存。 | 10 | (>= 1) |
| `IMPURITY` | 用于信息增益计算的标准（区分大小写）。 | “基尼” | `entropy`、`gini` |
| `MAX_DEPTH` | 树的最大深度（非负值）。 例如，深度`0`表示一个叶节点，深度`1`表示一个内部节点和2个叶节点。 | 5 | [0， 30] |
| `MIN_INFO_GAIN` | 在树节点上考虑拆分所需的最小信息增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 拆分后每个子项必须具有的加权样本数的最小分数。 如果拆分导致每个子代中总重量的分数小于此值，则放弃拆分。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 拆分后每个子级必须具有的最小实例数。 如果拆分产生的实例数少于此值，则拆分会被放弃。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 分配给直方图聚合的最大内存（以MB为单位）。 如果此值太小，则每个迭代只拆分1个节点，并且其聚合可能会超过此大小。 | 256 |                    |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `SEED` | 随机种子。 | 未设置 | 任何64位数字 |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任意字符串 |
| `ONE_VS_REST` | 启用或禁用使用One-vs-Rest包装此算法，用于多类分类问题。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'decision_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Factorization Machine Classifier] {#factorization-machine-classifier}

[!DNL Factorization Machine Classifier]是一个支持普通梯度下降和AdamW求解器的分类算法。 因子化机分类模型使用Logistic损失，该损失可通过梯度下降来优化，并且通常包含正则化项（如L2）以防止过拟合。

**参数**

下表概述了用于配置和优化[!DNL Factorization Machine Classifier]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------------------------------------|
| `TOL` | 收敛公差，控制优化精度。 | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | 因子的维数。 | 8 | (>= 0) |
| `FIT_INTERCEPT` | 指定是否适合截取项。 | `true` | `true`、`false` |
| `FIT_LINEAR` | 指定是否适合线性项（也称为单向项）。 | `true` | `true`、`false` |
| `INIT_STD` | 初始化系数的标准偏差。 | 0.01 | (>= 0) |
| `MAX_ITER` | 算法运行的最大迭代次数。 | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | 在训练期间用于小批次的数据部分。 必须在`(0, 1]`范围内。 | 1.0 | `(0, 1]` |
| `REG_PARAM` | 正则化参数有助于控制模型的复杂性和防止过拟合。 | 0.0 | (>= 0) |
| `SEED` | 算法中用于控制随机进程的随机种子。 | 未设置 | 任何64位数字 |
| `SOLVER` | 用于优化的求解器算法。 支持的选项为`gd`（梯度下降）和`adamW`。 | “adamW” | `gd`、`adamW` |
| `STEP_SIZE` | 优化的初始步长，通常解释为学习率。 | 1.0 | > 0 |
| `PROBABILITY_COL` | 预测类条件概率的列名称。 注意：并非所有模型都会输出经过良好校准的概率；应将这些概率视为置信度分数，而不是确切概率。 | “概率” | 任意字符串 |
| `PREDICTION_COL` | 预测类标签的列名称。 | “预测” | 任意字符串 |
| `RAW_PREDICTION_COL` | 原始预测值的列名称（也称为置信度）。 | &quot;rawPrediction&quot; | 任意字符串 |
| `ONE_VS_REST` | 指定是否为多类分类启用One-vs-Rest。 | FALSE | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree Classifier] {#gradient-boosted-tree-classifier}

[!DNL Gradient Boosted Tree Classifier]使用决策树集合来提高分类任务的准确性，组合多个树以增强模型性能。

**参数**

下表概述了用于配置和优化[!DNL Gradient Boosted Tree Classifier]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 最大桶数确定如何将连续特征划分为离散间隔。 这会影响特征在每个决策树节点上的分割方式。 更多的二进制文件提供了更高的粒度。 | 32 | 必须至少为2，并且等于或大于任何分类特征中的类别数。 |
| `CACHE_NODE_IDS` | 如果`false`，则算法将树传递到执行器以将实例与节点进行匹配。 如果`true`，则算法会缓存每个实例的节点ID，从而加快深度树的训练。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 例如，`10`表示每10次迭代就检查一次缓存。 | 10 | (>= 1) |
| `MAX_DEPTH` | 树的最大深度（非负值）。 例如，深度`0`表示一个叶节点，深度`1`表示一个内部节点和2个叶节点。 | 5 | (>= 0) |
| `MIN_INFO_GAIN` | 在树节点上考虑拆分所需的最小信息增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 拆分后每个子项必须具有的加权样本数的最小分数。 如果拆分导致每个子代中总重量的分数小于此值，则放弃拆分。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 拆分后每个子级必须具有的最小实例数。 如果拆分产生的实例数少于此值，则拆分会被放弃。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 分配给直方图聚合的最大内存（以MB为单位）。 如果此值太小，则每个迭代只拆分1个节点，并且其聚合可能会超过此大小。 | 256 |                                                                                                      |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `VALIDATION_INDICATOR_COL` | 列名称指示每一行是用于训练还是用于验证。 `false`用于培训，`true`用于验证。 | 未设置 | 任意字符串 |
| `RAW_PREDICTION_COL` | 原始预测值的列名称（也称为置信度）。 | &quot;rawPrediction&quot; | 任意字符串 |
| `LEAF_COL` | 通过预排序遍历生成的叶索引的列名，即每个树中每个实例的预测叶索引。 | “” | 任意字符串 |
| `FEATURE_SUBSET_STRATEGY` | 每个树节点中考虑进行拆分的特征数。 支持的选项： `auto`、`all`、`onethird`、`sqrt`、`log2`和`n`（部分功能）。 | &quot;auto&quot; | `auto`，`all`，`onethird`，`sqrt`，`log2`，`n` （其中`n`是介于0和1.0之间的小数） |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 |                                                                                                      |
| `LOSS_TYPE` | [!DNL Gradient Boosted Tree]模型尝试最小化的损失函数。 支持的选项： `logistic`。 | “物流” | `logistic` |
| `STEP_SIZE` | `(0, 1]`范围内的步长大小（也称为学习率），用于缩小每个估算器的贡献。 | 0.1 | `(0, 1]` |
| `MAX_ITER` | 算法的最大迭代次数。 | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | 用于训练每个决策树的训练数据的小数，在`(0, 1]`范围内。 | 1.0 | `(0, 1]` |
| `PROBABILITY_COL` | 预测类条件概率的列名称。 注意：并非所有模型都会输出经过良好校准的概率；应将这些概率视为置信度分数，而不是确切概率。 | “概率” | 任意字符串 |
| `ONE_VS_REST` | 为多类分类启用或禁用使用One-vs-Rest包装此算法。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Linear Support Vector Classifier] （线性SVC） {#linear-support-vector-classifier}

[!DNL Linear Support Vector Classifier] (LinearSVC)构造一个超平面以分类高维空间中的数据。 您可以使用它来最大化类之间的边距，以最大限度地减少分类错误。

**参数**

下表概述了用于配置和优化[!DNL Linear Support Vector Classifier (LinearSVC)]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_ITER` | 算法运行的最大迭代次数。 | 100 | (>= 0) |
| `AGGREGATION_DEPTH` | 树聚合的建议深度。 | 2 |                                                                                                      |
| `FIT_INTERCEPT` | 是否适合截取条件。 | `true` | `true`、`false` |
| `TOL` | 优化的收敛公差。 | 1E-6 | (>= 0) |
| `MAX_BLOCK_SIZE_IN_MB` | 用于将输入数据栈叠到块中的最大内存（以MB为单位）。 将数据栈叠在分区内，如果分区中的剩余数据大小较小，则相应地调整该值。 | 0.0 | (>= 0) |
| `REG_PARAM` | 正则化参数有助于控制模型的复杂性和防止过拟合。 | 0.0 | (>= 0) |
| `STANDARDIZATION` | 是否在拟合模型之前标准化训练特征。 | `true` | `true`、`false` |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `RAW_PREDICTION_COL` | 原始预测值的列名称（也称为置信度）。 | &quot;rawPrediction&quot; | 任意字符串 |
| `ONE_VS_REST` | 为多类分类启用或禁用使用One-vs-Rest包装此算法。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'linear_svc_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Logistic Regression] {#logistic-regression}

[!DNL Logistic Regression]是用于二进制分类的监督算法。 它使用Logistic函数对实例属于某个类的概率进行建模，使其适用于目标为将实例分类为两个类别之一的任务。

**参数**

下表概述了用于配置和优化[!DNL Logistic Regression]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| `MAX_ITER` | 算法运行的最大迭代次数。 | 100 | (>= 0) |
| `REGPARAM` | 利用正则化参数控制模型的复杂性。 | 0.0 | (>= 0) |
| `ELASTICNETPARAM` | `ElasticNet`混合参数控制L1 （套索）和L2 （凸纹）处罚之间的平衡。 值为0会应用L2惩罚（Ridge，用于减小系数的大小），值为1会应用L1惩罚（Lasso，通过将某些系数设置为零来鼓励稀疏性）。 | 0.0 | (>= 0， &lt;= 1) |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'logistic_reg'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Multilayer Perceptron Classifier] {#multilayer-perceptron-classifier}

[!DNL Multilayer Perceptron Classifier]是一个前向神经网络分类器，由多个完全连通的节点层组成。 层中的每个节点使用输入数据的加权线性组合将输入映射到输出，具有节点权重(`w`)和偏差(`b`)，然后是激活函数。 此过程有助于通过调整关键参数来配置和优化高级统计模型，并提供代码示例以作进一步指导。—>

**参数**

| 参数 | 描述 | 默认值 | 可能值 |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | 算法运行的最大迭代次数。 | 100 | (>= 0) |
| `BLOCK_SIZE` | 用于在分区内的矩阵中栈叠输入数据的块大小。 如果块大小超过分区中的剩余数据，则相应地调整块大小。 | 128 | (>= 0) |
| `STEP_SIZE` | 用于每个优化迭代的步长（仅适用于求解器`gd`）。 | 0.03 | (> 0) |
| `TOL` | 优化的收敛公差。 | `1E-6` | (>= 0) |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `SEED` | 算法中用于控制随机进程的随机种子。 | 未设置 | 任何64位数字 |
| `PROBABILITY_COL` | 预测类条件概率的列名称。 这些应被视为置信度分数，而不是确切概率。 | “概率” | 任意字符串 |
| `RAW_PREDICTION_COL` | 原始预测值的列名称（也称为置信度）。 | &quot;rawPrediction&quot; | 任意字符串 |
| `ONE_VS_REST` | 为多类分类启用或禁用使用One-vs-Rest包装此算法。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'multilayer_perceptron_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Naive Bayes Classifier] {#naive-bayes-classifier}

[!DNL Naive Bayes Classifier]是一个简单的概率多类分类器，它基于Bayes定理，特征间具有强（朴素）独立性假设。 该方法训练效率高，只需对训练数据进行一次遍历，即可计算每个特征给定每个标签的条件概率分布。 对于预测，它使用Bayes定理来计算给定观测值的每个标签的条件概率分布。

**参数**

| 参数 | 描述 | 默认值 | 可能值 |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MODEL_TYPE` | 指定模型类型。 支持的选项为`"multinomial"`、`"complement"`、`"bernoulli"`和`"gaussian"`。 模型类型区分大小写。 | &quot;多项式&quot; | `"multinomial"`、`"complement"`、`"bernoulli"`、`"gaussian"` |
| `SMOOTHING` | 平滑参数，用于平滑分类数据和处理不可见特征。 | 1.0 | (>= 0) |
| `PROBABILITY_COL` | 预测类条件概率的列名称。 这些应被视为置信度分数，而不是确切概率。 | “概率” | 任意字符串 |
| `WEIGHT_COL` | 实例权重的列名称。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任意字符串 |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `RAW_PREDICTION_COL` | 原始预测值的列名称（也称为置信度）。 | &quot;rawPrediction&quot; | 任意字符串 |
| `ONE_VS_REST` | 指定是否为多类分类启用One-vs-Rest。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'naive_bayes_classifier'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Classifier] {#random-forest-classifier}

[!DNL Random Forest Classifier]是一种集成学习算法，用于在训练期间构建多个决策树。 它通过平均预测和选择大多数树为分类任务选择的类别来缓解过度拟合。

**参数**

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 最大桶数确定如何将连续特征划分为离散间隔。 这会影响特征在每个决策树节点上的分割方式。 更多的二进制文件提供了更高的粒度。 | 32 | 必须至少为2，并且等于或大于任何分类特征中的类别数。 |
| `CACHE_NODE_IDS` | 如果`false`，则算法将树传递到执行器以将实例与节点进行匹配。 如果为`true`，则算法将缓存每个实例的节点ID，从而加快训练速度。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 例如，`10`表示每10次迭代就检查一次缓存。 | 10 | (>= 1) |
| `IMPURITY` | 用于信息增益计算的标准（区分大小写）。 | “基尼” | `entropy`、`gini` |
| `MAX_DEPTH` | 树的最大深度（非负值）。 例如，深度`0`表示一个叶节点，深度`1`表示一个内部节点和2个叶节点。 | 5 | (>= 0) |
| `MIN_INFO_GAIN` | 在树节点上考虑拆分所需的最小信息增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 拆分后每个子项必须具有的加权样本数的最小分数。 如果拆分导致每个子代中总重量的分数小于此值，则放弃拆分。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 拆分后每个子级必须具有的最小实例数。 如果拆分产生的实例数少于此值，则拆分会被放弃。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 分配给直方图聚合的最大内存（以MB为单位）。 如果此值太小，则每个迭代只拆分1个节点，并且其聚合可能会超过此大小。 | 256 | (>= 1) |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任意字符串 |
| `SEED` | 算法中用于控制随机进程的随机种子。 | -1689246527 | 任何64位数字 |
| `BOOTSTRAP` | 构建树时是否使用引导示例。 | `true` | `true`、`false` |
| `NUM_TREES` | 要训练的树的数量。 如果`1`，则不使用引导。 如果大于`1`，则应用引导。 | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | 用于学习每个决策树的训练数据部分。 | 1.0 | (> 0， &lt;= 1) |
| `LEAF_COL` | 叶索引的列名，按预排序包含每个树中每个实例的预测叶索引。 | “” | 任意字符串 |
| `PROBABILITY_COL` | 预测类条件概率的列名称。 这些应被视为置信度分数，而不是确切概率。 | “概率” | 任意字符串 |
| `RAW_PREDICTION_COL` | 原始预测值的列名称（也称为置信度）。 | &quot;rawPrediction&quot; | 任意字符串 |
| `ONE_VS_REST` | 指定是否为多类分类启用One-vs-Rest。 | `false` | `true`、`false` |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'random_forest_classifier'
) AS
  select col1, col2, col3 from training-dataset
```

## 后续步骤

阅读本文档后，您现在知道如何配置和使用各种分类算法。 接下来，请参阅有关[回归](./regression.md)和[群集](./clustering.md)的文档，了解其他类型的高级统计模型。

