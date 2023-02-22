---
title: 数据集示例
description: 查询服务示例数据集使您能够对大数据进行探索性查询，同时极大地缩短了处理时间，同时也降低了查询准确性。 本指南提供了有关如何管理示例以便进行近似查询处理的信息
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 13779e619345c228ff2a1981efabf5b1917c4fdb
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 数据集示例

Adobe Experience Platform查询服务提供示例数据集作为其近似查询处理功能的一部分。 使用现有的统一随机样本创建示例数据集 [!DNL Azure Data Lake Storage] (ADLS)仅使用原始数据中某个百分比记录的数据集。 此百分比称为采样率。 通过调整采样率以控制准确性和处理时间的平衡，您可以对大数据进行探索性查询，并大大减少了处理时间，同时也降低了查询准确性。

由于许多用户在数据集上的聚合操作不需要确切的答案，因此发出近似查询以返回近似答案对于大型数据集上的探索性查询更有效。 由于示例数据集仅包含原始数据集中某一百分比的数据，因此您可以使用查询准确性来缩短响应时间。 在读取时，查询服务必须扫描的行数少，这样产生的结果比查询整个数据集的速度要快。

为了帮助您管理用于近似查询处理的示例，查询服务支持对数据集示例执行以下操作：

- [创建统一的随机数据集示例。](#create-a-sample)
- [（可选）指定筛选条件](##optional-filter-criteria)
- [查看ADLS表的示例列表。](#view-list-of-samples)
- [直接查询示例数据集。](#query-sample-datasets)
- [删除示例。](#delete-a-sample)
- 删除原始ADLS表时关联的示例。

## 快速入门 {#get-started}

要使用本文档中详细描述的创建和删除近似查询处理功能，必须将会话标记设置为 `true`. 在查询编辑器或PSQL客户端的命令行中，输入 `SET aqp=true;` 命令。

>[!NOTE]
>
>每次登录平台时，必须启用会话标记。

![高亮显示“SET aqp=true；”命令的查询编辑器。](../images/essential-concepts/set-session-flag.png)

## 创建统一的随机数据集示例 {#create-a-sample}

使用 `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` 命令来从该数据集创建统一的随机示例。

采样率是从原始数据集获取的记录的百分比。 您可以使用 `TABLESAMPLE SAMPLERATE` 关键词。 在本例中，值5.0等于50%的采样率。 值2.5等于25%，以此类推。

>[!IMPORTANT]
>
>系统允许每个数据集最多包含5个示例。 如果尝试创建第六个示例数据集，屏幕上会显示一条错误消息，指出已达到示例限制。

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## （可选）指定筛选条件 {#optional-filter-criteria}

您可以选择为统一随机示例指定筛选条件。 这允许您根据分析表的过滤子集创建示例。

创建示例时，首先应用可选过滤器，然后根据数据集的过滤视图创建示例。 应用了过滤器的数据集示例遵循以下查询格式：

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

此类过滤样本数据集的实际示例如下：

```sql
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

在提供的示例中，表名为 `large_table`，则原始表格的筛选条件为 `month(to_timestamp(timestamp)) in ('8', '9')`，且取样率为（过滤数据的X%），在这种情况下， `10`.

## 查看示例列表 {#view-list-of-samples}

使用 `sample_meta()` 函数查看与ADLS表关联的示例列表。

```sql
SELECT sample_meta('example_dataset_name')
```

数据集示例列表以以下示例的格式显示。

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## 查询示例数据集 {#query-sample-datasets}

使用 `{EXAMPLE_DATASET_NAME}` 直接查询示例表。 或者，添加 `WITHAPPROXIMATE` 关键字到查询和查询服务的结尾会自动使用最近创建的示例。

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## 删除数据集示例 {#delete-a-sample}

删除操作允许您在达到五个数据集示例的最大限制后创建新示例。

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>如果您有多个从原始ADLS数据集派生的示例数据集，则在删除原始数据集时，所有关联的示例也会被删除。
