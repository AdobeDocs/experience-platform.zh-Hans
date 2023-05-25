---
title: 数据集统计信息计算
description: 本文档介绍如何使用SQL命令计算Azure Data Lake Storage (ADLS)数据集的列级统计信息。
source-git-commit: b063bcf7b3d2079715ac18fde55f47cea078b609
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 数据集统计信息计算

您现在可以计算列级别统计信息 [!DNL Azure Data Lake Storage] (ADLS)数据集具有 `COMPUTE STATISTICS` 和 `SHOW STATISTICS` sql命令。 用于计算数据集统计信息的SQL命令是 `ANALYZE TABLE` 命令。 有关以下内容的完整详细信息： `ANALYZE TABLE` 命令位于 [SQL参考文档](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>目前，生成的统计信息仅对该会话有效，并且不会在会话之间持续存在。 无法跨不同的PSQL会话访问它们。

使用 `SHOW STATISTICS FOR <alias_name>` 命令中，您可以看到使用 `ANALYZE TABLE COMPUTE STATISTICS` 命令。 通过组合这些命令，您现在可以计算整个数据集、数据集子集、所有列或列子集的列统计信息。

>[!IMPORTANT]
>
>此 `COMPUTE STATISTICS`， `FILTERCONTEXT`， `FOR COLUMNS`、和 `SHOW STATISTICS` data warehouse表不支持命令。 的这些扩展 `ANALYZE TABLE` 命令当前仅支持ADLS表。 欲了解更多信息，请参见 [“分析表”部分](../sql/syntax.md#analyze-table) SQL语法指南中的。

本指南可帮助您构建查询，以便计算ADLS数据集的列统计信息。 使用这些命令，可以使用SQL查询通过PSQL客户端查看会话中生成的统计信息。

## 计算统计信息 {#compute-statistics}

其他构造已添加到 `ANALYZE TABLE` 命令允许您 **计算数据集子集和某些列的统计信息**. 为此，您必须使用 `ANALYZE TABLE <tableName> COMPUTE STATISTICS` 格式。

>[!IMPORTANT]
>
>缺省行为计算 **整个数据集** 和 **所有列**. 要计算所有列的统计信息，可以使用查询格式 `ANALYZE TABLE COMPUTE STATISTICS`. 您是 **非** 建议在ADLS数据集上使用此项，因为数据集的大小可能非常大（可能为PB数据）。 相反，您应该始终考虑使用以下方式运行analyze命令 `FILTERCONTEXT` 和指定的列列表。 请参阅以下章节： [限制分析的列](#limit-included-columns) 和 [添加筛选条件](#filter-condition) 了解更多详细信息。

以下示例计算 `adc_geometric` 数据集和 **所有** 列中的列。

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` 不支持数组或映射数据类型。 您可以设置 `skip_stats_for_complex_datatypes` 如果输入数据流具有带数组和映射数据类型的列，则标记为通知或出错。 默认情况下，该标记设置为true。 要启用通知或错误，请使用以下命令： `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

控制台输出不显示响应analyze table compute statistics命令的统计信息。 相反，控制台将显示单行列 `Statistics ID` 具有用于引用结果的通用唯一标识符。 成功完成 `COMPUTE STATISTICS` 查询，结果显示如下：

```console
| Statistics ID    | 
| ---------------- |
| QqMtDfHQOdYJpZlb |
(1 row)
```

要查看输出，您必须使用 `SHOW STATISTICS` 命令。 说明 [如何显示统计信息](#show-statistics) 稍后在文档中提供。

## 限制包含的列 {#limit-included-columns}

您可以通过按名称引用特定数据集列来计算这些列的统计信息。 使用 `FOR COLUMNS (<col1>, <col2>)` 用于定位特定列的语法。 以下示例计算列的统计信息  `commerce`， `id`、和 `timestamp` 数据集 `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

您可以计算任何根级别或嵌套列的统计信息。 以下示例演示了这些引用。

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 添加时间戳筛选条件 {#filter-condition}

可添加时间戳筛选条件以集中对列进行分析。 这可用于过滤掉历史数据或集中特定时段的数据分析。 此 `FILTERCONTEXT` 命令根据您提供的筛选条件计算数据集子集的统计信息。

在以下示例中，将计算数据集所有列的统计信息 `tableName`，其中列时间戳的值介于指定的值范围 `2023-04-01 00:00:00` 和 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

您可以将列限制和过滤器结合使用，为数据集列创建高度特定的计算查询。 例如，以下查询计算列的统计信息 `commerce`， `id`、和 `timestamp` 数据集 `tableName`，其中列时间戳的值介于指定的值范围 `2023-04-01 00:00:00` 和 `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR (columns commerce, id, timestamp);
```

<!-- ## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. -->

## 显示统计信息 {#show-statistics}

<!-- Commented out until the <alias_name> feature is released.
The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  -->

即使使用筛选条件和列列表，计算也可以针对大量数据。 查询服务为统计信息ID生成一个通用唯一标识符以存储此计算的信息。 然后，您可以使用此统计信息ID查找计算出的统计信息，其中 `SHOW STATISTICS` 命令。

生成的统计信息ID和统计信息仅对此特定会话有效，不能跨不同的PSQL会话访问。 计算统计信息当前不是永久性的。 要显示统计信息，请使用下面显示的命令。

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

输出可能类似于下面的示例。

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.session.timestamp                    |            450 |          -2313 |          21903 |               7.0 |                 0.0 |         0 | Long
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(13 rows)
```

## 后续步骤 {#next-steps}

通过阅读本文档，您现在可以更好地了解如何使用SQL查询从ADLS数据集生成列级统计信息。 建议您阅读 [SQl语法指南](../sql/syntax.md) 以了解Adobe Experience Platform查询服务的更多功能。
