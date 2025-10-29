---
title: 使用统计和机器学习进行机器人过滤
description: 了解如何使用Data Distiller统计和机器学习来识别和过滤机器人活动，以确保准确分析并改进数据完整性。
exl-id: 30d98281-7d15-47a6-b365-3baa07356010
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# 使用统计和机器学习进行机器人过滤

机器人滤波的实际应用跨越了各个行业。 在电子商务中，它提高了转化率指标的可靠性，新闻网站可以从减少虚假参与指标中受益，广告网络可以确保公平计费。 要维护准确的分析并确保点击流或Web流量数据中的数据完整性，您必须解决机器人活动问题。 通过使用Data Distiller实施有效的机器人过滤并消除不需要的流量，您可以确保高质量的分析数据。

本文档提供了使用SQL和机器学习技术识别和过滤机器人活动的全面指南。 它展示了一系列互补方法，从基本过滤开始，推进到基于机器学习的检测和评估。 采用这种强大的框架来增强机器人检测并维护数据完整性。

## 了解机器人活动 {#understand-bot-activity}

通过检测特定时间间隔内用户操作的峰值，可以识别机器人活动。 例如，单个用户在较短时间范围内执行过多点击可能表示机器人行为。 机器人过滤中使用的两个关键属性是：

- **ECID (Experience Cloud访客ID)：**&#x200B;用于标识访客的通用、永久性ID。
- **时间戳：**&#x200B;网站上发生活动的时间和日期。

以下示例演示了如何使用SQL和机器学习技术来识别、优化和预测机器人活动。 使用这些方法可提高数据完整性并确保分析可操作性。

## 基于SQL的机器人筛选 {#sql-based-bot-filtering}

此基于SQL的机器人过滤示例演示了如何使用SQL查询定义阈值并根据预定义的规则检测机器人活动。 这种基本方法通过消除异常活动来帮助识别Web流量中的异常。 通过自定义具有定义的阈值和间隔的检测规则，您可以有效地定制机器人过滤以适合您的特定流量模式。

### 定义机器人活动的阈值 {#define-thresholds}

首先分析您的数据集以识别和分类用户行为。 将焦点集中在ECID、时间戳和`webPageDetails.name`（所访问网页的名称）等属性上，以对用户操作进行分组并检测指示机器人活动的模式。

下面的SQL查询演示了如何应用一分钟内点击超过60次的阈值来识别可疑活动：

```sql
SELECT *
FROM analytics_events_table
WHERE enduserids._experience.ecid NOT IN (
    SELECT enduserids._experience.ecid
    FROM analytics_events_table
    GROUP BY Unix_timestamp(timestamp) / 60, enduserids._experience.ecid
    HAVING Count(*) > 60
);
```

### 展开到多个间隔 {#expand-to-multiple-intervals}

接下来，为阈值定义不同的时间间隔。 这些间隔可能包括：

- **1分钟间隔：**&#x200B;最多60次点击。
- **5分钟间隔：**&#x200B;最多300次点击。
- **30分钟间隔：**&#x200B;最多1800次点击。

以下SQL查询创建一个名为`analytics_events_clicks_count_criteria`的视图来处理多个间隔的阈值。 该语句将1分钟、5分钟和30分钟间隔的点击计数合并到一个结构化数据集中，并根据预定义的阈值标记潜在的机器人活动。

```sql
CREATE VIEW analytics_events_clicks_count_criteria as  
SELECT struct (
        cast(count_1_min AS int) one_minute,
        cast(count_5_mins AS int) five_minute,
        cast(count_30_mins AS int) thirty_minute
       ) count_per_id,
       id,
      struct (
        struct (name) webpagedetails
      ) web,
      CASE
        WHEN count.one_minute > 50 THEN 1
        ELSE 0
      END AS isBot
FROM (
  SELECT table_count_1_min.mcid AS id,
         count_1_min,
         count_5_mins,
         count_30_mins,
         table_count_1_min.name AS name
  FROM (
      (SELECT mcid, Max(count_1_min) AS count_1_min, name
       FROM (SELECT enduserids._experience.mcid.id AS mcid,
                    Count(*) AS count_1_min,
                    web.webPageDetails.name AS name
             FROM delta_table
             WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                               AND TO_TIMESTAMP('2019-09-01 23:00:00')
             GROUP BY UNIX_TIMESTAMP(timestamp) / 60,
                      enduserids._experience.mcid.id,
                      web.webPageDetails.name)
       GROUP BY mcid, name) AS table_count_1_min
       LEFT JOIN
       (SELECT mcid, Max(count_5_mins) AS count_5_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_5_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 300,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_5_mins
       ON table_count_1_min.mcid = table_count_5_mins.mcid
       LEFT JOIN
       (SELECT mcid, Max(count_30_mins) AS count_30_mins, name
        FROM (SELECT enduserids._experience.mcid.id AS mcid,
                     Count(*) AS count_30_mins,
                     web.webPageDetails.name AS name
              FROM delta_table
              WHERE TIMESTAMP BETWEEN TO_TIMESTAMP('2019-09-01 00:00:00')
                                AND TO_TIMESTAMP('2019-09-01 23:00:00')
              GROUP BY UNIX_TIMESTAMP(timestamp) / 1800,
                       enduserids._experience.mcid.id,
                       web.webPageDetails.name)
        GROUP BY mcid, name) AS table_count_30_mins
       ON table_count_1_min.mcid = table_count_30_mins.mcid
  )
)
```

