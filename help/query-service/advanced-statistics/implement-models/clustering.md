---
title: 聚类算法
description: 了解如何使用关键参数、描述和示例代码配置和优化各种聚类算法，以帮助您实施高级统计模型。
role: Developer
exl-id: 273853c6-85d2-43e5-b51a-aa9d20b313ae
source-git-commit: 69c08f688d355e689e78426dd4b0ed1f4934965c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 4%

---

# 聚类算法 {#clustering-algorithms}

聚类算法根据数据点的相似性将其分组为不同的聚类，使无监督学习能够揭示数据中的模式。 要创建聚类算法，请使用`OPTIONS`子句中的`type`参数指定要用于模型训练的算法。 接下来，将相关参数定义为键值对以微调模型。

>[!NOTE]
>
>确保您了解所选算法的参数要求。 如果选择不自定义某些参数，系统将应用默认设置。 请查阅相关文档，以了解每个参数的函数和默认值。

## [!DNL K-Means] {#kmeans}

`K-Means`是一种将数据点划分为预定数目的群集(k)的群集算法。 由于算法简单，效率较高，所以成为最常用的聚类算法之一。

**参数**

使用`K-Means`时，可以在`OPTIONS`子句中设置以下参数：

| 参数 | 描述 | 默认值 | 可能值 |
|---------------------|---------------------------------------------------------------------------------------------------------------|-----------------|----------------------------------|
| `MAX_ITER` | 算法应运行的迭代次数。 | `20` | (>= 0) |
| `TOL` | 收敛容差级别。 | `0.0001` | (>= 0) |
| `NUM_CLUSTERS` | 要创建的群集数(`k`)。 | `2` | (>1) |
| `DISTANCE_TYPE` | 用于计算两点之间距离的算法。 值区分大小写。 | `euclidean` | `euclidean`、`cosine` |
| `KMEANS_INIT_METHOD` | 群集中心的初始化算法。 | `k-means\|\|` | `random`，`k-means\|\|` (k-means++的并行版本) |
| `INIT_STEPS` | `k-means\|\|`初始化模式的步骤数（仅当`KMEANS_INIT_METHOD`为`k-means\|\|`时适用）。 | `2` | (>0) |
| `PREDICTION_COL` | 将存储预测的列的名称。 | `prediction` | 任意字符串 |
| `SEED` | 重复性的随机种子。 | `-1689246527` | 任何64位数字 |
| `WEIGHT_COL` | 用于实例权重的列的名称。 如果未设置，则所有实例都将平均加权。 | `not set` | 不适用 |

{style="table-layout:auto"}

**示例**

```sql
CREATE MODEL modelname 
OPTIONS(
  type = 'kmeans',
  MAX_ITERATIONS = 30,
  NUM_CLUSTERS = 4
) 
AS SELECT col1, col2, col3 FROM training-dataset;
```

## [!DNL Bisecting K-means] {#bisecting-kmeans}

[!DNL Bisecting K-means]是一种使用分裂（或“自上而下”）方法的层次聚类算法。 所有观测值都从单个簇开始，在构建层次时递归执行分割。 [!DNL Bisecting K-means]通常比常规的K均值更快，但它通常会产生不同的聚类结果。

**参数**

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------------|
| `MAX_ITER` | 算法运行的最大迭代次数。 | 20 | (>= 0) |
| `WEIGHT_COL` | 实例权重的列名称。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任意字符串 |
| `NUM_CLUSTERS` | 所需的叶群集数。 如果没有可分割的簇，实际数字可能会更小。 | 4 | (> 1) |
| `SEED` | 算法中用于控制随机进程的随机种子。 | 未设置 | 任何64位数字 |
| `DISTANCE_MEASURE` | 用于计算点之间相似性的距离度量。 | “欧几里德” | `euclidean`、`cosine` |
| `MIN_DIVISIBLE_CLUSTER_SIZE` | 可分簇所需的最小点数（如果>= 1.0）或最小点比例（如果&lt; 1.0）。 | 1.0 | (>= 0) |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'bisecting_kmeans',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Gaussian Mixture Model] {#gaussian-mixture-model}

[!DNL Gaussian Mixture Model]表示从k个高斯子分布之一提取数据点的复合分布，每个子分布都有自己的概率。 它用于建模假定由多个高斯分布的混合产生的数据集。

**参数**

| 参数 | 描述 | 默认值 | 可能值 |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | 算法运行的最大迭代次数。 | 100 | (>= 0) |
| `WEIGHT_COL` | 列名称，例如，权重。 如果未设置或为空，则所有实例权重都将被视为`1.0`。 | 未设置 | 任何有效的列名或为空 |
| `NUM_CLUSTERS` | 混合模型中独立高斯分布的个数。 | 2 | (> 1) |
| `SEED` | 算法中用于控制随机进程的随机种子。 | 未设置 | 任何64位数字 |
| `AGGREGATION_DEPTH` | 此参数控制计算期间使用的聚合树的深度。 | 2 | (>= 1) |
| `PROBABILITY_COL` | 预测类条件概率的列名称。 这些应被视为置信度分数，而不是确切概率。 | “概率” | 任意字符串 |
| `TOL` | 迭代算法的收敛容限。 | 0.01 | (>= 0) |
| `PREDICTION_COL` | 预测输出的列名称。 | “预测” | 任意字符串 |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'gaussian_mixture',
) AS
  select col1, col2, col3 from training-dataset
