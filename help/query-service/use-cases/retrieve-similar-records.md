---
title: 使用高阶函数检索类似记录
description: 了解如何基于相似性量度和相似性阈值，从一个或多个数据集识别和检索相似或相关记录。 此工作流可突出显示不同数据集之间的有意义的关系或重叠。
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# 使用高阶函数检索类似记录

使用Data Distiller高阶函数解决各种常见用例。 要识别一个或多个数据集的类似或相关记录并进行检索，请使用本指南中详述的过滤器、转换和缩减函数。 要了解如何使用高位函数处理复杂的数据类型，请参阅关于如何[管理数组并映射数据类型](../sql/higher-order-functions.md)的文档。

使用本指南可以识别来自不同数据集的产品，这些产品在其特征或属性方面具有显着相似性。 此方法为以下方面提供了解决方案：重复数据删除、记录链接、推荐系统、信息检索、文本分析等。

该文档描述了相似度连接的实现过程，然后使用Data Distiller的高阶函数计算数据集之间的相似度并根据选定的属性过滤它们。 为过程的每个步骤提供了SQL代码段和解释。 工作流使用Jaccard相似性度量实现相似性连接，使用Data Distiller高阶函数进行标记化。 然后使用这些方法基于相似性度量从一个或多个数据集识别和检索相似或相关的记录。 该过程的关键部分包括：[使用更高阶函数的tokenization](#data-transformation)、[唯一元素交叉联接](#cross-join-unique-elements)、[Jaccard相似度计算](#compute-the-jaccard-similarity-measure)以及[基于阈值的筛选](#similarity-threshold-filter)。

## 先决条件

在继续阅读本文档之前，您应该熟悉以下概念：

- **相似性联接**&#x200B;是一种操作，它根据记录之间的相似性度量从一个或多个表中标识和检索记录对。 相似连接的主要要求如下：
   - **相似性量度**：相似性连接依赖于预定义的相似性量度或量度。 这些度量包括：Jaccard相似度、余弦相似度、编辑距离等。 量度取决于数据的性质和用例。 此量度量化了两个记录的相似或异同。
   - **阈值**：使用相似性阈值来确定两个记录何时被视为相似到足以包含在连接结果中。 相似度分数高于阈值的记录被视为匹配。
- **Jaccard相似度**&#x200B;指标，即Jaccard相似性度量，是用来衡量样本集相似性和多样性的统计量。 它定义为交集的大小除以样本集的并集的大小。 Jaccard相似性度量的范围从0到1。 Jaccard相似度为零表示集合之间没有相似性，Jaccard相似度为1表示集合相同。
  ![一个维恩图以说明Jaccard相似性度量。](../images/use-cases/jaccard-similarity.png)
- **数据Distiller中的高阶函数**&#x200B;是动态的内联工具，可直接在SQL语句中处理和转换数据。 这些通用函数消除了数据操作中多个步骤的需要，尤其是当[处理复杂类型（如数组和映射](../sql/higher-order-functions.md)）时。 通过提高查询效率和简化转换，高阶函数有助于在各种业务情景下更灵活地分析和更好地决策。

## 快速入门

需要数据Distiller SKU才能对Adobe Experience Platform数据执行更高阶的功能。 如果您没有Data Distiller SKU，请联系您的Adobe客户服务代表以了解更多信息。

## 建立相似性 {#establish-similarity}

此用例需要文本字符串之间的相似性度量，以后可以使用该度量来建立用于过滤的阈值。 在此示例中，集A和集B中的产品表示两个文档中的单词。

Jaccard相似性度量可以应用于广泛的数据类型，包括文本数据、分类数据和二进制数据。 它同样适用于实时或批量处理，因为对于大型数据集的计算是高效的。

产品集A和产品集B包含此工作流的测试数据。

- 产品集A： `{iPhone, iPad, iWatch, iPad Mini}`
- 产品集B： `{iPhone, iPad, Macbook Pro}`

要计算产品集A和B之间的Jaccard相似度，首先要找到产品集的&#x200B;**交集**（公共元素）。 在这种情况下，`{iPhone, iPad}`。 接下来，查找两个产品集的&#x200B;**union**（所有唯一元素）。 在此示例中，`{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`。

最后，使用Jaccard相似度公式`J(A,B) = A∪B / A∩B`计算相似度。

J =雅卡距离
A =设置1
B =设置2

产品集A和B之间的Jaccard相似度为0.4。这表示两个文档中使用的单词之间具有中等程度的相似性。 这两个集之间的这种相似性定义了相似性连接中的列。 这些列表示存储在表中并用于执行相似性计算的信息段或与数据相关联的特征。

### 基于字符串相似度的成对Jaccard计算 {#pairwise-similarity}

为了更准确地比较字符串之间的相似度，必须计算字符串之间的配对相似度。 两两相似性将高维对象分割成较小维对象以供比较和分析。 为此，文本字符串将分成更小的部分或单位（令牌）。 它们可以是单个字母、字母组（如音节）或整个单词。 计算集合A中每个元素与集合B中每个元素之间的每对令牌的相似度。此标记化为从数据中提取分析和计算比较、关系和见解奠定了基础。

对于配对相似度计算，此示例使用字符双图（两个字符令牌）来比较集合A和集合B中产品的文本字符串之间的相似度匹配。双元格是给定序列或文本中两个项目或元素的连续序列。 你可以将它推广到n克。

此示例假定大小写无关紧要，并且不应计入空格。 根据这些标准，集A和集B具有以下双图：

产品集A双克：

- iPhone(5)： “ip”、“ph”、“ho”、“on”、“ne”
- iPad (3)： “ip”、“pa”、“ad”
- iWatch (5)： “iw”、“wa”、“at”、“tc”、“ch”
- iPad Mini (7)： “ip”、“pa”、“ad”、“dm”、“mi”、“in”、“ni”

产品集B双克：

- iPhone(5)： “ip”、“ph”、“ho”、“on”、“ne”
- iPad (3)： “ip”、“pa”、“ad”
- Macbook Pro (9)： “Ma”、“ac”、“cb”、“bo”、“oo”、“ok”、“kp”、“pr”、“ro”

接下来，计算每对图像的Jaccard相似系数：

|                   | iPhone（设置B） | iPad（设置B） | Macbook Pro（设置B） |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone（设置A） | （交集：5，并集：5） = 5 / 5 = 1 | （交集：1，并集：7） =1 / 7 ≈ 0.14 | （交集：0，并集：14） = 0 / 14 = 0 |
| iPad（设置A） | （交集：1，并集：7） = 1 / 7 ≈ 0.14 | （交集：3，并集：3） = 3 / 3 = 1 | （交集：0，并集：12） = 0 / 12 = 0 |
| iWatch（设置A） | （交集：0，并集：8） = 0 / 8 = 0 | （交集：0，并集：8） = 0 / 8 = 0 | （交集：0，并集：8） = 0 / 8 =0 |
| iPad Mini（设置A） | （交集：1，并集：11） = 1 / 11 ≈ 0.09 | （交集：3，并集：7） = 3 / 7 ≈ 0.43 | （交集：0，并集：16） = 0 / 16 = 0 |

{style="table-layout:auto"}

## 使用SQL创建测试数据 {#create-test-data}

要手动创建产品集的测试表，请使用SQL CREATE TABLE语句。

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

以下描述提供了上述SQL代码块的划分：

- 第1行： `CREATE TEMP TABLE featurevector1 AS`：此语句创建名为`featurevector1`的临时表。 临时表通常只能在当前会话中访问，并且会在会话结束时自动删除。
- 第1行和第2行： `SELECT * FROM (...)`：此部分代码是用于生成插入到`featurevector1`表中的数据的子查询。
在子查询中，使用`UNION ALL`命令合并多个`SELECT`语句。 每个`SELECT`语句都生成一行数据，这些数据具有为`ProductName`列指定的值。
- 第3行： `SELECT 'iPad' AS ProductName`：这将在`ProductName`列中生成值为`iPad`的行。
- 第5行： `SELECT 'iPhone'`：这将在`ProductName`列中生成值为`iPhone`的行。

SQL语句创建一个表，如下所示：

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

要创建第二个特征向量，请使用以下SQL语句：

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## 数据转换 {#data-transformation}

在此示例中，必须执行若干操作才能准确地比较集合。 首先，在特征向量中去除所有空格，假定这些空格对相似性度量没有贡献； 然后，去除特征向量中存在的任何重复项，因为它们浪费了计算处理。 然后，从特征向量中提取两个字符（双图）的令牌。 在本例中，假设它们重叠。

>[!NOTE]
>
>为了便于说明，将在每个步骤的特征向量旁添加已处理的列。

以下部分说明了在开始标记化过程之前先进行的数据转换（如重复数据删除、去除空格和小写转换）。

### 删除重复项 {#deduplication}

接下来，使用`DISTINCT`子句删除重复项。 此示例中没有重复项，但这是提高任何比较准确性的重要步骤。 下面显示了必要的SQL：

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### 去除空格 {#whitespace-removal}

在以下SQL语句中，从特征向量中删除空格。 查询的`replace(ProductName, ' ', '') AS featurevector1_nospaces`部分从`featurevector1`表中获取`ProductName`列并使用`replace()`函数。 `REPLACE`函数将所有出现的空格(“ ”)替换为空字符串(“)。 这会有效地从`ProductName`值中删除所有空格。 结果别名为`featurevector1_nospaces`。

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

结果如下表所示：

|   | featurevector1_distinct | featurevector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

下面显示了SQL语句及其在第二个特征向量上的结果：

+++选择以展开

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

结果如下所示：

|   | featurevector2_distinct | featurevector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### 转换为小写 {#lowercase-conversion}

接下来，对SQL进行了改进，将产品名称转换为小写并删除所有空格。 下层函数(`lower(...)`)应用于`replace()`函数的结果。 lower函数将修改后的`ProductName`值中的所有字符转换为小写。 这可以确保值为小写，而不管它们的原始大小写如何。

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

此语句的结果为：

|   | featurevector1_distinct | 特征向量1_转换 |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

下面显示了SQL语句及其在第二个特征向量上的结果：

+++选择以展开

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

结果如下所示：

|   | featurevector2_distinct | 特征向量2_转换 |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### 使用SQL提取令牌 {#tokenization}

下一步是标记化或文本拆分。 标记化是将文本拆分为各个术语的过程。 通常，这包括将句子拆分为单词。 在此示例中，通过使用SQL函数（如`regexp_extract_all`）提取令牌，将字符串划分为双格（和高阶n格）。 必须为有效的标记化生成重叠的双向图。

SQL已进一步改进为使用`regexp_extract_all`。 `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:`此部分查询进一步处理在上一步中创建的修改的`ProductName`值。 它使用`regexp_extract_all()`函数从修改的小写`ProductName`值中提取一到两个字符的所有非重叠子字符串。 `.{2}`正则表达式模式与长度为两个字符的子字符串匹配。 函数的`regexp_extract_all(..., '.{2}', 0)`部分随后从输入文本中提取所有匹配的子字符串。

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

结果如下表所示：

+++选择以展开

|   | featurevector1_distinct | 特征向量1_转换 | 令牌 |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;，&quot;ad&quot;，&quot;mi&quot;，&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;，&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;，&quot;at&quot;， &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;，&quot;ho&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

要进一步提高准确性，必须使用SQL创建重叠令牌。 例如，上面的“iPad”字符串缺少“pa”令牌。 要解决此问题，请将lookahead运算符（使用`substring`）移动一步，并生成双图。

与上一步类似，`regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):`从修改的产品名称中提取双字符序列，但使用`substring`方法从第二个字符开始创建重叠令牌。 接下来，在第3-7行(`array_union(...) AS tokens`)中，`array_union()`函数将两个正则表达式提取得到的双字符序列的数组组合在一起。 这可确保结果包含来自非重叠和重叠序列的唯一令牌。

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

结果如下表所示：

+++选择以展开

|   | featurevector1_distinct | 特征向量1_转换 | 令牌 |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;，&quot;ad&quot;，&quot;mi&quot;，&quot;ni&quot;，&quot;pa&quot;，&quot;dm&quot;，&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;，&quot;ad&quot;，&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;，&quot;at&quot;，&quot;ch&quot;，&quot;wa&quot;，&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;，&quot;ho&quot;，&quot;ne&quot;，&quot;ph&quot;，&quot;on&quot;} |

