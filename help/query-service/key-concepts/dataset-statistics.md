---
title: 数据集统计信息计算
description: 本文档介绍如何使用SQL命令计算Azure Data Lake Storage (ADLS)数据集的列级统计信息。
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# 数据集统计信息计算

您现在可以使用[!DNL Azure Data Lake Storage] SQL命令计算`COMPUTE STATISTICS` (ADLS)数据集的列级统计信息。 用于计算数据集统计信息的SQL命令是`ANALYZE TABLE`命令的扩展。 有关`ANALYZE TABLE`命令的完整详细信息可在[SQL参考文档](../sql/syntax.md#analyze-table)中找到。

>[!NOTE]
>
>计算的统计信息存储在具有会话级持久性的临时表中。 您可以在该会话期间随时访问计算结果。 无法跨不同的PSQL会话访问它们。

要查看使用`ANALYZE TABLE COMPUTE STATISTICS`命令计算的统计信息，可以对别名或统计信息ID使用SELECT查询。 您还可以将统计分析的范围限制为整个数据集、数据集的子集、所有列或列的子集。

>[!IMPORTANT]
>
>加速存储表不支持`COMPUTE STATISTICS`、`FILTERCONTEXT`和`FOR COLUMNS`命令。 当前，只有ADLS表支持`ANALYZE TABLE`命令的这些扩展。 有关详细信息，请参阅SQL语法指南的[ANALYZE TABLE部分](../sql/syntax.md#analyze-table)。

本指南可帮助您构建查询，以便计算ADLS数据集的列统计信息。 使用这些命令，可以使用SQL查询通过PSQL客户端查看会话中生成的统计信息。

## 计算统计信息 {#compute-statistics}

已向`ANALYZE TABLE`命令添加了其他构造，该命令允许您&#x200B;**计算数据集子集和某些列的统计信息**。 要计算数据集统计信息，必须使用`ANALYZE TABLE <tableName> COMPUTE STATISTICS`格式。

>[!IMPORTANT]
>
>默认行为计算&#x200B;**整个数据集**&#x200B;和&#x200B;**所有列**&#x200B;的统计信息。 若要计算所有列的统计信息，应使用查询格式`ANALYZE TABLE COMPUTE STATISTICS`。 建议您&#x200B;**不要**&#x200B;在ADLS数据集上使用不带过滤器的`COMPUTE STATISTICS`命令，因为数据集的大小可能非常大（可能是PB数据）。 相反，您应该始终考虑使用`FILTERCONTEXT`和指定的列列表来运行分析命令。 有关更多详细信息，请参阅[限制分析的列](#limit-included-columns)和[添加筛选条件](#filter-condition)的部分。

下面显示的示例用于计算`adc_geometric`数据集以及数据集中&#x200B;**所有**&#x200B;列的统计信息。

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS`命令不支持数组或映射数据类型。 如果输入数据框架具有带数组的列并映射数据类型，则可以设置`skip_stats_for_complex_datatypes`标志以接收通知或出错。 默认情况下，该标记设置为true。 要启用通知或错误，请使用以下命令： `SET skip_stats_for_complex_datatypes = false`。

## 创建别名 {#alias-name}

由于计算结果可能是大量数据，直接在控制台输出中返回计算数据是不合理的。 虽然别名是可选的，但建议您在计算统计信息时使用别名作为最佳实践。 在语句中提供别名，以描述性引用SQL查询中的结果。 或者，自动生成的`Statistics ID`用于存储计算的信息。

下面的示例将输出计算统计信息存储在`alias_name`中以供以后参考。 运行`ANALYZE TABLE`命令后，查询中使用的别名即可供参考。

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

上述示例的输出为`SUCCESSFULLY COMPLETED, alias_name`。 控制台输出在响应analyze table compute statistics命令时不显示统计信息。 要查看详细结果，必须对别名或统计信息ID使用SELECT查询。

## 查看已计算统计信息的输出 {#view-output-of-computed-statistics}

如果您未提前提供别名，查询服务将自动为`Statistics ID`生成一个格式为`<tableName_stats_{incremental_number}>`的名称。 如果提供了别名，则该别名会显示在`Statistics ID`列中。

`COMPUTE STATISTICS`查询的示例输出如下所示：

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

然后，您可以通过引用&#x200B;**直接**&#x200B;查询计算的统计信息`Statistics ID`。 下面的示例语句允许您在与`Statistics ID`或别名一起使用时完整查看输出。

```sql
SELECT * FROM adc_geometric_stats_1; 
```

计算的统计信息输出可能与下面的示例类似。

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
|------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
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
(12 rows)
```

## 显示统计分析元数据 {#show-statistics}

您可以使用`SHOW STATISTICS`命令显示会话中生成的所有临时统计数据的元数据。 此命令可帮助您优化统计分析的范围。

下面显示了`SHOW STATISTICS`的示例输出。

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
|----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

下面提供了元数据列名的说明。

| 列名 | 描述 |
|---|---|
| `statsId` | 此ID引用了`COMPUTE STATISTICS`命令生成的临时统计信息表。 |
| `tableName` | 用于分析的原始表。 |
| `columnSet` | 专门为分析选择的任何列的列表。 空值表示已分析所有列。 有关详细信息，请参阅[限制列](#limit-included-columns)部分。 |
| `filterContext` | 应用于分析的任何过滤器的列表。 |
| `timestamp` | 应用于您的数据分析的任何时间顺序过滤器，以重点关注特定时段。 有关更多详细信息，请参阅[时间戳筛选条件部分](#filter-condition)。 |

可以使用该统计信息ID或别名在该会话中随时通过SELECT语句查找计算的统计信息。 生成的统计信息ID和统计信息仅对此特定会话有效，不能跨不同的PSQL会话访问。 计算的统计信息当前不是持久的。 有关更多详细信息，请参阅有关如何[查看计算统计信息](#view-output-of-computed-statistics)的输出的部分。

## 限制包含的列 {#limit-included-columns}

要集中分析，您可以通过按名称引用特定数据集列来计算这些列的统计信息。 使用`FOR COLUMNS (<col1>, <col2>)`语法定位特定列。 以下示例计算数据集`commerce`的列`id`、`timestamp`和`tableName`的统计信息。

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

您可以计算任何根级别或嵌套列的统计信息。 以下示例演示了这些引用。

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## 添加时间戳筛选条件 {#filter-condition}

要根据时间顺序集中分析列，您可以添加时间戳筛选条件。 此条件可用于过滤掉历史数据或集中特定时段的数据分析。 `FILTERCONTEXT`命令根据您提供的筛选条件计算数据集子集的统计信息。

在以下示例中，对数据集`tableName`的所有列计算统计信息，其中列时间戳的值介于指定的范围`2023-04-01 00:00:00`和`2023-04-05 00:00:00`之间。

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

您可以将列限制和过滤器结合使用，为数据集列创建高度特定的计算查询。 例如，以下查询计算数据集`commerce`的列`id`、`timestamp`和`tableName`的统计信息，其中列时间戳的值介于指定的范围`2023-04-01 00:00:00`和`2023-04-05 00:00:00`之间。

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## 后续步骤 {#next-steps}

通过阅读本文档，您现在可以更好地了解如何使用SQL查询从ADLS数据集生成列级统计信息。 建议您阅读[SQl语法指南](../sql/syntax.md)，以了解Adobe Experience Platform查询服务的更多功能。
