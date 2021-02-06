---
keywords: 洞察；归因ai；归因ai洞察；AAI查询服务；归因查询；归因得分
solution: Intelligent Services, Experience Platform
title: 使用查询服务分析归因得分
topic: Attribution AI queries
description: 了解如何使用Adobe Experience Platform查询服务分析Attribution AI分数。
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# 使用查询服务分析归因得分

数据中的每一行都表示转换，在转换中，相关触点的信息将作为`touchpointsDetail`列下的结构数组存储。

| 触点信息 | 栏目 |
| ---------------------- | ------ |
| 触点名称 | `touchpointsDetail. touchpointName` |
| 触点渠道 | `touchpointsDetail.touchPoint.mediaChannel` |
| 触点Attribution AI算法得分 | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## 查找数据路径

在Adobe Experience PlatformUI中，在左侧导航中选择&#x200B;**[!UICONTROL 数据集]**。 将显示&#x200B;**[!UICONTROL 数据集]**&#x200B;页。 接下来，选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡并查找Attribution AI得分的输出数据集。

![访问实例](./images/aai-query/datasets_browse.png)

选择输出数据集。 此时将显示数据集活动页。

![数据集活动页](./images/aai-query/select_preview.png)

在数据集活动页面中，选择右上角的&#x200B;**[!UICONTROL 预览数据集]**&#x200B;预览数据集，以数据并确保数据按预期方式摄取。

![预览数据集](./images/aai-query/preview_dataset.JPG)

预览模式后，在右边栏中选择数据。 将出现一个带模式名称和说明的弹出窗口。 选择模式名称超链接以重定向到评分模式。

![选择模式](./images/aai-query/select_schema.png)

使用评分模式，您可以选择或搜索值。 选择后，**[!UICONTROL 字段属性]**&#x200B;侧边栏将打开，允许您复制路径以用于创建查询。

![复制路径](./images/aai-query/copy_path.png)

## 访问查询服务

要从平台UI中访问查询服务，请在左侧导航中选择&#x200B;**[!UICONTROL 查询]**，然后选择&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡。 将加载先前保存的列表的查询。

![查询服务浏览](./images/aai-query/query_tab.png)

接下来，选择右上角的&#x200B;**[!UICONTROL 创建查询]**。 加载查询编辑器。 使用查询编辑器，您可以开始使用评分数据创建查询。

![查询编辑器](./images/aai-query/query_example.png)

有关查询编辑器的详细信息，请访问[查询编辑器用户指南](../../query-service/ui/user-guide.md)。

## 查询模板，用于归因得分分析

以下查询可用作不同得分分析的模板。 您需要将`_tenantId`和`your_score_output_dataset`替换为评分输出模式中找到的正确值。

>[!NOTE]
>
> 根据数据的摄取方式，以下使用的值（如`timestamp`）的格式可能不同。

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

**每天转换数**

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

**按接触点和转换日期划分的增量单位（在转换窗口中）**

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

**按触点和触点日期划分的增量单位（在转换窗口中）**

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

**高级——路径长度分析**

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

**高级——转换路径分析上的接触点数目不同**

获取每个转换事件类型在转换路径上的不同接触点数的分布：

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
