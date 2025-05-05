---
title: 特征转换技术
description: 了解基本预处理技术（如数据转换、编码和特征缩放），这些技术为统计模型训练准备数据。 它涵盖了处理缺失值和转换分类数据以提高模型性能和准确性的重要性。
role: Developer
exl-id: ed7fa9b7-f74e-481b-afba-8690ce50c777
source-git-commit: e7bc30c153f67c59e9c04e8c8df60394f48871d0
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 8%

---

# 特征变换技术

转换是重要的预处理步骤，可将数据转换为适合模型训练和分析的格式，从而确保最佳的性能和准确性。 本文档作为补充的语法资源，提供了有关用于数据预处理的关键特征转换技术的详细信息。

机器学习模型无法直接处理字符串值或null值，这使得数据预处理至关重要。 本指南介绍如何使用各种转换来估算缺失值、将分类数据转换为数字格式以及应用特征缩放技术（如单热编码和矢量化）。 这些方法使模型能够有效地解释和学习数据，最终提高其性能。

## 自动特征转换 {#automatic-transformations}

如果选择跳过`CREATE MODEL`命令中的`TRANSFORM`子句，则功能转换会自动进行。 自动数据预处理包括空替换和标准特征转换（基于数据类型）。 自动输入数值和文本列，然后进行特征转换，以确保数据采用适合机器学习模型训练的格式。 此过程包括缺少数据估算以及分类、数字和布尔转换。

>[!IMPORTANT]
>
>训练时使用的特征转换也将在预测和评估时使用的特征转换。

下表说明在`CREATE MODEL`命令期间省略`TRANSFORM`子句时如何处理不同的数据类型。

### 空替换 {#automatic-null-replacement}

| 数据类型 | 空替换 |
|-----------------|-----------------------------------------------------|
| 数值 | 空值将替换为列的平均值。 |
| 类别 | Null将替换为`ml_unknown`关键字。 |
| 布尔值 | Null被替换为`FALSE`值。 |
| 时间戳 | 此字段应为连续字段。 |
| 嵌套/结构 | 替换取决于叶节点的数据类型。 |

### 特征转换 {#automatic-feature-transformation}

| 数据类型 | 特征转换 |
|-----------------|-----------------------------------------------------|
| 数值 | 非必需 — 因为机器学习算法可以理解此数据类型。 |
| 字符串 | 出现字符串索引。 |
| 布尔值 | 出现字符串索引。 |
| 时间戳 | 没有发生操作。 |
| 结构 | 该值将展开到其叶节点。 根据叶节点的数据类型进行转换。 |

**示例**

```sql
CREATE model modelname options(model_type='logistic_reg', label='rating') AS SELECT * FROM movie_rating;
```

## 手动功能转换 {#manual-transformations}

