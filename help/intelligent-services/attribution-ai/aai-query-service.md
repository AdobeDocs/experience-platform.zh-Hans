---
keywords: 洞察；归因ai；归因ai洞察；AAI查询服务；归因查询；归因得分
solution: Intelligent Services, Experience Platform
title: 使用查询服务分析归因分数
topic-legacy: Attribution AI queries
description: 了解如何使用Adobe Experience Platform 查询 Service分析Attribution AI分数。
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 使用查询服务分析归因得分

数据中的每一行都表示一个转换，其中相关触点的信息作为`touchpointsDetail`列下的结构数组存储。

| 触点信息 | 栏目 |
| ---------------------- | ------ |
| 触点名称 | `touchpointsDetail. touchpointName` |
| 触点渠道 | `touchpointsDetail.touchPoint.mediaChannel` |
| 触点Attribution AI算法得分 | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## 查找数据路径

在Adobe Experience Platform UI中，选择左侧导航中的&#x200B;**[!UICONTROL Datasets]**。 将显示&#x200B;**[!UICONTROL Datasets]**&#x200B;页。 接下来，选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡并查找Attribution AI分数的输出数据集。

![访问您的实例](./images/aai-query/datasets_browse.png)

选择输出数据集。 此时将显示数据集活动页。

![数据集活动页](./images/aai-query/select_preview.png)

在数据集活动页面中，选择右上角的&#x200B;**[!UICONTROL Preview dataset]**&#x200B;以预览您的数据，并确保按预期方式摄取数据。

![预览数据集](./images/aai-query/preview_dataset.JPG)

预览模式后，选择右边栏中的数据。 将出现一个带模式名称和说明的快显窗口。 选择模式名称超链接以重定向到评分模式。

![选择模式](./images/aai-query/select_schema.png)

使用评分模式，您可以选择或搜索值。 选择后，将打开&#x200B;**[!UICONTROL Field properties]**&#x200B;侧边栏，以便复制路径以用于创建查询。

![复制路径](./images/aai-query/copy_path.png)

## 访问查询服务

要从平台UI中访问查询服务，请在左侧导航中选择&#x200B;**[!UICONTROL Queries]**，然后选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡进行开始。 将加载先前保存的查询的列表。

![查询服务浏览](./images/aai-query/query_tab.png)

接下来，选择右上角的&#x200B;**[!UICONTROL Create query]**。 加载查询编辑器。 使用查询编辑器，您可以开始使用评分数据创建查询。

![查询编辑器](./images/aai-query/query_example.png)

有关查询编辑器的详细信息，请访问[查询编辑器用户指南](../../query-service/ui/user-guide.md)。

## 查询模板，用于归因得分分析

以下查询可用作不同得分分析方案的模板。 您需要将`_tenantId`和`your_score_output_dataset`替换为在评分输出模式中找到的正确值。

>[!NOTE]
>
> 根据数据的摄取方式，下面使用的值（如`timestamp`）可能采用不同的格式。

### 验证示例

**按转换事件（在转换窗口中）划分的转换总数**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**仅转换事件的总数（在转换窗口中）**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### 趋势分析示例

**每天转换次数**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### 分发分析示例

**按定义类型（在转换窗口中）划分的转换路径上的接触点数量**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### Insight生成示例

**按接触点和转换日期（在转换窗口中）划分的增量单位**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**按接触点和接触点日期（在转换窗口中）划分的增量单位**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**所有评分模型的特定接触点类型的汇总得分（在转换窗口中）**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**高级 — 路径长度分析**

获取每个转换事件类型的路径长度分布：

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**高级 — 转换路径上的不同接触点数分析**

获取每个转化事件类型在转化路径上的不同接触点数的分布：

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```

### 模式拼合和爆炸示例

此查询将结构列拼合为多个奇数列，并将数组分解为多个行。 这有助于将归因分数转换为CSV格式。 此查询的输出具有一个转换，并且每个行中对应于该转换的触点之一。

>[!TIP]
>
> 在此示例中，除了`_tenantId`和`your_score_output_dataset`之外，还需要替换`{COLUMN_NAME}`。 `COLUMN_NAME`变量可以采用配置Attribution AI实例期间添加的可选传递列名(报告列)的值。 请查看您的评分输出模式，以找到完成此查询所需的`{COLUMN_NAME}`值。

```sql
SELECT 
  segmentation,
  conversionName,
  scoreCreatedTime,
  aaid, _id, eventMergeId,
  conversion.eventType as conversion_eventType,
  conversion.quantity as conversion_quantity,
  conversion.eventSource as conversion_eventSource,
  conversion.priceTotal as conversion_priceTotal,
  conversion.timestamp as conversion_timestamp,
  conversion.geo as conversion_geo,
  conversion.receivedTimestamp as conversion_receivedTimestamp,
  conversion.dataSource as conversion_dataSource,
  conversion.productType as conversion_productType,
  conversion.passThrough.{COLUMN_NAME} as conversion_passThru_column,
  conversion.skuId as conversion_skuId,
  conversion.product as conversion_product,
  touchpointName,
  touchPoint.campaignGroup as tp_campaignGroup, 
  touchPoint.mediaType as tp_mediaType,
  touchPoint.campaignTag as tp_campaignTag,
  touchPoint.timestamp as tp_timestamp,
  touchPoint.geo as tp_geo,
  touchPoint.receivedTimestamp as tp_receivedTimestamp,
  touchPoint.passThrough.{COLUMN_NAME} as tp_passThru_column,
  touchPoint.campaignName as tp_campaignName,
  touchPoint.mediaAction as tp_mediaAction,
  touchPoint.mediaChannel as tp_mediaChannel,
  touchPoint.eventid as tp_eventid,
  scores.*
FROM (
  SELECT
        _tenantId.your_score_output_dataset.segmentation,
        _tenantId.your_score_output_dataset.conversionName,
        _tenantId.your_score_output_dataset.scoreCreatedTime,
        _tenantId.your_score_output_dataset.conversion,
        _id,
        eventMergeId,
        map_values(identityMap)[0][0].id as aaid,
        inline(_tenantId.your_score_output_dataset.touchpointsDetail)
  FROM
        your_score_output_dataset
)
```
