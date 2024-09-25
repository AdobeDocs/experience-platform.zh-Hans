---
title: 使用Experience Query Service中的超多维数据集进行高效的大数据分析
description: 了解如何使用Adobe Experience Platform查询服务中的多维数据集，通过近似的唯一计数优化大数据分析，从而减少完全数据重新处理的需要。
source-git-commit: e21eab682b2d29da4441a32d7307af7cf873f295
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---

# 使用超多维数据集进行高效的大数据分析

>[!AVAILABILITY]
>
>此功能仅适用于已购买[Data Distiller SKU](./data-distiller/overview.md)的用户。 有关更多信息，请与您的Adobe代表联系。

了解如何在Adobe Experience Platform的Experience Query Service中使用超多维数据集，以提高效率执行高级数据分析。 本文档介绍如何使用[[!DNL Apache Datasketches] 库](https://datasketches.apache.org/)的高级函数以增量方式处理不同的计数和复杂的计算，而不必每次都重新处理历史数据。

在大数据分析中，生成量度，如非重复计数、分位数、最频繁项目、联接和图分析通常涉及非累加计数（其中结果不能简单地从子组中求和）。 传统方法需要重新处理所有历史数据，这可能占用大量资源和时间。 使用草图（即使用概率表示大型数据集的简洁摘要）和高级查询服务功能，通过减少重新计算的需要来简化此过程。

## 超多维数据集的关键功能 {#key-functions}

超多维数据集提供了多种强大的功能，以提高数据分析效率和灵活性。

1. **计算独特用户或不同查询数**：使用SQL功能生成与数据的各种维度（如产品查看、网站访问或商业活动）交互的独特用户数，而无需重复重新分析原始数据。
2. **增量处理**：执行增量更新以折叠和合并跨维度和时间的数据点，而不从头开始重新计算所有内容。
3. **多维度分析**：超立方体支持多维度过滤和重新排列数据，以创建表示维度组合的摘要行。 然后，这些摘要可用于以最小的计算开销生成见解。

## 超多维数据集用例 {#use-cases}

使用超多维数据集高效地为各种用户交互生成不同的计数，而无需每次都完全重新计算数据。 以下是一些实用的使用场景：

- 分析在定义的时间段内查看特定产品的独特访客。
- 识别在给定时间段内与多个产品进行交互的用户，以增强交叉销售分析。
- 区分随着时间的推移，使用一种产品而不是另一种产品的用户，以揭示偏好设置模式。
- 将在线和离线交互数据相结合，可全面了解用户在特定时段内的行为。
- 跟踪用户在事件中不同活动之间的移动，以优化布局和服务。

## 使用超多维数据集的好处

在这些情况下，您可以预先计算特定类别的基本信息。 但是，在跨多个维度和时间段分析数据时，必须从原始数据重新计算所有内容，或使用查询服务超多维数据集。 超立方体通过高效组织数据来简化流程，这允许灵活过滤和多维度分析，而无需重新处理。 他们使用高级功能快速准确地评估结果，从而提供关键优势，例如提高处理效率、可扩展性和对复杂分析任务的适应性。

### 查询处理的数据大小效率

查询服务可以将数百万或数十亿数据点（例如，用户ID）压缩为称为草图的紧凑形式。 此草图显着减小了查询处理的数据大小，从而维护了可扩展性并使处理变得更加简单和快速。 无论原始数据变得多大，草图的大小都会保持很小，这使得分析大数据变得更加易于管理和高效。

下图说明如何将Commerce、产品信息和Web维度ExperienceEvents处理为草图，然后使用草图来估计唯一计数。

![显示使用查询服务创建草绘的信息图形。 该图说明了如何将Commerce、产品信息和Web维度的ExperienceEvents处理为草图，然后使用这些草图来近似唯一计数。](./images/hypercubes/hypercube-overview.png)

### 合并草图，使数据分析更快速、更轻松

要避免重新计算并提高处理速度，可以合并来自不同类别或组的草图。 查询服务还通过将您的数据组织到超多维数据集来简化设计，其中每一行在草图列旁边成为其分区（维度的集合）的摘要。 超多维数据集的每一行都包含维度组合，但没有任何原始数据。 执行查询时，指定要用于生成附加量度的维列，并合并这些行的草图。

![该图显示了如何合并来自不同ExperienceEvents的草图，以便在各个维度中创建近似的唯一计数。](./images/hypercubes/merge-sketches.png)

### 成本效益 {#cost-effectiveness}

客户数据通常是大规模的，但您无需使用增量处理来重新处理历史数据。 草图要小得多，可以实现更快的实时结果，同时节省计算资源和成本。 此数据转换使交互式查询更加可行和高效。

## 函数概述

本节概述每个函数如何通过有效使用草图和超多维数据集来优化数据处理并增强分析能力。 它详细介绍了它们的用途、示例语法、参数和预期输出。

### 创建具有HLL草图的唯一计数估计

`hll_build_agg`是一个创建HLL (HyperLogLog)草图的聚合函数。 此函数是一种简洁的概率方法，用于估计分组数据集中列或表达式中的唯一值数量。

#### 函数定义

```sql
hll_build_agg(column [, lgConfigK])
```

**用法：**

以下示例演示如何在查询中构建函数。

```sql
SELECT
   [dim1, dim2 ... ,] hll_build_agg(coalesce(col1, col2, col3)) AS sketch_col
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### 参数

| 参数 | 描述 |
|---------------------------|---------------------------------------|
| `column` | 要在其上创建草绘的列或列名称。 |
| `lgConfigK` | *Int*（可选） K的以log-base-2表示，其中K是HLL Sketch的存储桶或插槽的数量。 最小值： 4。 最大值：12。 默认值： 12。 |

#### 输出

| 输出列 | 描述 |
|---------------------------|---------------------------------------|
| `sketch_res` | 包含字符串形式的列，该字符串包含字符串化的HLL草图。 |

#### SQL示例

以下示例在`customer_id`列上构建聚合草图：

```sql
SELECT
  country,
  hll_build_agg(customer_id, 10) AS sketch
FROM
  EXPLODE(
    ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
      ('UA', 'customer_id_1', 'invoice_id_11'),
      ('CZ', 'customer_id_2', 'invoice_id_22'),
      ('CZ', 'customer_id_2', 'invoice_id_23'),
      ('BR', 'customer_id_3', 'invoice_id_31'),
      ('UA', 'customer_id_2', 'invoice_id_24')
    ])