若要在`CREATE MODEL`语句中定义自定义数据预处理，请将`TRANSFORM`子句与任意数量的可用转换函数结合使用。 这些手动预处理函数也可以在`TRANSFORM`子句之外使用。 可以使用下面[&#128279;](#available-transformations)的转换器部分中讨论的所有转换来手动预处理数据。

### 关键特性 {#key-characteristics}

下面是定义预处理函数时要考虑的特征转换的主要特征：

- **语法**： `TRANSFORM(functionName(colName, parameters) <aliasNAME>)`
   - 别名在语法中是必需的。 您必须提供别名，否则查询将失败。

- **参数**：参数是位置参数。 这意味着，每个参数只能采用某些值，如果提供了自定义值，则需要指定前面的所有参数。 有关哪个函数采用哪个参数的详细信息，请参阅相关文档。

- **链接转换器**：一个转换器的输出可以成为另一个转换器的输入。

- **功能用法**：上次的功能转换被用作机器学习模型的功能。

**示例**

```sql
CREATE MODEL modelname 
TRANSFORM(
  string_imputer(language, 'adding_null') AS imp_language, 
  numeric_imputer(users_count, 'mode') AS imp_users_count, 
  string_indexer(imp_language) AS si_lang,  
  vector_assembler(array(imp_users_count, si_lang, watch_minutes)) AS features
)  
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='rating') 
AS SELECT * FROM df;
```

## 可用的转换 {#available-transformations}

有19种可用的转换。 这些转换被拆分为[常规转换](#general-transformations)、[数值转换](#numeric-transformations)、[分类转换](#categorical-transformations)和[文本转换](#textual-transformations)。

### 常规转换 {#general-transformations}

请阅读此部分，了解有关用于各种数据类型的转换器的详细信息。 如果您需要应用并非特定于分类或文本数据的转换，则此信息至关重要。

>[!NOTE]
>
>输入数据类型是指应用估算的列。 输出数据类型是指转换生效后作为输出生成的列。

#### 数值输入器 {#numeric-imputer}

**数值输入器**&#x200B;转换器完成数据集中缺少值的操作。 这使用缺失值所在列的平均值、中间值或模式。 输入列应为`DoubleType`或`FloatType`。 可在[Spark算法文档](https://spark.apache.org/docs/2.2.0/ml-features.html#imputer)中找到更多信息和示例。

>[!NOTE]
>
>输入列中的所有null值都被视为缺失，因此也会被推断。

**数据类型**

- 输入数据类型：数字
- 输出数据类型：数字

**定义**

```sql
transformer(numeric_imputer(hour, 'mean') hour_imputed)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
| -------- | ------------ | ----- | -------- | -------- |
| `STRATEGY` | 一种估算策略。 可用值为： [`mean`、`median`、`mode`]。 | 字符串 | 平均值 | 可选 |

{style="table-layout:auto"}

**推算前的示例**

| ID | 小时 |
|---|---|
| 0 | 18.0 |
| 1 | null |
| 2 | 8.0 |

**估算后的示例（使用平均策略）**

| ID | 小时 |
|---|---|
| 0 | 18.0 |
| 1 | 13.0 |
| 2 | 8.0 |

#### 字符串输入器 {#string-imputer}

**String输入器**&#x200B;转换器使用用户提供的字符串作为函数参数来完成数据集中的缺失值。 输入和输出列应为`string`数据类型。

>[!NOTE]
>
>输入列中的所有null值都被视为缺失，并被指定的字符串替换。

**数据类型**

- 输入数据类型：字符串
- 输出数据类型：字符串

**定义**

```sql
transform(string_imputer(name, 'unknown_name') as name_imputed)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | 替换null的值。 | 字符串 | ml_unknown | 可选 |

{style="table-layout:auto"}

**推算前的示例**

| ID | name |
|---|---|
| 0 | John |
| 1 | null |
| 2 | Alice |

**填充后的示例（使用“ml_unknown”作为替换）**

| ID | name |
|---|---|
| 0 | John |
| 1 | ml_unknown |
| 2 | Alice |

#### 布尔型输入器 {#boolean-imputer}

**Boolean输入器**&#x200B;转换器完成了一个布尔列的数据集中缺少值的操作。 输入列和输出列的类型应为`Boolean`。

>[!NOTE]
>
>输入列中的所有null值都被视为缺失，并被指定的布尔值替换。

**数据类型**

- 输入数据类型：布尔型
- 输出数据类型：布尔型

**定义**

```sql
transform(boolean_imputer(name, true) as name_imputed)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
| -------- | ------------ | ----- | -------- | -------- |
| `NULL_REPLACEMENT` | 布尔型输入器。 允许的值： [`true`，`false`]。 | 布尔 | false | 可选 |

**推算前的示例**

| ID | 标志 |
|---|---|
| 0 | true |
| 1 | null |
| 2 | false |

**计算后的示例（使用“true”作为替换）**

| ID | 标志 |
|---|---|
| 0 | true |
| 1 | true |
| 2 | false |

#### 矢量组合器 {#vector-assembler}

`VectorAssembler`转换器将指定的输入列列表合并为单个矢量列，从而更容易管理机器学习模型中的多个功能。 这对于将原始特征和由不同特征变换器生成的特征合并到一个统一特征向量中特别有用。 `VectorAssembler`接受数字、布尔和矢量类型的输入列。 在每一行中，输入列的值以指定顺序串连到向量中。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#vectorassembler) -->

**数据类型**

- 输入数据类型： `array[string]` （具有数字/数组[数字]值的列名）
- 输出数据类型： `Vector[double]`

**定义**

```sql
transform(vector_assembler(id, hour, mobile, userFeatures) as features)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
| -------- | ------------ | ----- | -------- | -------- |
| 无 | 此转换器不需要其他参数。 | 无 | 无 | 无 |

{style="table-layout:auto"}

**转换前的示例**

| ID | 小时 | 移动设备 | 用户功能 | 已单击 |
|---|-------|--------|------------------|---------|
| 0 | 18 | 1.0 | [0.0， 10.0， 0.5] | 1.0 |

{style="table-layout:auto"}

转换后的&#x200B;**示例**

| ID | 小时 | 移动设备 | 用户功能 | 已单击 | 功能 |
|---|------|--------|------------------|---------|-------------------------------|
| 0 | 18 | 1.0 | [0.0， 10.0， 0.5] | 1.0 | [18.0， 1.0， 0.0， 10.0， 0.5] |

{style="table-layout:auto"}

### 数值转换 {#numeric-transformations}

阅读此部分以了解用于处理和缩放数值数据的可用转换器。 这些转换器是处理和优化数据集中的数值功能所必需的。

#### 二进制化程序 {#binarizer}

`Binarizer`转换器通过称为二进制化的过程将数字特征转换为二进制(0/1)特征。 大于指定阈值的特征值将转换为1.0，而等于或小于阈值的值将转换为0.0。`Binarizer`支持输入列的`Vector`和`Double`类型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#binarizer). -->

**数据类型**

- 输入数据类型：数值列
- 输出数据类型：数字

**定义**

```sql
transform(numeric_imputer(rating, 'mode') rating_imp, binarizer(rating_imp) rating_binarizer)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|------------|----------------------------------------------------------------------------------------------------------|----------|----------|----------|
| `THRESHOLD` | 用于二值化连续特征的阈值参数。 大于阈值的特征被二进制化为1.0，而等于或小于阈值的特征被二进制化为0.0。 | int/double | 0.0 | 可选 |

{style="table-layout:auto"}

**二进制化前的输入示例**

| ID | 评级 |
|---|---------|
| 0 | -18.0 |
| 1 | 13.0 |
| 2 | 8.0 |

**二值化后的输出示例（默认阈值为0.0）**

| ID | 评级 |
|---|---------|
| 0 | 0.0 |
| 1 | 1.0 |
| 2 | 1.0 |

具有自定义阈值的&#x200B;**定义**

```sql
transform(numeric_imputer(age, 'mode') age_imp, binarizer(age_imp, 14.0) age_binarizer)
```

**二值化后的输出示例（阈值为14.0）**

| ID | 年龄 |
|---|-------|
| 0 | 0.0 |
| 1 | 0.0 |
| 2 | 1.0 |

#### Bucketizer {#bucketizer}

`Bucketizer`转换器根据用户指定的阈值将连续功能列转换为功能桶列。 此过程对于将连续数据分段到离散的二进制文件桶或存储桶非常有用。 `Bucketizer`需要定义存储桶边界的`splits`参数。

**数据类型**

- 输入数据类型：数值列
- 输出数据类型：数字（捆绑值）

**定义**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|----------|----------|
| `splits` | 用于将连续特征映射到存储桶中的参数。 通过`n+1`拆分，有`n`桶。 拆分必须严格按照递增的顺序进行，并且范围(x，y)用于每个分段，最后一个分段除外，包括y。 | 数组（双精度） | 不适用 | 可选 |

{style="table-layout:auto"}

**拆分示例**

- 数组(Double.NegativeInfinity， 0.0， 1.0， Double.PositiveInfinity)
- 数组(0.0、1.0、2.0)

拆分应涵盖双精度值的整个范围；否则，指定拆分之外的值将被视为错误。

**转换示例**

此示例获取一列连续功能(`course_duration`)，根据提供的`splits`将其量化，然后将生成的存储桶与其他功能组合在一起。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MinMaxScaler {#minmaxscaler}

`MinMaxScaler`转换器将矢量行数据集中的每个功能重新缩放到指定的范围，通常为[0、1]。 这可确保所有特征对模型的贡献相等。 它尤其适用于对特征缩放敏感的模型，例如基于梯度下降的算法。 `MinMaxScaler`对以下参数进行操作：

- **分钟**：转换的下限，由所有功能共享。 默认值为`0.0`。
- **max**：转换的上限，由所有功能共享。 默认值为`1.0`。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#minmaxscaler).  -->

**数据类型**

- 输入数据类型： `Array[Double]`
- 输出数据类型： `Array[Double]`

**定义**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|--------------------------------------------------------------------------------------------------|------|---------|----------|
| `min` | 转换后的下限，由所有特征共享。 | double | 0.0 | 可选 |
| `max` | 转换后的上限，由所有功能共享。 | double | 1.0 | 可选 |

**转换示例**

此示例转换一组特征，在应用若干其他转换后使用MinMaxScaler将它们重新缩放到指定范围。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling, min_max_scaler(maxScaling) as features)
```

#### MaxAbsScaler {#maxabsscaler}

`MaxAbsScaler`转换器将矢量行数据集中的每个功能重新缩放到范围[-1， 1]，方法是除以每个功能的最大绝对值。 此转换非常适合于保留具有正值和负值的数据集中的稀疏性，因为它不会移动或居中数据。 这使`MaxAbsScaler`特别适合于对输入特征尺度敏感的模型，例如涉及距离计算的模型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#maxabsscaler). -->

**数据类型**

- 输入数据类型： `Array[Double]`
- 输出数据类型： `Array[Double]`

**定义**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|---------------------------------------------------------------------------------------------------------|------|---------|----------|
| 无 | MaxAbsScaler的操作不需要任何附加参数。 | 无 | 无 | 无 |

**转换示例**

此示例应用了包括`MaxAbsScaler`在内的多种转换来重新缩放功能，使其位于[-1， 1]范围内。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, max_abs_scaler(vec_assembler) as maxScaling)
```

#### 规范化器 {#normalizer}

`Normalizer`是一个转换器，它将矢量行数据集中的每个矢量标准化为具有单位范数。 此过程可确保一致的缩放而不改变矢量的方向。 这种变换在依赖于距离测量或其他基于向量的计算的机器学习模型中特别有用，特别是在向量的大小发生显着变化时。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#normalizer) -->

**数据类型**

- 输入数据类型： `array[double]` / `vector[double]`
- 输出数据类型： `vector[double]`

**定义**

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|----------------------------------------------------------------------------------------|---------|---------|----------|
| `p` | 指定用于规范化的`p-norm`（例如，`1-norm`、`2-norm`等）。 | 整数 | 2 | 可选 |

**转换示例**

此示例演示如何使用指定的`p-norm`应用多个转换（包括`Normalizer`）来标准化一组功能。

```sql
TRANSFORM(binarizer(time_spent, 5.0) as binary, bucketizer(course_duration, array(-440.5, 0.0, 150.0, 1000.7)) as buck_features, vector_assembler(array(buck_features, users_count, binary)) as vec_assembler, normalizer(vec_assembler, 3) as normalized)
```

#### QuantileDiscretizer {#quantilediscretizer}

`QuantileDiscretizer`是一个转换器，它将具有连续特征的列转换为捆绑的分类特征，其二进制文件数由`numBuckets`参数决定。 在某些情况下，如果非重复值太少而无法创建足够的数量，则实际存储段数可能小于该指定数。

此转换对于简化连续数据的表示或为更好地处理分类输入的算法做好准备特别有用。

**数据类型**

- 输入数据类型：数值列
- 输出数据类型：数字列（类别）

**定义**

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|--------------|--------------------------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `NUM_BUCKETS` | 数据点分组到的存储段（数量位或类别）的数量。 此数字必须大于或等于2。 | 整数 | 2 | 可选 |

**转换示例**

此示例演示了`QuantileDiscretizer`如何将一列连续功能(`hour`)合并到三个分类存储桶中。

```sql
TRANSFORM(quantile_discretizer(hour, 3) as result)
```

**离散化前后示例**

| ID | 小时 | 结果 |
|---|------|--------|
| 0 | 18.0 | 2.0 |
| 1 | 19.0 | 2.0 |
| 2 | 8.0 | 1.0 |
| 3 | 5.0 | 1.0 |
| 4 | 2.2 | 0.0 |

#### StandardScaler {#standardscaler}

`StandardScaler`是一个转换器，它将矢量行数据集中的每个功能标准化为具有单位标准差和/或平均数零。 这个过程使得数据更适合于假设特征以一致尺度围绕零的算法。 这种转换对于SVM、Logistic回归和神经网络等机器学习模型尤其重要，在这些模型中，未标准化的数据可能导致收敛问题或降低精度。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#standardscaler).  -->

**数据类型**

- 输入数据类型：矢量
- 输出数据类型：矢量

**定义**

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|------------|------------------------------------------------------------------------------------------------------|---------|---------|----------|
| `withStd` | 缩放数据以获得单位标准偏差。 | 布尔 | True | 可选 |
| `withMean` | 在缩放之前使用平均值居中数据。 此选项产生密集输出，因此请谨慎使用稀疏输入。 | 布尔 | False | 可选 |

**转换示例**

此示例演示如何将StandardScaler应用于一组特征，用单位标准偏差和零平均值标准化它们。

```sql
TRANSFORM(standard_scaler(feature) as ss_features)
```

### 分类转换 {#categorical-transformations}

阅读本节内容，了解为机器学习模型转换和预处理分类数据而设计的可用转换器。 这些转换针对的是表示不同类别或标签的数据点，而不是数值。

#### StringIndexer {#stringindexer}

`StringIndexer`是一个转换器，它将标签字符串列编码为数字索引列。 索引范围从0到`numLabels`，并按标签频率排序（最常见的标签收到索引0）。 如果输入列是数字，则在编制索引前会将其转换为字符串。 如果用户指定了不可见标签，则可以将这些标签分配给索引`numLabels`。

此转换对于将分类字符串数据转换为数字形式特别有用，因此它适用于需要数字输入的机器学习模型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stringindexer) -->

**数据类型**

- 输入数据类型：字符串
- 输出数据类型：数字

**定义**

```sql
TRANSFORM(string_indexer(category) as si_category)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|-------------|------|---------|----------|
| 无 | `StringIndexer`不需要任何额外的参数来执行其操作。 | 无 | 无 | 无 |

**转换示例**

此示例演示如何将`StringIndexer`应用于分类功能，并将其转换为数字索引。

```sql
TRANSFORM(string_indexer(category) as si_category)
```

#### OneHotEncoder {#onehotencoder}

`OneHotEncoder`是一个转换器，它将标签索引列转换为稀疏二进制向量列，其中每个向量最多有一个单值。 此编码对于允许需要数值输入的算法（如Logistic回归）有效地合并分类数据特别有用。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#onehotencoder).  -->

**数据类型**

- 输入数据类型：数字
- 输出数据类型： Vector[Int]

**定义**

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|-------------|------|---------|----------|
| 无 | OneHotEncoder的操作不需要任何附加参数。 | 无 | 无 | 无 |

**转换示例**

此示例演示如何首先将`StringIndexer`应用于分类功能，然后使用`OneHotEncoder`将索引值转换为二进制矢量。

```sql
TRANSFORM(string_indexer(category) as si_category, one_hot_encoder(si_category) as ohe_category)
```

### 文本转换 {#textual-transformations}

本节详细介绍可用于处理文本数据并将文本数据转换为机器学习模型可以使用的格式的转换器。 此部分对于处理自然语言数据和文本分析的开发人员至关重要。

#### CountVectorizer {#countvectorizer}

`CountVectorizer`是一个转换器，它将文本文档的集合转换为令牌计数的矢量，基于从语料库中提取的词汇生成稀疏表示。 此转换对于将文本数据转换为机器学习算法(例如LDA（潜在狄利克雷分配）)可以使用的数字格式至关重要，因为它表示每个文档中的令牌频率。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#countvectorizer). -->

**数据类型**

- 输入数据类型：数组[字符串]
- 输出数据类型：密集矢量

**定义**

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|---------|----------|
| `VOCAB_SIZE` | 词汇的最大尺寸。 CountVectorizer生成的词汇只考虑在整个语料中按词频排序的前`vocabSize`个词。 | 整数 | 218 | 可选 |
| `MIN_DOC_FREQ` | 指定术语要包含在词汇中必须出现在中的不同文档的最小数目。 可以是绝对数或文档的小数（如果是双精度类型）。 | 两次 | 1.0 | 可选 |
| `MAX_DOC_FREQ` | 指定术语可以出现在词汇表中的不同文档的最大数目。 可以是绝对数或文档的小数（如果是双精度类型）。 | 两次 | (263)-1 | 可选 |
| `MIN_TERM_FREQ` | 过滤掉文档中的罕见单词。 频率/计数小于给定阈值的术语将被忽略。 可以是文档的令牌计数的绝对数字或小数。 | 两次 | 1.0 | 可选 |

{style="table-layout:auto"}

**转换示例**

此示例演示了CountVectorizer如何将文本数组集合转换为令牌计数的向量，从而生成稀疏表示。

```sql
TRANSFORM(count_vectorizer(texts) as cv_output)
```

**矢量化前后示例**

| ID | 文本 | cv_output |
|----|---------------------------------|-----------------------------------|
| 0 | Array(&quot;a&quot;， &quot;b&quot;， &quot;c&quot;) | (3，[0,1，2]，[1.0,1.0,1.0]) |
| 1 | 数组(“a”、“b”、“b”、“c”、“a”) | (3，[0,1，2]，[2.0,2.0,1.0]) |

{style="table-layout:auto"}

#### NGram {#ngram}

`NGram`是生成n元语法序列的转换器，其中n元语法是某个整数(`𝑛`)的(&#39;??&#39;)令牌序列（通常是词）。 输出由以空格分隔的“??”连续单词字符串组成，这些字符串可用作机器学习模型（特别是侧重于自然语言处理的模型）中的特征。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#n-gram). -->

**数据类型**

- 输入数据类型：数组[字符串]
- 输出数据类型：数组[字符串]

**定义**

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|-----------------------------------------------------------------------------------------------|---------|-------------------|----------|
| `N` | 最小n元组长度，必须大于或等于1。 | 整数 | 2（二进制） | 可选 |

{style="table-layout:auto"}

**转换示例**

此示例演示了NGram转换器如何根据从文本数据派生的令牌列表创建3克序列。

```sql
TRANSFORM(tokenizer(review_comments) as token_comments, ngram(token_comments, 3) as n_tokens)
```

**n-gram转换之前和之后的示例**

| ID | 文本 | n_tokens |
|----|-------------------------------------------------------|-------------------------------------------------------|
| 0 | [&quot;this&quot;、&quot;was&quot;、&quot;an&quot;、&quot;entering&quot;、&quot;movie&quot;] | [“这是”、“是一个娱乐”、“一个娱乐电影”] |

{style="table-layout:auto"}

#### StopWordsRemover {#stopwordsremover}

`StopWordsRemover`是一个转换器，它从字符串序列中删除停用词，过滤掉没有重要意义的常用词。 它将一系列字符串（如Tokenizer的输出）作为输入，并删除由`stopWords`参数指定的所有停用词。

此转换有助于预处理文本数据，通过消除对整体意义贡献不大的单词来提高下游机器学习模型的有效性。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#stopwordsremover) -->

**数据类型**

- 输入数据类型：数组[字符串]
- 输出数据类型：数组[字符串]

**定义**

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|--------------------|--------------------------------------------------------------------------------------------------|---------------|-------------------------|----------|
| `stopWords` | 要过滤掉的单词。 | 数组[字符串] | 默认：英语停用词 | 可选 |

{style="table-layout:auto"}

<!-- Q) should this be the `CUSTOM_STOP_WORDS` parameter or the `stopWords` parameter?  -->

**转换示例**

此示例显示`StopWordsRemover`如何从令牌列表中过滤掉常见的英文停用词。

```sql
TRANSFORM(stop_words_remover(raw) as filtered)
```

**删除停用词前后的示例**

| ID | 原始 | 已筛选 |
|----|------------------------------|--------------------------|
| 0 | [我看见了，红色气球] | [已观看，红色，气球] |
| 1 | [Mary， had， a， little， lamb] | [Mary， little， lamb] |

**带有自定义停用词的示例**

此示例演示如何使用自定义的停用词列表从输入序列中过滤掉特定词。

```sql
TRANSFORM(stop_words_remover(raw, array("red", "I", "had")) as filtered)
```

**删除自定义停用词前后的示例**

| ID | 原始 | 已筛选 |
|----|------------------------------|--------------------------|
| 0 | [我看见了，红色气球] | [看见，气球] |
| 1 | [Mary， had， a， little， lamb] | [Mary， a， little， lamb] |

#### TF-IDF {#tf-idf}

`TF-IDF` （术语频率 — 逆文档频率）是用于测量文档中单词相对于语料库的重要性的转换器。 术语频率(TF)是指术语\(t\)出现在文档\(d\)中的次数，而文档频率(DF)则测量语料库中\(D\)包含术语\(t\)的文档数量。 这种方法在文本挖掘中广泛使用，以减少“a”、“the”和“of”等带有少量唯一信息的常见单词的影响。

此转换在文本挖掘和自然语言处理任务中特别有用，因为它为文档内和整个语料库中的每个单词的重要性分配一个数值。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tf-idf) -->