该语句使用`table_count_1_min`值和网页联接来自`table_count_5_mins`、`table_count_30_mins`和`mcid`的数据。 然后，它跨多个时间间隔合并每个用户的点击计数，以提供用户活动的完整视图。 最后，标记逻辑会识别一分钟内超过50次点击的用户，并将它们标记为机器人(`isBot = 1`)。

### 输出数据集结构

输出数据集的结构包含平面和嵌套字段。 此结构允许在检测异常流量时具有灵活性，并支持使用SQL和机器学习的高级过滤策略。 嵌套字段包括`count`和`web`，它们封装有关活动阈值和网页的粒度详细信息。 捕获这些量度意味着可以轻松提取特征以用于训练和预测任务。

以下架构图概述了生成数据集的结构，并重点说明了如何使用嵌套和平面字段进行高效处理和机器人检测。

```console
root
 |-- count: struct (nullable = false)
 |    |-- one_minute: integer (nullable = true)
 |    |-- five_minute: integer (nullable = true)
 |    |-- thirty_minute: integer (nullable = true)
 |-- id: string (nullable = true)
 |-- web: struct (nullable = false)
 |    |-- webpagedetails: struct (nullable = false)
 |    |    |-- name: string (nullable = true)
 |-- isBot: integer (nullable = false)
```

### 用于训练的输出数据集

此表达式的结果可能与下面提供的表类似。 在表中，`isBot`列用作区分机器人活动和非机器人活动的标签。

```console
| `id`         | `count_per_id`                                      |`isBot`| `web`                                                                                                                    |
|--------------|-----------------------------------------------------|-------|------------------------------------------------------------------------------------------------------------------------|
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":99}| 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 2.5532E+18   | {"one_minute":99,"five_minute":1,"thirty_minute":1} | 1     | {"webpagedetails":{"name":"KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg=="}} |
| 1E+18        | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
| 1.00007E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"8DN0dM4rlvJxt4oByYLKZ/wuHyq/8CvsWNyXvGYnImytXn/bjUizfRSl86vmju7MFMXxnhTBoCWLHtyVSWro9LYg0MhN8jGbswLRLXoOIyh2wduVbc9XeN8yyQElkJm3AW3zcqC7iXNVv2eBS8vwGg=="}} |
| 1.00008E+18  | {"one_minute":1,"five_minute":1,"thirty_minute":1}  | 0     | {"webpagedetails":{"name":"KR+CC8TQzPyMOE/bk7EGgN3lSvP8OsxeI2aLaVrbaeLn8XK3y3zok2ryVyZoiBu3"}}                       |
```

## 用于机器人过滤的高级统计函数 {#statistical-functions-for-bot-filtering}

第二个示例以基本的SQL过滤为基础，采用机器学习技术细化阈值并提高过滤精度。 通过使用高级统计函数（如回归分析或聚类算法），此方法将引入预测功能，可用于开发用于更准确地处理复杂数据集的模型。

### 构建训练数据集 {#build-a-training-dataset}

首先，准备一个数据集，其中包含机器学习模型可以使用的扁平和嵌套结构（如上所述）。 有关如何执行此操作的进一步指导，请参阅[使用嵌套数据结构文档](../../key-concepts/nested-data-structures.md)。 按时间戳、用户ID和网页名称对数据进行分组，以识别机器人活动中的模式。

### 使用TRANSFORM和OPTIONS子句创建模型 {#transform-and-preprocess}

要转换数据集并有效配置机器学习模型，请执行以下步骤。 这些步骤详细说明了如何处理null值、准备特征以及定义模型参数以获得最佳性能。