```

## [!DNL Latent Dirichlet Allocation] (LDA) {#latent-dirichlet-allocation}

[!DNL Latent Dirichlet Allocation] (LDA)是一种概率模型，可从文档集合中捕获基础主题结构。 它是一个三级层次贝叶斯模型，包含词层、主题层和文档层。 LDA使用这些层以及观察到的文档来构建潜在的主题结构。

**参数**

| 参数 | 描述 | 默认值 | 可能值 |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|------------------------------------------|
| `MAX_ITER` | 算法运行的最大迭代次数。 | 20 | (>= 0) |
| `OPTIMIZER` | 用于估计LDA模型的优化程序或推理算法。 支持的选项为`"online"`（在线变分贝叶斯）和`"em"`（期望最大化）。 | &quot;online&quot; | `online`，`em` （不区分大小写） |
| `NUM_CLUSTERS` | 要创建的群集数(k)。 | 10 | (> 1) |
| `CHECKPOINT_INTERVAL` | 指定对缓存的节点ID进行检查的频率。 | 10 | (>= 1) |
| `DOC_CONCENTRATION` | 集中参数(“alpha”)确定关于跨文档主题分布的先前假设。 默认行为由优化程序确定。 对于`EM`优化程序，alpha值应大于1.0(默认值：均匀分布为(50/k) + 1)，确保对称主题分布。 对于`online`优化程序，Alpha值可以为0或更大（默认：均匀分布为1.0/k），从而允许更灵活的主题初始化。 | 自动 | 长度k的任意单值或矢量，其中EM的值> 1 |
| `KEEP_LAST_CHECKPOINT` | 指示在使用`em`优化程序时是否保留最后一个检查点。 如果数据分区丢失，则删除检查点可能会导致失败。 当不再需要检查点时，会自动将检查点从存储中删除，具体情况由引用计数确定。 | `true` | `true`、`false` |
| `LEARNING_DECAY` | `online`优化程序的学习速率，设置为介于`(0.5, 1.0]`之间的指数衰减速率。 | 0.51 | `(0.5, 1.0]` |
| `LEARNING_OFFSET` | `online`优化程序的学习参数，用于降低早期迭代的权重，以降低早期迭代的计数。 | 1024 | (> 0) |
| `SEED` | 用于在算法中控制随机进程的随机种子。 | 未设置 | 任何64位数字 |
| `OPTIMIZE_DOC_CONCENTRATION` | 对于`online`优化器：是否在培训期间优化`docConcentration`（文档主题分发的Dirichlet参数）。 | `false` | `true`、`false` |
| `SUBSAMPLING_RATE` | 对于`online`优化程序：在`(0, 1]`范围内，在每次小批次梯度下降迭代中采样和使用的语料的分数。 | 0.05 | `(0, 1]` |
| `TOPIC_CONCENTRATION` | 集中参数（“beta”或“eta”）定义对主题于条款之分布所作之先前假设。 默认值由优化程序确定：对于`EM`，值> 1.0（默认值= 0.1 + 1）。 对于`online`，值≥0 （默认值= 1.0/k）。 | 自动 | 长度k的任意单值或矢量，其中EM的值> 1 |
| `TOPIC_DISTRIBUTION_COL` | 此参数输出每个文档的估计主题混合分布，在文献中通常称为“theta”。 对于空文档，它返回零向量。 估计值使用变分近似（“伽马”）导出。 | 未设置 | 任意字符串 |

{style="table-layout:auto"}

**示例**

```sql
Create MODEL modelname OPTIONS(
  type = 'lda',
) AS
  select col1, col2, col3 from training-dataset
```

## 后续步骤

阅读本文档后，您现在知道如何配置和使用各种聚类算法。 接下来，请参阅有关[分类](./classification.md)和[回归](./regression.md)的文档，了解其他类型的高级统计模型。
