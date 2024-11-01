---
title: 回归算法
description: 了解如何使用关键参数、描述和示例代码配置和优化各种回归算法，以帮助您实施高级统计模型。
role: Developer
source-git-commit: b248e8f8420b617a117d36aabad615e5bbf66b58
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 4%

---

# 回归算法 {#regression-algorithms}

本文档概述了各种回归算法，重点介绍了它们的配置、关键参数以及在高级统计模型中的实际使用。 利用回归算法对因变量与自变量之间的关系进行建模，根据观测数据预测连续结果。 每个部分都包含参数描述和示例代码，以帮助您为诸如线性、随机林和生存回归等任务实施和优化这些算法。

## [!DNL Decision Tree]回归 {#decision-tree-regression}

[!DNL Decision Tree]学习是一种用于统计、数据挖掘和机器学习的监督学习方法。 该方法使用分类决策树或回归决策树作为预测模型，对一组观测值做出结论。

**参数**

下表概述了用于配置和优化决策树模型性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 最大桶数确定如何将连续特征划分为离散间隔。 这会影响特征在每个决策树节点上的分割方式。 更多的二进制文件提供了更高的粒度。 | 32 | 在任何分类特征中必须至少为2并且至少为类别数。 |
| `CACHE_NODE_IDS` | 如果`false`，则算法将树传递到执行器以将实例与节点进行匹配。 如果`true`，则算法将缓存每个实例的节点ID。 缓存可以加快对更深层树的训练。 | false | `true`或`false` |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 例如，`10`表示每10次迭代将检查一次缓存。 | 10 | (>=1) |
| `IMPURITY` | 用于信息增益计算的标准（区分大小写）。 | `gini` | `entropy`、`gini` |
| `MAX_DEPTH` | 树的最大深度（非负值）。 例如，深度`0`表示一个叶节点，深度`1`表示一个内部节点和2个叶节点。 | 5 | [0， 30] |
| `MIN_INFO_GAIN` | 在树节点上考虑拆分所需的最小信息增益。 | 0.0 | (>=0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 拆分后每个子项必须具有的加权样本数的最小分数。 如果拆分导致每个子代中总重量的分数小于此值，则放弃拆分。 | 0.0 | (>=0.0， 0.5) |
| `MIN_INSTANCES_PER_NODE` | 拆分后每个子级必须具有的最小实例数。 如果拆分产生的实例数少于此值，则拆分会被放弃。 | 1 | (>=1) |
| `MAX_MEMORY_IN_MB` | 分配给直方图聚合的最大内存（以MB为单位）。 如果内存太小，则每个迭代只拆分1个节点，这可能导致聚合超过大小。 | 256 |                                                                                                        |
| `PREDICTION_COL` | 预测列名称的参数。 | “预测” | 任意字符串 |
| `SEED` | 随机种子的参数。 | 不适用 | 任何64位数字 |
| `WEIGHT_COL` | 权重列名称的参数。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 |                                                                                                        |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'decision_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Factorization Machines]回归 {#factorization-machines-regression}

[!DNL Factorization Machines]是一个支持正常梯度下降和AdamW求解器的回归学习算法。 算法基于S. Rendle (2010)的论文“[!DNL Factorization Machines]”。

**参数**

下表概述了用于配置和优化[!DNL Factorization Machines]回归性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|------------------------|--------------------------------------------------------------------------------------|---------------|----------------|
| `TOL` | 收敛公差。 | `1E-6` | (>= 0) |
| `FACTOR_SIZE` | 因子的维数。 | 8 | (>= 0) |
| `FIT_INTERCEPT` | 是否适合截取条件。 | `true` | `true`、`false` |
| `FIT_LINEAR` | 是否适合线性项（也称为单向项）。 | `true` | `true`、`false` |
| `INIT_STD` | 初始系数的标准偏差。 | 0.01 | (>= 0) |
| `MAX_ITER` | 算法应运行的迭代次数。 | 100 | (>= 0) |
| `MINI_BATCH_FRACTION` | 小批分数，它必须在`(0, 1]`范围内。 | 1.0 | `(0, 1]` |
| `REG_PARAM` | 正则化参数。 | 0.0 | (>= 0) |
| `SEED` | 随机种子。 | 未设置 | 任何64位数字 |
| `SOLVER` | 用于优化的求解器算法。 | “adamW” | `gd`、`adamW` |
| `STEP_SIZE` | 第一步的初始步长（类似于学习率）。 | 1.0 |                   |
| `PREDICTION_COL` | 预测列名称。 | “预测” | 任意字符串 |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'factorization_machines_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Generalized Linear]回归 {#generalized-linear-regression}

与线性回归(假设结果遵循正态（高斯）分布)不同，[!DNL Generalized Linear]模型(GLM)允许结果遵循不同类型的分布，如[!DNL Poisson]或二项式，具体取决于数据的性质。

**参数**

下表概述了用于配置和优化[!DNL Generalized Linear]回归性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-------------------------------------------------------------------------|
| `MAX_ITER` | 设置最大迭代次数（适用于使用求解器`irls`）。 | 25 | (>= 0) |
| `REG_PARAM` | 正则化参数。 | 未设置 | (>= 0) |
| `TOL` | 收敛公差。 | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | `treeAggregate`的建议深度。 | 2 | (>= 2) |
| `FAMILY` | 族参数，用于描述模型中使用的误差分布。 支持的选项为`gaussian`、`binomial`、`poisson`、`gamma`和`tweedie`。 | “高斯” | `gaussian`，`binomial`，`poisson`，`gamma`，`tweedie` |
| `FIT_INTERCEPT` | 是否适合截取条件。 | `true` | `true`、`false` |
| `LINK` | 链接函数，定义线性预测器和分布函数平均值之间的关系。 支持的选项为`identity`、`log`、`inverse`、`logit`、`probit`、`cloglog`和`sqrt`。 | 未设置 | `identity`，`log`，`inverse`，`logit`，`probit`，`cloglog`，`sqrt` |
| `LINK_POWER` | 电源链接函数中的索引，适用于[!DNL Tweedie]系列。 如果未设置，则在R `statmod`包之后，默认为`1 - variancePower`。 0、1、-1和0.5的链接幂分别对应于Log、Identity、Inverse和Sqrt链接。 | 1 |
| `SOLVER` | 用于优化的求解器算法。 支持的选项： `irls`（反复重新加权的最小二乘）。 | &quot;irls&quot; | `irls` |
| `VARIANCE_POWER` | [!DNL Tweedie]分布的方差函数中的幂，它定义方差与平均值之间的关系。 支持的值为0和`[1, inf)`。 | 0.0 | 0，`[1, inf)` |
| `LINK_PREDICTION_COL` | 链接预测（线性预测器）列名称。 | 未设置 | 任意字符串 |
| `OFFSET_COL` | 偏移列名称。 如果未设置，则所有实例偏移都将被视为0.0。偏移特征的常数系数为1.0。 | 未设置 |                                                                        |
| `WEIGHT_COL` | 权重列名称。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 在二项式族中，权重对应于试验次数，并且在AIC计算中舍入非整数权重。 | 未设置 |                                                                        |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'generalized_linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Gradient Boosted Tree]回归 {#gradient-boosted-tree-regression}

梯度提升树(GBTs)是一种有效的分类和回归方法，它将多决策树的预测结合起来，以提高预测精度和模型性能。

**参数**

下表概述了用于配置和优化[!DNL Gradient Boosted Tree]回归性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 用于将连续特征划分为离散间隔的最大桶数，这有助于确定特征在每个决策树节点上的分割方式。 更多的二进制文件提供了更高的粒度。 | 32 | 必须至少为2，并且等于或大于任何分类特征中的类别数。 |
| `CACHE_NODE_IDS` | 如果`false`，则算法将树传递到执行器以将实例与节点进行匹配。 如果`true`，则算法将缓存每个实例的节点ID。 缓存可以加快对更深层树的训练。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 例如，`10`意味着每10次迭代就检查一次缓存。 | 10 | (>= 1) |
| `MAX_DEPTH` | 树的最大深度（非负值）。 例如，深度`0`表示1个叶节点，深度`1`表示1个内部节点和2个叶节点。 | 5 | (>= 0) |
| `MIN_INFO_GAIN` | 在树节点上考虑拆分所需的最小信息增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 拆分后每个子项必须具有的加权样本数的最小分数。 如果拆分导致每个子代中的总权重分数小于此值，则拆分会被丢弃。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 拆分后每个子级必须具有的最小实例数。 如果拆分产生的实例数少于此值，则拆分会被放弃。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 分配给直方图聚合的最大内存（以MB为单位）。 如果此值太小，则每个迭代只拆分1个节点，并且其聚合可能会超过此大小。 | 256 |                                                                                                      |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `VALIDATION_INDICATOR_COL` | 列名，指示每行是用于训练还是用于验证。 `false`用于培训，`true`用于验证。 | 未设置 | 任意字符串 |
| `LEAF_COL` | 叶索引的列名称。 通过预排序遍历生成每个树中各个实例的预测叶索引。 | “” | 任意字符串 |
| `FEATURE_SUBSET_STRATEGY` | 每个树节点中考虑进行拆分的特征数。 | &quot;auto&quot; | `auto`，`all`，`onethird`，`sqrt`，`log2`，`n` （其中`n`是介于0和1.0之间的小数） |
| `SEED` | 随机种子。 | 未设置 | 任何64位数字 |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 |                                                                                                      |
| `LOSS_TYPE` | [!DNL Gradient Boosted Tree]模型尝试最小化的损失函数。 | &quot;squared&quot; | `squared` (L2)和`absolute` (L1)。 注意：值不区分大小写。 |
| `STEP_SIZE` | `(0, 1]`范围内的步长大小（也称为学习率），用于缩小每个估算器的贡献。 | 0.1 | `(0, 1]` |
| `MAX_ITER` | 算法的最大迭代次数。 | 20 | (>= 0) |
| `SUBSAMPLING_RATE` | 用于学习每个决策树的训练数据的小数，在`(0, 1]`范围内。 | 1.0 | `(0, 1]` |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'gradient_boosted_tree_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Isotonic]回归 {#isotonic-regression}

[!DNL Isotonic Regression]是一种算法，用于迭代调整距离，同时保留数据中的相对不相似顺序。

**参数**

下表概述了用于配置和优化[!DNL Isotonic Regression]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `ISOTONIC` | 指定当`true`时输出序列是等调（递增），还是当`false`时输出序列是反调（递减）。 | `true` | `true`、`false` |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任意字符串 |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `FEATURE_INDEX` | 功能的索引，在`featuresCol`为矢量列时适用。 如果未设置，则默认值为`0`。 否则，它没有效果。 | 0 |                 |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'isotonic_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Linear]回归 {#linear-regression}

[!DNL Linear Regression]是一种监督机器学习算法，它将线性方程式拟合到数据，以便对依赖变量和独立特征之间的关系建模。

**参数**

下表概述了用于配置和优化[!DNL Linear Regression]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | 最大迭代次数。 | 100 | (>= 0) |
| `REGPARAM` | 正则化参数用于控制模型的复杂性。 | 0.0 | (>= 0) |
| `ELASTICNETPARAM` | ElasticNet混合参数，用于控制L1（套索）和L2（脊）之间的平衡。 值为0将应用L2惩罚，值为1将应用L1惩罚。 | 0.0 | (>= 0， &lt;= 1) |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'linear_reg'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Random Forest Regression] {#random-forest-regression}

[!DNL Random Forest Regression]是一种集成算法，用于在训练期间构建多个决策树，并返回这些决策树用于回归任务的平均预测，有助于防止过度拟合。

**参数**

下表概述了用于配置和优化[!DNL Random Forest Regression]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|------------------------------------------------------------------------------------------------------|
| `MAX_BINS` | 用于离散连续特征并确定每个节点上的特征拆分方式的最大二进制文件数。 更多的二进制文件提供了更高的粒度。 | 32 | 必须至少为2，并且至少等于任何分类特征中的类别数。 |
| `CACHE_NODE_IDS` | 如果`false`，则算法将树传递到执行器以将实例与节点进行匹配。 如果`true`，则算法会缓存每个实例的节点ID，从而加快深度树的训练。 | `false` | `true`、`false` |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 例如，`10`意味着每10次迭代就检查一次缓存。 | 10 | (>= 1) |
| `IMPURITY` | 用于信息增益计算的标准（区分大小写）。 | &quot;熵&quot; | `entropy`、`gini` |
| `MAX_DEPTH` | 树的最大深度（非负值）。 例如，深度`0`表示一个叶节点，深度`1`表示一个内部节点和2个叶节点。 | 5 | [0， 30] |
| `MIN_INFO_GAIN` | 在树节点上考虑拆分所需的最小信息增益。 | 0.0 | (>= 0.0) |
| `MIN_WEIGHT_FRACTION_PER_NODE` | 拆分后每个子项必须具有的加权样本数的最小分数。 如果拆分导致每个子代中总重量的分数小于此值，则放弃拆分。 | 0.0 | (>= 0.0， &lt;= 0.5) |
| `MIN_INSTANCES_PER_NODE` | 拆分后每个子级必须具有的最小实例数。 如果拆分产生的实例数少于此值，则拆分会被放弃。 | 1 | (>= 1) |
| `MAX_MEMORY_IN_MB` | 分配给直方图聚合的最大内存（以MB为单位）。 如果此值太小，则每个迭代只拆分1个节点，并且其聚合可能会超过此大小。 | 256 |                                                                                                      |
| `BOOTSTRAP` | 是否在构建树时使用引导示例。 | TRUE | `true`、`false` |
| `NUM_TREES` | 要训练的树的数量（至少1）。 如果`1`，则不使用引导。 如果大于`1`，则应用引导。 | 20 | (>= 1) |
| `SUBSAMPLING_RATE` | 用于训练每个决策树的训练数据的部分，在`(0, 1]`范围内。 | 1.0 | `(0, 1]` |
| `LEAF_COL` | 通过预排序遍历生成的叶索引的列名，即每个树中每个实例的预测叶索引。 | “” | 任意字符串 |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `SEED` | 随机种子。 | 未设置 | 任何64位数字 |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任何有效的列名或留空。 |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'random_forest_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## [!DNL Survival Regression] {#survival-regression}

[!DNL Survival Regression]用于根据[!DNL Weibull distribution]拟合参数存活率回归模型，称为[!DNL Accelerated Failure Time] (AFT)模型。 它可以将实例栈叠到块中以提高性能。

**参数**

下表概述了用于配置和优化[!DNL Survival Regression]性能的关键参数。

| 参数 | 描述 | 默认值 | 可能值 |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| `MAX_ITER` | 算法应运行的最大迭代次数。 | 100 | (>= 0) |
| `TOL` | 收敛公差。 | `1E-6` | (>= 0) |
| `AGGREGATION_DEPTH` | `treeAggregate`的建议深度。 如果特征尺寸或分区数很大，可将此参数设置为较大的值。 | 2 | (>= 2) |
| `FIT_INTERCEPT` | 是否适合截取条件。 | TRUE | `true`、`false` |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |
| `CENSOR_COL` | 用于审查的列名称。 值为`1`表示该事件已发生（未审查），而`0`表示该事件已审查。 | &quot;censor&quot; | 0， 1 |
| `MAX_BLOCK_SIZE_IN_MB` | 用于将输入数据栈叠到块中的最大内存（以MB为单位）。 如果分区中的剩余数据大小较小，则相应地调整此值。 值`0`允许自动调整。 | 0.0 | (>= 0) |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname OPTIONS(
  type = 'survival_regression'
) AS
  SELECT col1, col2, col3 FROM training-dataset
```

## 后续步骤

阅读本文档后，您现在知道如何配置和使用各种回归算法。 接下来，请参阅有关[分类](./classification.md)和[群集](./clustering.md)的文档，了解其他类型的高级统计模型。