>[!TIP]
>
>要了解有关使用转换和预处理数据的更多信息，请参阅[功能转换技术文档](../feature-transformation.md)。

1. 要在数字、字符串和布尔列中填充null值，请分别使用`numeric_imputer`、`string_imputer`和`boolean_imputer`函数。 此步骤确保机器学习算法能够处理数据而不会出错。
2. 应用特征转换来准备数据以进行建模。 应用`binarized`、`quantile_discretizer`或`string_indexer`对列进行分类或标准化。 接下来，将输入器（`numeric_imputer`和`string_imputer`）的输出馈送到后续转换器（如`string_indexer`或`quantile_discretizer`）以创建有意义的功能。
3. 使用`vector_assembler`函数将转换后的列组合为一个功能列。 然后使用`min_max_scaler`缩放特征以标准化值以获得更好的模型性能。 注意：在SQL示例中，TRANSFORM子句中提到的最后一个转换将成为机器学习模型使用的特征列。
4. 在OPTIONS子句中指定模型类型和任何其他超参数。 例如，此处选择了`decision_tree_classifier`，因为这是一个分类问题。 已调整(`max_depth`)其他参数（如`MAX_DEPTH=4`）以优化模型以获得更好的性能。
5. 组合特征并标记输出数据。 使用SELECT子句指定用于训练的数据集。 此子句应包括功能列(`count_per_id`、`web`、`id`)和标签列(`isBot`)，后者指示操作是否可能是机器人。

您的语句可能与下面的示例类似。

```sql
CREATE MODEL bot_filtering_model
TRANSFORM (
  numeric_imputer(count_per_id.one_minute, 'mean') imputed_one_minute,
  numeric_imputer(count_per_id.five_minute, 'mode') imputed_five_minute,
  numeric_imputer(count_per_id.thirty_minute) imputed_thirty_minute,
  string_imputer(id, 'unknown') imputed_id,
  string_indexer(imputed_id) si_id,
  quantile_discretizer(imputed_five_minute) buckets_five,
  string_indexer(web.webpagedetails.NAME) si_name,
  quantile_discretizer(imputed_thirty_minute) buckets_thirty,
  vector_assembler(array(si_id, imputed_one_minute, buckets_five, si_name, buckets_thirty)) features,
  min_max_scaler(features) scaled_features
)
OPTIONS (model_type='decision_tree_classifier', max_depth=4, label='isBot')
AS
SELECT count_per_id, isBot, web, id FROM analytics_events_clicks_count_criteria;
```

**结果**

在以下显示的结果中，已成功使用唯一ID、名称和版本创建模型`bot_filtering_model`。 此输出可用作跟踪和管理模型的参考。 使用这些参考信息可确定预测或评估所需的确切配置和版本。

```console
           Created Model ID           |       Created Model       | Version
|--------------------------------------+---------------------------+---------
 2fb4b49e-d35c-44cf-af19-cc210e7dc72c | bot_filtering_model       |       1
```

### 评估经过训练的模型 {#evaluate-trained-model}

创建模型后，使用`MODEL_EVALUATE`命令评估其性能。 该步骤保证了模型满足检测机器人活动的精度和性能要求。

在SQL命令中使用以下参数评估模型：

1. 指定模型名称(`bot_filtering_model`)以指示要计算的模型。 此名称必须与之前使用`CREATE MODEL`命令创建的名称匹配。
2. 在第二个参数中提供模型版本(`1`)以指定要计算的模型版本。 如果存在多个版本，这将确保使用正确的版本。
3. 包含评估数据集，以定义用于评估的数据集。 请确保数据集包含训练期间使用的相同功能列(`count_per_id`、`web`、`id`)和标签列(`isBot`)。

>[!NOTE]
>
>在模型训练期间应用的转换将在评估期间自动应用。

```sql
SELECT *
FROM   model_evaluate(bot_filtering_model, 1,
                      SELECT count_per_id, isBot, web, id
                      FROM   analytics_events_clicks_count_criteria);
```

**结果**

响应包括精准度、精准度、召回率和AUC-ROC等量度。 结果确认了模型是否表现良好。

>[!NOTE]
>
>在0-1范围内的值表示比例或概率，1.0表示完美性能。

```console
auc_roc | accuracy | precision | recall
|---------+----------+-----------+--------
     1.0 |      1.0 |       1.0 |    1.0
```

