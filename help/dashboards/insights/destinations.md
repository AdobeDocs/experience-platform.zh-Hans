---
title: 目标分析
description: 发现支持目标分析的SQL，并使用这些查询生成自定义分析，以进一步探索从Adobe Experience Platform激活数据的问题。
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 3%

---

# 目标洞察

通过分析数据模型而获得的见解，可使您的Adobe Real-Time CDP数据更易于访问、理解并影响决策。

通过访问支持这些分析的SQL来了解您的目标分析，然后生成您自己的分析以进一步探索如何将数据从Adobe Experience Platform激活到您的目标平台。 通过使用现有的Real-Time CDP数据模型SQL作为灵感，根据独特的业务需求创建查询，将原始数据转换为新的可操作洞察。

有关如何直接通过PLatform UI调整分析的SQL的详细信息，请参阅[查看SQL文档](../view-sql.md)。

以下分析均可用作[目标仪表板](../guides/destinations.md)或自定义[用户定义的仪表板](../standard-dashboards.md)的一部分。 有关如何自定义仪表板或[&#128279;](../customize/custom-widgets.md)在构件库和[用户定义的仪表板](../standard-dashboards.md#create-widget)中创建和编辑新构件的说明，请参阅[自定义概述](../customize/overview.md)。

## 已激活的受众 {#activated-audiences}

通过此洞察回答的问题：

- 按特定目标过滤的已激活受众的总数是多少？
- 每个目标的激活受众计数是多少？

+++选择以显示生成此分析的SQL

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

有关此分析的外观和功能的信息，请参阅[激活的受众小组件文档](../guides/destinations.md#activated-audiences)。

## 所有目标的活跃受众 {#activated-audiences-across-all-destinations}

通过此洞察回答的问题：

- 在所有目标中激活了多少受众？
- 激活的受众的总数是多少？

+++选择以显示生成此分析的SQL

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

有关此洞察的外观和功能的信息，请参阅所有目标构件文档中的[激活的受众](../guides/destinations.md#activated-audiences-across-all-destinations)。

## 按目标平台列出的活动目标 {#active-destinations-by-destination-platform}

通过此洞察回答的问题：

- 有多少个目标处于活动状态？
- 按目标平台划分的活动目标划分是什么？
- 按每个目标平台划分的活动目标数量是多少？

+++选择以显示生成此分析的SQL

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

有关此洞察的外观和功能的信息，请参阅[按目标平台划分的活动目标小组件文档](../guides/destinations.md#active-destinations-by-destination-platform)。

## 受众规模趋势 {#audience-size-trend}

通过此洞察回答的问题：

- 受众规模随时间的变化如何，包括映射到目标的受众的异常？
- 如何才能找到在30天、90天和12个月的指定时间段内按目标列出的受众规模整体趋势？
- 受众对规模有贡献的主要特征是什么，例如，任何电子邮件营销活动的尖峰是什么？

+++选择以显示生成此分析的SQL

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

有关此分析的外观和功能的信息，请参阅[受众规模趋势构件文档](../guides/destinations.md#audience-size-trend)。

## 普通受众 {#common-audiences}

通过此洞察回答的问题：

- 哪些受众在两个不同的目标之间通用？
- 两个不同目标之间的每个常见受众都有多少个配置文件？
- 两个目标映射到的最大受众是哪个？

+++选择以显示生成此分析的SQL

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

有关此分析的外观和功能的信息，请参阅[常用受众小组件文档](../guides/destinations.md#common-audiences)。

## 目标状态 {#destination-status}

通过此洞察回答的问题：

- 允许使用的目标总数是多少？
- 已禁用的目标总数是多少？
- 已启用目标和已禁用目标之间的百分比分摊是多少？

+++选择以显示生成此分析的SQL

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

有关此分析的外观和功能的信息，请参阅[目标状态构件文档](../guides/destinations.md#destination-status)。

## 目标计数 {#destinations-count}

通过此洞察回答的问题：

- 当前配置了多少个目标？
- 目标总数会如何随时间变化？

+++选择以显示生成此分析的SQL

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

有关此分析的外观和功能的信息，请参阅[目标计数构件文档](../guides/destinations.md#destinations-count)。

## 映射的受众健康 {#mapped-audience-health}

通过此洞察回答的问题：

- 哪些映射到目标的受众在过去30天内有显着变化？
- 映射受众的最新大小以及在上个月是否发生了更改？
- 如何根据上个月大小变化的严重程度列出映射到目标的所有受众？

+++选择以显示生成此分析的SQL

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

有关此分析的外观和功能的信息，请参阅[映射的受众运行状况小组件文档](../guides/destinations.md#mapped-audience-health)。

## 已映射受众 {#mapped-audiences}

通过此洞察回答的问题：

- 有多少受众映射到特定目标？
- 映射受众的数量会随时间发生何种变化？
- 可在何处比较两个目标以查看映射到每个目标的受众重叠？

+++选择以显示生成此分析的SQL

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

有关此分析的外观和功能的信息，请参阅[映射的受众小组件文档](../guides/destinations.md#mapped-audiences)。

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## 最常用的目标 {#most-used-destinations}

通过此洞察回答的问题：

- 最常用的目标有哪些？
- 每个目标映射到多少受众，按最多到最少排序？
- 将受众映射到目标会如何从一个快照更改为另一个快照？

+++选择以显示生成此分析的SQL

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

有关此分析的外观和功能的信息，请参阅[最常用的目标构件文档](../guides/destinations.md#most-used-destinations)。

## 最近激活的受众 {#recently-activated-audiences}

通过此洞察回答的问题：

- 受众最近激活到哪个目标？
- 如何查找按上次更新日期排序的所有目标的列表？
- 如何根据最近的激活比较两个目标？

+++选择以显示生成此分析的SQL

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

有关此分析的外观和功能的信息，请参阅[最近激活的受众小组件文档](../guides/destinations.md#recently-activated-audiences)。

## 最近激活的受众（按目标） {#recently-activated-audiences-by-destination}

通过此洞察回答的问题：

- 哪些受众已激活到特定目标？
- 如何查找由特定受众激活的受众列表（从最近到最近）？
- 如何按为特定目标激活的日期查找受众列表？

+++选择以显示生成此分析的SQL

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

有关此分析的外观和功能的信息，请参阅[目标构件最近激活的受众文档](../guides/destinations.md#recently-activated-audiences-by-destination)。

## 最近创建的目标 {#recently-created-destinations}

通过此洞察回答的问题：

- 哪些是最近创建的目标？
- 如何查找目标列表及其创建日期？
- 最近创建了什么新目标？

+++选择以显示生成此分析的SQL

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

有关此分析的外观和功能的信息，请参阅[最近创建的目标构件文档](../guides/destinations.md#recently-created-destinations)。

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## 后续步骤 {#next-steps}

通过阅读本文档，您现在了解了生成仪表板分析的SQL以及此分析可以解决哪些常见问题。 您现在可以编辑和迭代这些SQL查询以生成您自己的见解。

有关如何直接通过PLatform UI调整分析的SQL的详细信息，请参阅[查看SQL文档](../view-sql.md)。

您还可以阅读并了解为[配置文件](./profiles.md)、[帐户配置文件](./account-profiles.md)和[受众](./audiences.md)仪表板生成分析的SQL。
