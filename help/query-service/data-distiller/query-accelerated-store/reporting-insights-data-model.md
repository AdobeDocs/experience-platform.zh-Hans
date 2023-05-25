---
title: Query Accelerated Store报告分析指南
description: 了解如何通过Query Service构建报告见解数据模型，以与加速商店数据和用户定义的仪表板一起使用。
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Query accelerated store报告见解指南

Query accelerated store允许您减少从数据中获得关键见解所需的时间和处理能力。 通常，会定期（例如，每小时或每天）处理数据，其中会创建和报告聚合视图。 对这些从汇总数据生成的报表的分析可得出旨在提高业务绩效的见解。 Query accelerated store提供缓存服务、并发、交互式体验和无状态API。 但是，它假定已针对聚合查询而非原始数据查询对数据进行预处理和优化。

查询加速存储允许您构建自定义数据模型和/或扩展现有Adobe Real-time Customer Data Platform数据模型。 然后，您可以与互动或将报表见解嵌入到您选择的报表/可视化图表框架中。 请参阅Real-time Customer Data Platform Insights数据模型文档，了解如何 [自定义您的SQL查询模板，以便为您的营销和关键绩效指标(KPI)用例创建Real-Time CDP报表](../../../dashboards/cdp-insights-data-model.md).

Adobe Experience Platform的Real-Time CDP数据模型提供有关用户档案、区段和目标的洞察，并启用Real-Time CDP洞察功能板。 本文档将指导您完成创建报表分析数据模型的过程，以及如何根据需要扩展Real-Time CDP数据模型。

## 先决条件

本教程使用用户定义的功能板在Platform UI中可视化自定义数据模型中的数据。 请查看 [用户定义的功能板文档](../../../dashboards/user-defined-dashboards.md) 以了解有关此功能的更多信息。

## 快速入门

要构建用于报表分析的自定义数据模型，并扩展包含扩充的Platform数据的Real-Time CDP数据模型，需要数据Distiller SKU。 请查看 [封装](../../packages.md) 和 [护栏](../../guardrails.md#query-accelerated-store) 与数据Distiller SKU相关的文档。 如果您没有Data Distiller SKU，请联系您的Adobe客户服务代表以了解更多信息。

<!-- Document is hidden temporarily
Please see the [packaging](../../packages.md), [guardrails](../../guardrails.md#query-accelerated-store), and [licensing](../../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

## 构建报表见解数据模型

本教程使用构建受众洞察数据模型的示例。 如果您使用一个或多个广告商平台来访问受众，则可以使用广告商的API来获取受众的大致匹配计数。

最初，您有一个来自您的源（可能来自广告商平台API）的初始数据模型。 要汇总查看原始数据，请按照下图所述创建报表分析模型。 这允许一个数据集获取受众匹配的上限和下限。

![受众分析用户模型的实体关系图(ERD)。](../../images/query-accelerated-store/audience-insight-user-model.png)

在此示例中， `externalaudiencereach` 表/数据集基于ID并跟踪匹配计数的下限和上限。 此 `externalaudiencemapping` 维度表/数据集将外部ID映射到Platform上的目标和区段。

## 使用Data Distiller创建报表见解模型

接下来，创建报告洞察模型(`audienceinsight` 在本例中)和使用SQL命令 `ACCOUNT=acp_query_batch and TYPE=QSACCEL` 以确保在加速存储上创建。 然后使用查询服务创建 `audienceinsight.audiencemodel` 架构 `audienceinsight` 数据库。

>[!NOTE]
>
>以下各项需要数据Distiller SKU： `ACCOUNT=acp_query_batch` 命令。 如果没有它，则会在数据湖上创建常规数据模型。

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## 创建表、关系和填充数据

您现在已经创建了 `audienceinsight` 报告洞察模型，创建 `externalaudiencereach` 和 `externalaudiencemapping` 表并建立它们之间的关系。 接下来，使用 `ALTER TABLE` 命令在表之间添加外键约束并定义关系。 以下SQL示例演示了如何执行此操作。

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) segment_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

成功执行这两项操作后 `ALTER TABLE` 命令，事实表与维度表之间的关系形成。

语句运行后，使用 `SHOW datagroups;` 命令以从 `audienceinsight.audiencemodel`. 您的列表结果应类似于以下提供的示例。

>[!IMPORTANT]
>
>只有加速存储中的数据才能从查询服务无状态API端点访问 `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## 查询报表分析数据模型

使用查询服务查询 `audiencemodel.externalaudiencereach` 维度表。 下面显示了示例查询。

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

列表结果包括计数和ID。

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## 使用Real-Time CDP分析数据模型扩展数据模型

您可以使用其他详细信息扩展受众模型，以创建更丰富的维度表。 例如，您可以将区段名称和目标名称映射到外部受众标识符。 要实现此目的，请使用查询服务创建或刷新新数据集，并将其添加到将区段和目标与外部身份结合在一起的受众模型。 下图说明了此数据模型扩展的概念。

![链接Real-Time CDP洞察数据模型和查询加速存储模型的ERD图表。](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## 创建维度表以扩展您的报表见解模型

使用查询服务将扩充Real-Time CDP维度数据集中的关键描述性属性添加到 `audienceinsight` 数据模型，并在事实表与新维度表之间建立关系。 以下SQL演示了如何将现有维度表集成到报表分析数据模型中。

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         segment_name,
         destination_status,
         a.destination_id,
         a.segment_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_segments AS b
                      ON ( ( a.segment_id ) = ( b.segment_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

使用 `SHOW datagroups;` 用于确认创建附加 `external_seg_dest_map` 维度表。

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## 查询扩展加速商店报告见解数据模型

现在， `audienceinsight` 数据模型已得到增强，可以查询。 以下SQL显示了映射的目标和区段的列表。

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.segment_name,
       b.destination_status,
       b.destination_id,
       b.segment_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

查询返回查询加速存储上的所有数据集：

```console
ext_custom_audience_id | destination_name |       segment_name        | destination_status | destination_id | segment_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## 使用用户定义的仪表板可视化您的数据

现在您已经创建了自定义数据模型，接下来可以使用自定义查询和用户定义的仪表板可视化您的数据。

以下SQL提供了按目标中的受众划分的匹配计数，以及按区段划分的受众的每个目标。

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.segment_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.segment_name
ORDER BY b.destination_name
LIMIT  5000
```

下图提供了一个示例，说明了如何使用您的报表分析数据模型实现可能的自定义可视化图表。

![根据新报表分析数据模型创建的按目标和区段构件划分的匹配计数。](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

您的自定义数据模型可在用户定义的仪表板工作区中的可用数据模型列表中找到。 请参阅 [用户定义的仪表板指南](../../../dashboards/user-defined-dashboards.md) 以获取有关如何使用自定义数据模型的指导。