| **指标** | **描述** |
|--------------|-----------------------------------------------------------------------------------------------------|
| `auc_roc` | 此量度表示模型分类机器人和非机器人的效率。 它广泛用于评估分类模型。 |
| `accuracy` | 模型所做的正确预测的百分比。 |
| `precision` | 在所有预测的机器人中，真正的机器人预测所占的比例。 |
| `recall` | 在所有实际机器人中检测到的真实机器人的比例。 |

>[!TIP]
>
>要在生产沙盒上使用，请考虑在测试数据集上评估模型，以确保它有效地进行泛化。

### 预测机器人活动 {#predict-bot-activity}

将`MODEL_PREDICT`命令与经过训练的模型结合使用，以识别哪些用户(`id`)是机器人。 请按照以下步骤生成用于识别机器人活动的预测：

1. 在第一个参数中使用模型名称(`bot_filtering_model`)来指定要用于预测的模型。
2. 在第二个参数中指定模型版本(`1`)以确保使用正确的模型版本。
3. 要为预测提供正确的数据，请使用SELECT语句指定功能列(`count_per_id`、`web`、`id`)。 不要包含标签列(`isBot`)，因为模型将为此字段生成预测。

```sql
SELECT *
FROM model_predict(bot_filtering_model, 1,
    SELECT count_per_id, web, id FROM analytics_events_clicks_count_criteria
);
```

**结果**

响应包括每个用户(`id`)的预测以及有关其活动和模型分类结果的详细信息。 此输出允许详细检查用户行为和模型机器人活动的分类。

<!-- Q) Anil, why is there no ID in the first two rows? Can we get that info? Or should it be the same as the other IDs? -->

```console
         id          | count.one_minute | count.five_minute | count.thirty_minute |                                                                  web.webpagedetails.name                                                                  | prediction
|---------------------+------------------+-------------------+---------------------+-------+----------------------------------------------------------------------------------------------------------------------------------------------------+------------
                     |              110 |                   |                     |   4UNDilcY5VAgu2pRmX4/gtVnj+YxDDQaJd1G8p8WX46//wYcrHy+APUN0I556E80j1gIzFmilA6DV4s0Zcs4ruiP36gLgC7bj4TH0q6LU0E=                                             |        1.0  
                     |              105 |                   |                     |   lrSaZk04Yq+5P9+6l4BohwXik0s0/XeW9X28ZgWt1yj1QQztiAt9Qgt2WYrWcAeoGZChAJw/l8e4ojZDT5WHCjteSt35S01Vv1JzDGPAg+IyhIzMTsVyLpW8WWpXjJoMCt6Tv7fFdF73EIH+IrK5fA== |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
 2553215812530219515 |               99 |                 1 |                   1 |   KR+CC8TQzPyK4ord6w1PfJay1+h6snSF++xFERc4ogrEX4clJROgzkGgnSTSGWWZfNS/Ouz2K0VtkHG77vwoTg==                                                                 |        1.0
```

下表说明了每个量度：

| 列名称 | 描述 |
|---------------------------|----------------------------------------------------------------------------------------------------------|
| `id` | 每个用户的唯一标识符。 |
| `count.one_minute` | 1 — 分钟间隔内的聚合单击计数。 |
| `count.five_minute` | 5分钟间隔内的聚合单击计数。 |
| `count.thirty_minute` | 30分钟间隔内的聚合单击计数。 |
| `web.webpagedetails.name` | 所访问网页的名称。 这会为用户活动提供上下文。 |
| `prediction` | 模型的预测。 `1.0`结果表示用户根据其活动模式标记为机器人。 |

## 管理您的模型 {#manage-models}

要管理您的机器学习模型，请使用下面部分中列出的SQL关键字。

### 列出可用模型 {#list-available-models}

使用`SHOW MODELS;`命令高效地管理和查看模型。 此命令列出在当前工作区中创建的所有机器学习模型。 输出提供可用模型的概述，并包含其名称、版本和其他元数据。

```sql
SHOW MODELS;
```

### 删除模型 {#delete-models}

要释放资源并确保仅保留相关模型，请使用`DROP MODEL`命令删除过时或不必要的模型。 此命令会删除在关键词之后指定的任何机器学习模型。 在下面的示例中，`bot_filtering_model`已从系统中删除。

```sql
DROP MODEL bot_filtering_model;
```

## 后续步骤

通过阅读本文档，您已了解如何使用Data Distiller方法通过SQL和机器学习技术识别和过滤机器人活动。 接下来，将这些概念应用于数据集，并自动化模型重新训练以持续改进。