{style="table-layout:auto"}

+++

但是，使用`substring`作为问题的解决方案存在限制。 如果从文本中生成基于三元组的令牌（三个字符），则需要使用两个`substrings`来回顾两次，以获取所需的班次。 要制造10克，您需要九个`substring`表达式。 这会使代码膨胀，变得不可持续。 使用纯正则表达式是不合适的。 我们需要新方法。

### 调整产品名称的长度 {#length-adjustment}

SQl可以通过序列和长度函数进行改进。 在下面的示例中，`sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)`生成一个数字序列，从1到修改的产品名称的长度减去3。 例如，如果修改后的产品名称为字符长度为8的“ipadmini”，则会生成从1到5(8-3)的数字。

下面的语句提取唯一的产品名称，然后将每个名称划分为四个字符长度的字符（令牌）序列（不包括空格），并将它们显示为两列。 其中一列显示唯一的产品名称，另一列显示其生成的令牌。

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

结果如下表所示：

+++选择以展开

|   | featurevector1_distinct | 令牌 |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;，&quot;padm&quot;，&quot;admi&quot;，&quot;dmin&quot;，&quot;mini&quot;} |
| 2 | iPad | {“ipad”} |
| 3 | iWatch | {&quot;iwat&quot;，&quot;watc&quot;，&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;，&quot;phon&quot;，&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### 确保设置令牌长度 {#ensure-set-token-length}

可以将其他条件添加到语句中，以确保生成的序列具有特定长度。 以下SQL语句通过使`transform`函数更复杂而扩展了令牌生成逻辑。 该语句使用`transform`中的`filter`函数以确保生成的序列长度为6个字符。 它通过将NULL值指定给这些职位来处理不可能出现的情况。

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

结果如下表所示：

+++选择以展开

|   | featurevector1_distinct | 令牌 |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;，&quot;padmin&quot;，&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {“iwatch”} |
| 4 | iPhone | {“iphone”} |

{style="table-layout:auto"}

+++

## 使用Data Distiller高阶函数探索解决方案 {#higher-order-function-solutions}

高阶函数是功能强大的构造，允许您实现“编程”，如Data Distiller中的语法。 它们可用于对数组中的多个值迭代函数。

在数据Distiller的上下文中，高阶函数非常适合于创建n元组和字符序列迭代。

`reduce`函数（尤其是在`transform`生成的序列中使用）提供了导出累计值或汇总的方法，这些值或汇总在各种分析和计划流程中可能至关重要。

例如，在下面的SQl语句中，`reduce()`函数使用自定义聚合器聚合数组中的元素。 它模拟for循环以&#x200B;**创建所有整数**&#x200B;从1到5的累积和。`1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`。

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

以下是对SQL语句的分析：

- 第1行： `transform`对序列中生成的每个元素应用函数`x -> reduce`。
- 第2行： `sequence(1, 5)`生成从1到5的数字序列。
- 行3： `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)`对序列（从1到5）中的每个元素x执行缩减操作。
   - `reduce`函数采用初始累加器值0、从1到当前值`x`的顺序，以及高阶函数`(acc, y) -> acc + y`来添加数字。
   - 高阶函数`acc + y`通过将当前值`y`加到累加器`acc`来累加总和。
- 第8行： `AS sum_result`将结果列重命名为sum_result。

总而言之，此高阶函数采用两个参数（`acc`和`y`）并定义要执行的操作，在此例中，该操作将`y`添加到累加器`acc`。 在缩减过程中，为序列中的每个元素执行此高阶函数。

此语句的输出是单列(`sum_result`)，其中包含从1到5的数字的累积和。

### 高阶函数的值 {#value-of-higher-order-functions}

本节将分析三元组SQL语句的精简版本，以更好地了解Data Distiller中高位函数的值，从而更有效地创建n元组。

以下语句对`featurevector1`表中的`ProductName`列进行操作。 它使用从生成的序列获得的位置，生成从表中的修改的产品名称派生的一组三个字符的子字符串。

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

以下是对SQL语句的分析：

- 第2行： `transform`将更高阶函数应用于序列中的每个整数。
- 第3行： `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)`生成从`1`到修改的产品名称长度减二的整数序列。
   - `length(lower(replace(ProductName, ' ', '')))`在将`ProductName`设为小写并删除空格后计算其长度。
   - `- 2`从长度中减去两个，以确保序列为3个字符的子字符串生成有效的起始位置。 减去2可确保在每个起始位置之后有足够的字符来提取由3个字符组成的子字符串。 此处的子字符串函数的操作方式类似于lookahead运算符。
- 第4行： `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)`是一个对生成序列中的每个整数`i`运行的高阶函数。
   - `substring(...)`函数从`ProductName`列中提取3个字符的子字符串。
   - 在提取子字符串之前，`lower(replace(ProductName, ' ', ''))`将`ProductName`转换为小写并删除空格以确保一致性。

输出是长度为三个字符的子字符串的列表，基于序列中指定的位置从修改的产品名称中提取。

## 筛选结果 {#filter-results}

`filter`函数具有后续[数据转换](#data-transformation)，允许从文本数据中提取更细致、更精确的相关信息。 这使您能够获取见解、提高数据质量并促进更好的决策过程。

以下SQL语句中的`filter`函数用于优化和限制字符串中的位置序列，使用后续转换函数从字符串中提取子字符串。

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

`filter`函数在修改的`ProductName`内生成有效起始位置的序列，并提取特定长度的子字符串。 仅允许提取由7个字符组成的子字符串的起始位置。

条件`i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))`确保起始位置`i`加上`6`（所需七字符子字符串的长度减一）不超过修改后的`ProductName`的长度。

`CASE`语句用于根据其长度有条件地包含或排除子字符串。 仅包含7个字符的子字符串；其他子字符串将替换为NULL。 然后，`transform`函数使用这些子字符串从`featurevector1`表中的`ProductName`列创建子字符串序列。

>[!TIP]
>
>您可以使用[参数化模板](../ui/parameterized-queries.md)功能在查询中重复使用和抽象逻辑。 例如，在构建通用实用程序函数（如上面显示的用于标记字符串的函数）时，可以使用字符数为参数的Data Distiller参数化模板。

## 计算两个特征向量间唯一元素的交叉连接 {#cross-join-unique-elements}

根据数据的特定转换确定两个数据集之间的差异或差异是维护数据准确性、提高数据质量和确保数据集之间一致性的常用过程。

下面的SQL语句在应用转换后提取`featurevector2`中存在，但`featurevector1`中不存在唯一的产品名称。

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>除了`EXCEPT`之外，您还可以根据您的用例使用`UNION`和`INTERSECT`。 此外，还可以尝试使用`ALL`或`DISTINCT`子句以查看包括所有值和仅返回指定列的唯一值之间的差异。

结果如下表所示：

+++选择以展开

|   | lower(replace(ProductName， &#39;， &quot;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

接下来，执行交叉连接以组合来自两个特征向量的元素，以创建元素对以进行比较。 此流程的第一步是创建标记化的矢量。

标记化矢量是文本数据的结构化表示，其中每个单词、短语或意义单位（标记）被转换为数字格式。 这种转换允许自然语言处理算法理解和分析文本信息。

下面的SQl创建一个标记化的矢量。

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>如果使用[!DNL DbVisualizer]，则在创建或删除表后，请刷新数据库连接，以便刷新表的元数据缓存。 数据Distiller不推送元数据更新。

结果如下表所示：

+++选择以展开

|   | featurevector1_distinct | 令牌 |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 3 | iWatch | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

然后对`featurevector2`重复该过程：

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

结果如下表所示：

+++选择以展开

|   | featurevector2_distinct | 令牌 |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

在两个标记化矢量都完成后，您现在可以创建交叉连接。 下面的SQL中显示了这一点：

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

以下是用来创建交叉连接的SQl的概要：

- 第2行： `A.featurevector1_distinct AS SetA_ProductNames`从表`A`中选择`featurevector1_distinct`列并为其分配别名`SetA_ProductNames`。 SQL的此部分将生成第一个数据集中不同产品名称的列表。
- 第4行： `A.tokens AS SetA_tokens1`从表或子查询`A`中选择`tokens`列并为其分配别名`SetA_tokens1`。 SQL的此部分会生成与第一个数据集中的产品名称关联的标记化值列表。
- 第8行： `CROSS JOIN`操作将合并两个数据集中所有可能的行组合。 换句话说，它将第一个表中的每个产品名称及其关联的令牌与第二个表(`B`)中的每个产品名称及其关联的令牌配对。 `A`这将生成两个数据集的笛卡尔乘积，其中，输出中的每一行表示两个数据集的产品名称及其关联令牌的组合。

结果如下表所示：

+++选择以展开

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |
| 7 | iWatch | ipad | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 8 | iWatch | macbookpro | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 9 | iWatch | iphone | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## 计算Jaccard相似性度量 {#compute-the-jaccard-similarity-measure}

然后，计算使用Jaccard相似度系数，通过比较两组产品名称之间的标记表示来进行相似度分析。 以下SQL脚本的输出提供了以下内容：两个集合中的产品名称、其令牌化表示形式、公共令牌和唯一令牌总数的计数，以及每对数据集已计算的Jaccard相似度系数。


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

以下是用于计算Jaccard相似系数的SQL的摘要：

- 第6行： `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count`计算`SetA_tokens1`和`SetB_tokens2`共用的令牌数量。 该计算是通过计算两个令牌阵列相交的大小来实现的。
- 第7行： `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count`计算`SetA_tokens1`和`SetB_tokens2`中的唯一令牌总数。 此行计算两个令牌数组的并集的大小。
- 第8-10行： `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity`计算令牌集之间的Jaccard相似度。 这些行将令牌交集的大小除以令牌并集的大小，并将结果四舍五入到两位小数。 结果是一个介于0和1之间的值，其中1表示完全相似性。

结果如下表所示：

+++选择以展开

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Jaccard相似性 |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 3 | 7 | 0.43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 16 | 0.0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;，&quot;dm&quot;，&quot;mi&quot;，&quot;in&quot;，&quot;ni&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 1 | 11 | 0.09 |
| 4 | ipad | ipad | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 3 | 3 | 1.0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 12 | 0.0 |
| 6 | ipad | iphone | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 1 | 7 | 0.14 |
| 7 | iWatch | ipad | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 0 | 8 | 0.0 |
| 8 | iWatch | macbookpro | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 14 | 0.0 |
| 9 | iWatch | iphone | {&quot;iw&quot;，&quot;wa&quot;，&quot;at&quot;，&quot;tc&quot;，&quot;ch&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 0 | 10 | 0.0 |
| 10 | iphone | ipad | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;pa&quot;，&quot;ad&quot;} | 1 | 7 | 0.14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ma&quot;，&quot;ac&quot;，&quot;cb&quot;，&quot;bo&quot;，&quot;ooo&quot;，&quot;ok&quot;，&quot;kp&quot;，&quot;pr&quot;，&quot;ro&quot;} | 0 | 14 | 0.0 |
| 12 | iphone | iphone | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | {&quot;ip&quot;，&quot;ph&quot;，&quot;ho&quot;，&quot;on&quot;，&quot;ne&quot;} | 5 | 5 | 1.0 |

{style="table-layout:auto"}

+++

## 基于Jaccard相似度阈值的筛选结果 {#similarity-threshold-filter}

最后，根据预先定义的阈值对结果进行筛选，仅选择符合相似准则的相似对。 下面的SQL语句筛选Jaccard相似系数至少为0.4的产品。这缩小了结果的范围，使结果成为具有相当程度相似性的配对。

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

此查询的结果提供了相似性连接的列，如下所示：

+++选择以展开

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++：

### 后续步骤 {#next-steps}

通过阅读本文档，您现在可以使用此逻辑来突出显示不同数据集之间有意义的关系或重叠。 从不同数据集中识别具有显着相似性的产品特征或属性的能力在现实世界中有着众多应用。 此逻辑可用于以下场景：

- 产品匹配：对客户分组或推荐类似产品。
- 数据清理：提高数据质量。
- 购物篮分析：分析客户行为、偏好和潜在的交叉销售机会。

如果您尚未这样做，则建议阅读[AI/ML功能管道概述](../data-distiller/ml-feature-pipelines/overview.md)。 使用该概述了解Data Distiller和您的首选机器学习如何构建自定义数据模型，以支持带有Experience Platform数据的营销用例。