**数据类型**

- 输入数据类型：数组[字符串]
- 输出数据类型： Vector[Int]

**定义**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------------|----------------------------------------------------------------------------------------|------|---------|----------|
| `NUM_FEATURES` | 要生成的功能数。 必须大于 0 | 整数 | 262144 | 可选 |
| `MIN_DOC_FREQ` | 模型中必须包含术语的最小文档数。 | 整数 | 0 | 可选 |

{style="table-layout:auto"}

**转换示例**

此示例演示了如何使用TF-IDF将标记化的句子转换为特征向量，该向量表示每个术语在整个语料库上下文中的重要性。

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Tokenizer {#tokenizer}

`Tokenizer`是将文本（如句子）划分为单个术语（通常是单词）的转换器。 它将句子转换为令牌数组，为文本预处理提供了一个基本步骤，为进一步的文本分析或建模过程准备数据。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#tokenizer) -->

**数据类型**

- 输入数据类型：文本句子
- 输出数据类型：数组[字符串]

**定义**

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|-----------|-------------|------|---------|----------|
| 无 | `Tokenizer`的操作不需要任何附加参数。 | 无 | 无 | 无 |

**转换示例**

此示例演示了在文本处理管道中，`Tokenizer`如何将句子划分为单个单词（令牌）。

```sql
create table td_idf_model transform(tokenizer(sentence) as token_sentence, tf_idf(token_sentence) as tf_sentence, vector_assembler(array(tf_sentence)) as feature) OPTIONS()
```

#### Word2Vec {#word2vec}

`Word2Vec`是一个估计器，它处理表示文档的词序列并训练`Word2VecModel`。 此模型将每个单词映射到一个唯一的固定大小的矢量上，并通过平均文档中所有单词的矢量将每个文档转换为一个矢量。 `Word2Vec`在自然语言处理任务中广泛使用，它创建可捕获语义含义的单词内嵌，将文本数据转换为表示单词之间关系的数字向量，并实现更有效的文本分析和机器学习模型。

<!-- More information and examples can be found in the [Spark algorithm documentation](https://spark.apache.org/docs/2.2.0/ml-features.html#word2vec) -->

**数据类型**

- 输入数据类型：数组[字符串]
- 输出数据类型：矢量[双精度]

**定义**

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**参数**

| 参数 | 描述 | 类型 | 默认 | 可选 |
|--------------|-----------------------------------------------------------------------------------------------------|---------|---------|----------|
| `VECTOR_SIZE` | 每个单词转换成的向量的维度。 | 整数 | 100 | 可选 |
| `MIN_COUNT` | `Word2Vec`模型的词汇中必须包含令牌的最小次数。 | 整数 | 5 | 可选 |

{style="table-layout:auto"}

**转换示例**

此示例显示`Word2Vec`如何将标记化的审阅转换为表示文档中单词向量的平均值的固定大小的向量。

```sql
TRANSFORM(tokenizer(review) as tokenized, word2Vec(tokenized, 10, 1) as word2Vec)
```

**Word2Vec转换之前和之后的示例**

| 审核 | 标记化 | word2Vec |
|-------------------------------|--------------------------------------|---------------------------------|
| 这是部有趣的电影 | [这个，曾经是个，娱乐性的，电影] | [-0.025713888928294182，0.00818799751577899，0.0092235435731709，-0.01515385233797133，0.012175946310162545，3.1129065901041035E-4,0.0025145105042611252，0.005757019785232843，-0.021328244300093502，0.009335877187550069] |

{style="table-layout:auto"}
