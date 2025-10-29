---
title: 使用基于SQL的Logistic回归预测客户流失
description: 了解如何使用基于SQL的Logistic回归预测客户流失。 本指南涵盖从模型创建到评估和预测的整个过程。 从客户购买行为中获得切实可行的洞察，以实施主动保留策略并优化业务决策。
exl-id: 3b18870d-104c-4dce-8549-a6818dc40d24
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 1%

---

# 使用基于SQL的Logistic回归预测客户流失

预测客户流失有助于企业通过切实可行的洞察力提高满意度和忠诚度，从而保留客户、优化资源并提高盈利能力。

了解如何使用基于SQL的Logistic回归来预测客户流失。 使用本全面的SQL指南，根据关键行为量度（如购买频率、平均订单值和上次购买间隔时间），将原始电子商务数据转换为有意义的客户洞察。 本文档介绍了从数据准备、特征工程到模型创建、评估和预测的整个过程。

使用本指南构建强大的客户流失预测模型，该模型可识别存在风险的客户、优化保留策略并推动更好的业务决策。 它包括分步说明、SQL查询和详细解释，以帮助您放心地在数据环境中应用机器学习技术。

## 快速入门

在创建流失模型之前，请务必探索关键客户功能和数据要求。 以下各节概述了准确模型训练所需的基本客户属性和必需数据字段。

### 定义客户功能 {#define-customer-features}

为了对客户流失进行准确分类，该模型分析了客户购买习惯和趋势。 下表概述了模型中使用的关键客户行为功能：

| 功能 | 描述 |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | 客户进行的购买总数。 |
| `total_revenue` | 客户购买产生的总收入。 |
| `avg_order_value` | 客户购买的平均值。 |
| `customer_lifetime` | 客户首次购买与上次购买之间的间隔天数。 |
| `days_since_last_purchase` | 自客户上次购买以来的天数。 |
| `purchase_frequency` | 客户进行购买的不同月份数。 |

### 假设和必填字段 {#assumptions-required-fields}

要生成客户流失预测，该模型依赖于`webevents`表中捕获客户事务详细信息的关键字段。 您的数据集必须包含以下字段：

| 字段 | 描述 |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | 用于跨会话跟踪客户的唯一标识符。 |
| `productListItems.priceTotal[0]` | 每笔交易记录的采购物料总成本。 |
| `productListItems.quantity[0]` | 购买中的项目总数。 |
| `timestamp` | 每个购买事件的确切日期和时间。 |
| `commerce.order.purchaseID` | 用于确认已完成购买的必需值。 |

数据集必须包含结构化历史客户交易记录，其中每一行表示一个购买事件。 每个事件都必须包含与SQL `DATEDIFF`函数兼容的适当日期时间格式的时间戳（例如，YYYY-MM-DD HH:MI:SS）。 此外，每个记录都必须在`ECID`字段中包含有效的Experience Cloud ID (`identityMap`)，以唯一标识客户。

>[!TIP]
>
>处理具有数百万条记录的大型数据集可能会显着影响性能。 要优化查询执行，请按照时间戳对体验数据集进行分区，使用快照执行增量处理，并根据需要应用高效的聚合函数。 此外，在聚合之前过滤数据，以减少处理开销。

## 创建模型 {#create-a-model}

要预测客户流失，您必须创建一个基于SQL的Logistic回归模型，以分析客户购买历史记录和行为量度。 该模型通过确定客户在过去90天内是否进行了购买而将客户分类为`churned`或`not churned`。

### 使用SQL创建流失预测模型 {#sql-create-model}

基于SQL的模型通过聚合关键量度并根据90天不活动规则分配流失标签来处理`webevents`数据。 这种方法将活跃客户与高风险客户区分开来。 SQL查询还执行特征工程以提高模型准确性并改进流失分类。 这些洞察力使您的企业能够实施有针对性的保留策略，减少流失，并最大化客户存留期价值。

>[!NOTE]
>
>客户流失预测模型使用90天的默认阈值将客户归类为已流失。 要调整此阈值以符合您的业务目标和保留策略，请修改SQL查询中的`DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90`条件。

使用以下SQL语句创建具有指定功能和标签的`retention_model_logistic_reg`模型：

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### 模型输出 {#model-output}

输出数据集包含与客户相关的量度及其流失状态。 每一行表示一个客户、其功能值及其流失状态。 您可以使用此输出分析客户行为、培训预测模型并制定有针对性的保留策略来保留有风险的客户。 下面显示了一个输出表示例：

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
|--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| 列 | 描述 |
|-----------|------------------------------------------------------------------------------------|
| `churned` | 该值指示客户是否在过去90天内进行了购买（0 =未流失，1 =流失）。 |

## 使用SQL评估模型 {#model-evaluation}

接下来，评估流失预测模型，以确定其在识别风险客户方面的有效性。 使用测量准确性和可靠性的关键指标评估模型性能。

要测量`retention_model_logistic_reg`模型在预测客户流失方面的准确性，请使用`model_evaluate`函数。 以下SQL示例使用与训练数据类似的数据集来评估模型：

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### 模型评估输出

评估输出包括AUC-ROC、准确性、精确度和召回率等关键性能指标。 这些量度可让您深入了解模型有效性，以便用于完善保留策略并做出数据驱动型决策。

>[!NOTE]
>
>性能值介于0到1之间，其中1.0表示完美性能。

```console
 auc_roc | accuracy | precision | recall 
|---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| 量度 | 描述 |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | 此量度表示模型区分流失客户和非流失客户的能力。 值越接近1表示性能越高。 |
| `accuracy` | 准确性量度表示正确预测的比例，提供了模型性能的整体衡量。 |
| `precision` | 精度表示正确识别的流失客户所占的比例，并指示流失预测中的可靠性。 高值表示误报更少。 |
| `recall` | 召回率衡量模型识别所有实际客户流失的能力。 高召回值表示缺少的流失客户更少。 |

>[!NOTE]
>
>本示例中的近乎完美的分数用于演示目的。 在实践中，由于噪声和可变性，真实数据可能会产生较低的值。

## 模型预测 {#model-prediction}

评估模型后，使用`model_predict`将其应用到新数据集并预测客户流失。 您可以使用这些预测来识别存在风险的客户，并实施有针对性的保留策略。

### 使用SQL生成流失预测 {#sql-model-predict}

以下SQL查询使用`retention_model_logistic_reg`模型预测客户流失，并使用与训练数据类似的数据集结构：

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### 模型预测输出 {#prediction-output}

输出数据集包括关键客户功能及其预测的流失状态，这指示客户是否有可能流失。 利用这些见解实施主动保留策略并减少客户流失。

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
|-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| 列 | 描述 |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | 基于模型的客户预测客户流失状态（0 =未流失，1 =流失）。 |

## 后续步骤

您现在已经了解如何创建、评估和使用基于SQL的模型来预测客户流失。 利用此基础，您可以分析客户行为，识别存在风险的客户，并实施主动保留策略以提高客户保留率。 要进一步增强和应用流失预测模型，请考虑以下步骤：

- 自动化该流程：将模型集成到数据管道中，以进行持续监控和实时洞察。 [了解如何使用SQL](../../../dashboards/query.md)验证和处理数据集。
- 监控模型性能：使用新数据持续评估模型，以保持准确性和相关性。  在Adobe Experience Platform UI中使用[AI助手](../../../ai-assistant/landing.md)来监视关键性能变化和[预测受众趋势](../../../ai-assistant/new-features/audience-forecasting.md)。