GROUP BY country;
```

**SQL示例输出：**

| 国家/地区 | Sketch |
|---------|------------------------------------------------------------|
| UA | AgEHBAMAAgCR9mUEulKKCQAAAAAAAAAAAAAAAAAAAAAA== |
| CZ | AgEHBAMAAAQC6UoaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaA== |
| BR | AgEHBAMAAAQCcmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA== |

### 使用HLL草图估算非重复计数

`hll_estimate`是一个标量函数，它提供数据集每一行内非重复计数的估计。 与聚合函数不同，`hll_estimate`按行操作，用于估计单个行中草图的不同计数。

>[!NOTE]
>
>此函数不能用作聚合函数。 对于聚合计数，请使用`sketch_count`。

#### 函数定义

```sql
hll_estimate(sketch_col)
```

**用法：**

以下示例演示如何在查询中构建函数。

```sql
SELECT
   [col1, col2 ... ,] hll_estimate(sketch_column) AS estimate
FROM fact_sketch_table
```

#### 参数

| 参数 | 描述 |
|---------------------------|---------------------------------------|
| `sketch_column` | 包含字符串化HLL草图的列。 它会估计每行中草图的独特计数。 |

#### 输出

| 输出列 | 描述 |
|---------------------------|---------------------------------------|
| `estimate` | 双精度类型的列，提供草绘的预估值，四舍五入到两位小数。 |

#### SQL示例

以下示例在HLL草图上使用`hll_estimate`函数按国家/地区估计客户的独特计数：

```sql
SELECT
  country,
  hll_estimate(hll_build_agg(customer_id, 10)) AS distinct_customers_by_country
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id, 10) AS sketch
    FROM 
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
  );
