---
keywords: 分析；归因ai；归因ai分析；AAI查询服务；归因查询；归因得分
feature: Attribution AI
title: 使用查询服务分析归因得分
description: 了解如何使用Adobe Experience Platform查询服务分析Attribution AI得分。
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 使用查询服务分析归因得分

数据中的每一行都表示一个转化，在该转化中，相关接触点的信息将存储为 `touchpointsDetail` 列。

| 接触点信息 | 栏目 |
| ---------------------- | ------ |
| 接触点名称 | `touchpointsDetail. touchpointName` |
| 接触点渠道 | `touchpointsDetail.touchPoint.mediaChannel` |
| 接触点Attribution AI算法得分 | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## 查找数据路径

在Adobe Experience Platform UI中，选择 **[!UICONTROL 数据集]** 中。 的 **[!UICONTROL 数据集]** 页面。 接下来，选择 **[!UICONTROL 浏览]** 选项卡，然后为您的Attribution AI得分查找输出数据集。

![访问您的实例](./images/aai-query/datasets_browse.png)

选择输出数据集。 此时会显示数据集活动页面。

![数据集活动页面](./images/aai-query/select_preview.png)

在数据集活动页面中，选择 **[!UICONTROL 预览数据集]** ，以预览数据并确保按预期摄取数据。

![预览数据集](./images/aai-query/preview_dataset.JPG)

预览数据后，选择右边栏中的架构。 此时会出现一个弹出窗口，其中包含架构名称和描述。 选择架构名称超链接可重定向到评分架构。

![选择架构](./images/aai-query/select_schema.png)

使用评分架构，您可以选择或搜索值。 选择后， **[!UICONTROL 字段属性]** 边栏会打开，用于复制用于创建查询的路径。

![复制路径](./images/aai-query/copy_path.png)

## 访问查询服务

要从平台UI中访问查询服务，请首先选择 **[!UICONTROL 查询]** 在左侧导航中，选择 **[!UICONTROL 浏览]** 选项卡。 将加载之前保存的查询列表。

![查询服务浏览](./images/aai-query/query_tab.png)

接下来，选择 **[!UICONTROL 创建查询]** 中。 加载查询编辑器。 使用查询编辑器，您可以开始使用评分数据创建查询。

![查询编辑器](./images/aai-query/query_example.png)

有关查询编辑器的更多信息，请访问 [查询编辑器用户指南](../../query-service/ui/user-guide.md).

## 用于归因分析的查询模板

以下查询可用作不同分数分析方案的模板。 您需要将 `_tenantId` 和 `your_score_output_dataset` 的值。

>[!NOTE]
>
> 根据数据的摄取方式，使用以下值，例如 `timestamp` 格式可能不同。

### 验证示例

**按转化事件（在转化窗口内）划分的转化总数**

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

**仅转化事件的总数（在转化窗口内）**

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

**每日转化数**

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

### 分布分析示例

**按定义类型（在转化窗口内）划分的转化路径上的接触点数量**

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

### 分析生成示例

**按接触点和转化日期划分的增量单位（在转化窗口内）**

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

**按接触点和接触点日期划分的增量单位（在转化窗口内）**

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

**所有评分模型的特定接触点类型的汇总得分（在转化窗口内）**

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

获取每个转化事件类型的路径长度分布：

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

**高级 — 转化路径分析中的接触点数量不同**

获取每个转化事件类型的转化路径上不同接触点数量的分布：

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

### 架构扁平化和展开示例

此查询会将struct列拼合为多个单数列，并将数组分解为多行。 这有助于将归因得分转换为CSV格式。 此查询的输出具有一行中的一个转化，以及与该转化对应的接触点之一。

>[!TIP]
>
> 在本例中，您需要将 `{COLUMN_NAME}` 除 `_tenantId` 和 `your_score_output_dataset`. 的 `COLUMN_NAME` 变量可采用配置Attribution AI实例期间添加的可选传递列名称（报表列）的值。 请查看您的评分输出架构以查找 `{COLUMN_NAME}` 完成此查询所需的值。

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
