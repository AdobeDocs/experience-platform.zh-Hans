---
title: 数据集示例
description: 查询服务示例数据集使您能够针对大数据执行探索性查询，并显着减少处理时间，而代价是查询准确性。 本指南提供了有关如何管理样本以进行近似查询处理的信息
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: ef71371b04746bbf12ac58e91c9ecb5806f7e771
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# 数据集示例

Adobe Experience Platform查询服务在其近似的查询处理功能中提供示例数据集。 使用来自现有样本的均匀随机样本创建样本数据集 [!DNL Azure Data Lake Storage] (ADLS)数据集仅使用原始记录的一个百分比。 此百分比称为采样速率。 通过调整采样率来控制精度与处理时间的平衡，可以对大数据进行探索性查询，从而大大减少处理时间，但代价是查询的准确性。

由于许多用户不需要对数据集上的聚合操作获得准确答案，因此对于大型数据集的探索性查询，发出近似查询以返回近似答案会更有效。 由于示例数据集仅包含来自原始数据集的数据的百分比，因此，您可以通过提高查询准确性来缩短响应时间。 在读取时，查询服务必须扫描的行数较少，产生的结果比查询整个数据集时更快。

为了帮助您管理用于近似查询处理的示例，查询服务支持对数据集示例执行以下操作：

- [创建统一的随机数据集示例。](#create-a-sample)
- [（可选）指定筛选条件](##optional-filter-criteria)
- [查看ADLS表的示例列表。](#view-list-of-samples)
- [直接查询示例数据集。](#query-sample-datasets)
- [删除示例。](#delete-a-sample)
- 删除原始ADLS表时删除关联的样例。

## 快速入门 {#get-started}

要使用本文档中详述的创建和删除近似查询处理功能，必须将会话标志设置为 `true`. 在查询编辑器或PSQL客户端的命令行中，输入 `SET aqp=true;` 命令。

>[!NOTE]
>
>每次登录Platform时，都必须启用会话标志。

![突出显示了“SET aqp=true；”命令的查询编辑器。](../images/essential-concepts/set-session-flag.png)

## 创建统一的随机数据集示例 {#create-a-sample}

使用 `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` 命令来使用该数据集名称创建统一的随机示例。

采样率是从原始数据集中获取的记录的百分比。 您可以使用控制采样速率 `TABLESAMPLE SAMPLERATE` 关键字。 在本例中，5.0的值等于50%的采样率。 值为2.5将等于25%，以此类推。

>[!IMPORTANT]
>
>系统允许每个数据集最多有五个示例。 如果尝试创建第六个示例数据集，屏幕上将显示一条错误消息，指示已达到示例限制。

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## （可选）指定筛选条件 {#optional-filter-criteria}

您可以选择为统一随机抽样指定筛选条件。 这允许您根据分析表的过滤子集创建示例。

创建示例时，首先应用可选过滤器，然后从数据集的已筛选视图创建示例。 应用了筛选条件的数据集示例遵循以下查询格式：

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

此类过滤样本数据集的实用示例如下：

```sql
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
ANALYZE TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

在提供的示例中，表名为 `large_table`，则原始表格上的筛选条件为 `month(to_timestamp(timestamp)) in ('8', '9')`，并且采样率为（过滤数据的X%），在这种情况下， `10`.

## 查看示例列表 {#view-list-of-samples}

使用 `sample_meta()` 函数以查看与ADLS表关联的示例列表。

```sql
SELECT sample_meta('example_dataset_name')
```

数据集示例列表以下面的示例格式显示。

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## 查询示例数据集 {#query-sample-datasets}

使用 `{EXAMPLE_DATASET_NAME}` 直接查询示例表。 或者，添加 `WITHAPPROXIMATE` 关键字到查询的结尾，查询服务自动使用最近创建的示例。

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