```

**SQL示例输出：**

| 国家/地区 | distinct_customers_by_country |
|---------|-------------------------------|
| UA | 2.00 |
| CZ | 1.00 |
| BR | 1.00 |

### 将多个HLL草图与`hll_merge_agg`合并

`hll_merge_agg`是一个聚合函数，它合并一个组内的多个HLL草图，生成一个新的草图作为输出。 它允许跨分区或维度组合草图，从而提高数据分析灵活性。

#### 函数定义

```sql
hll_merge_agg(sketch_col [, allowDifferentLgConfigK])
```

**用法：**

以下示例演示如何在查询中构建函数。

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_agg(sketch_column.sketch) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### 参数

| 参数 | 描述 |
|---------------------------|---------------------------------------|
| `sketch_column` | 包含字符串化HLL草图的列。 |
| `allowDifferentLgConfigK` | *Boolean*（可选）如果设置为true，则允许合并具有不同值`lgConfigK`的草图。 默认值为false。 如果值为false且草图的`lgConfigK`值不同，则会引发异常。 |

>[!NOTE]
>
>如果`allowDifferentLgConfigK`设置为false，则合并具有不同值`lgConfigK`的草图将导致`UnsupportedOperationException`。

#### 输出

| 输出列 | 描述 |
|----------------|-------------------------------------------------|
| `sketch_res` | 包含字符串化合并的HLL草绘的HLL草绘类型的列。 |

#### SQL示例

以下示例合并`customer_id`列上的多个HLL草图：

```sql
SELECT
   hll_merge_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**SQL示例输出：**

| 国家/地区 | hll_merge_agg(sketch， true) |
|---------|--------------------------------------------|
| UA | AgEHDAMAAwiR9mUEulKKCQAAAAAAAAAAAAAAA== |
| CZ | AgEHDAMAAAQi6Uoaaaaaaaaaaaaaaaaa== |
| BR | AgEHDAMAAAQicmH0HAAAAAAAAAAAAAAAAAAAA== |
| MX | AgEHFQMAAgiGL/kNdAAAAAAAAAAAAAAAAAAA== |

### 使用`hll_merge_count_agg`估算基数

`hll_merge_count_agg`是一个聚合函数，它根据列中的一个或多个草图估计基数（唯一元素的数量）。 对于分组内遇到的所有草图，它会返回单个估计值。 此函数用于聚合草图，不能用作逐行转换。 对于基于行的估计，请使用`sketch_estimate`。

#### 函数定义

```sql
hll_merge_count_agg(sketch_col [, allowDifferentLgConfigK])
```

**用法：**

以下示例演示如何在查询中构建函数。

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_count_agg(sketch_column) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### 参数

| 参数 | 描述 |
|-------------------------|----------------------------------------------|
| `sketch_column` | 包含字符串化HLL草图的列。 |
| `allowDifferentLgConfigK` | *Boolean*（可选）默认值为false。 如果设置为true，则允许合并具有不同值`lgConfigK`的草图。 否则，将引发`UnsupportedOperationException`。 |

#### 输出

| 输出列 | 描述 |
|---------------|----------------------------------------------------------|
| `estimate` | 双精度类型的列，提供草图的估计值。 |

#### SQL示例

以下示例使用`hll_merge_count_agg`函数估计具有发票的唯一客户的数量：

```sql
SELECT
   hll_merge_count_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**SQL示例输出：**

| 国家/地区 | hll_merge_count_agg(sketch， true) |
|---------|----------------------------------|
| UA | 2.0 |
| CZ | 1.0 |
| BR | 1.0 |
| MX | 2.0 |

## 限制

目前，草图在创建后无法更新。 未来的更新将引入更新草图的功能。 利用此功能，您可以更有效地处理错过的运行和迟到的数据。

## 后续步骤

通过阅读本文档，您现在知道如何使用超立方体和相关草图函数为复杂的多维分析执行高效的数据处理，而无需重新处理历史数据。 此方法可节省时间、降低成本，并提供实时、交互式查询所需的灵活性，使其成为Adobe Experience Platform中大数据分析的宝贵工具。

接下来，探索其他关键概念，如[增量加载](./key-concepts/incremental-load.md)和[数据重复数据删除](./key-concepts/deduplication.md)，以加深您对如何有效使用这些功能来满足特定数据需求的理解。


