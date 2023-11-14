---
title: Real-time Customer Data Platform分析数据模型
description: 了解如何将SQL查询与Real-time Customer Data Platform分析数据模型结合使用，以自定义您自己的营销和KPI用例的Real-Time CDP报表。
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: e55bbba92b0e3b9c86a9962ffa0131dfb7c15e77
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 2%

---

# Real-time Customer Data Platform分析数据模型

Real-time Customer Data Platform分析数据模型功能可公开支持各种个人资料、目标和分段构件分析的数据模型和SQL。 您可以自定义这些SQL查询模板，以便为营销和关键绩效指标(KPI)用例创建Real-Time CDP报表。 这些见解随后可用作用户定义的功能板的自定义构件。 请参阅query accelerated store报告见解文档以了解 [如何通过查询服务构建报表见解数据模型，以便与加速的商店数据和用户定义的仪表板一起使用](../query-service/data-distiller/query-accelerated-store/reporting-insights-data-model.md).

## 先决条件

本指南要求您对 [用户定义的仪表板功能](./user-defined-dashboards.md). 在继续阅读本指南之前，请先阅读文档。

## Real-Time CDP分析报告和用例

Real-Time CDP报表可提供有关您的配置文件数据及其与受众和目标的关系的见解。 开发各种星型架构模型来回答各种常见的营销用例，每个数据模型可以支持多个用例。

>[!IMPORTANT]
>
>用于Real-Time CDP报表的数据对于所选的合并策略和最近的每日快照而言是准确的。

### 配置文件模型 {#profile-model}

用户档案模型由三个数据集组成：

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

下图包含每个数据集中的相关数据字段。

![轮廓模型的ERD。](./images/cdp-insights/profile-model.png)

#### 用户档案计数用例

用于配置文件计数小部件的逻辑会返回生成快照时配置文件存储中合并的配置文件总数。 请参阅 [[!UICONTROL 配置文件计数] 构件文档](./guides/profiles.md#profile-count) 以了解更多信息。

生成 [!UICONTROL 配置文件计数] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_profiles) CNT
FROM qsaccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
AND adwh_fact_profile.merge_policy_id=${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

#### 单一身份配置文件用例

用于的逻辑 [!UICONTROL 单一身份配置文件] 小组件提供贵组织只有一种类型的ID类型来创建其身份的配置文件的计数。 请参阅[[!UICONTROL 单一身份配置文件] 构件文档](./guides/profiles.md#single-identity-profiles) 以了解更多信息。

生成 [!UICONTROL 单一身份配置文件] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT adwh_dim_merge_policies.merge_policy_name,
  sum(adwh_fact_profile.count_of_Single_Identity_profiles) CNT
FROM QSAccel.profile_agg.adwh_fact_profile
LEFT OUTER JOIN QSAccel.profile_agg.adwh_dim_merge_policies ON adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
WHERE adwh_fact_profile.date_key='${lastProcessDate}'
  AND adwh_fact_profile.merge_policy_id =${mergePolicyId}
GROUP BY adwh_dim_merge_policies.merge_policy_name;
```

+++

### 命名空间模型 {#namespace-model}

命名空间模型由以下数据集组成：

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

下图包含每个数据集中的相关数据字段。

![命名空间模型的ERD。](./images/cdp-insights/namespace-model.png)

#### 按身份用例列出的配置文件

此 [!UICONTROL 按身份列出的配置文件] 构件显示配置文件存储中所有合并配置文件的身份细分。 请参阅 [[!UICONTROL 按身份列出的配置文件] 构件文档](./guides/profiles.md#profiles-by-identity) 以了解更多信息。

生成 [!UICONTROL 按身份列出的配置文件] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT adwh_dim_namespaces.namespace_description,
    sum(adwh_fact_profile_by_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
JOIN qsaccel.profile_agg.adwh_dim_namespaces ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_namespace.merge_policy_id =${mergePolicyId}
AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
GROUP BY adwh_fact_profile_by_namespace.date_key,
        adwh_fact_profile_by_namespace.merge_policy_id,
        adwh_dim_namespaces.namespace_description
ORDER BY count_of_profiles DESC
LIMIT 5;
```

+++

#### 按身份用例的单一身份配置文件

用于的逻辑 [!UICONTROL 按身份列出的单一身份配置文件] 构件说明仅使用单个唯一标识符标识的用户档案总数。 请参阅 [按身份构件文档的单一身份配置文件](./guides/profiles.md#single-identity-profiles-by-identity) 以了解更多信息。

生成 [!UICONTROL 按身份列出的单一身份配置文件] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT
  adwh_dim_namespaces.namespace_description,
  sum(adwh_fact_profile_by_namespace.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_namespace
  LEFT OUTER JOIN
    qsaccel.profile_agg.adwh_dim_namespaces
    ON adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE
  adwh_fact_profile_by_namespace.merge_policy_id=${mergePolicyId}
  AND adwh_fact_profile_by_namespace.date_key='${lastProcessDate}'
GROUP BY
  adwh_fact_profile_by_namespace.date_key,
  adwh_fact_profile_by_namespace.merge_policy_id,
  adwh_dim_namespaces.namespace_description;
```

+++

### 受众模型 {#audience-model}

受众模型由以下数据集组成：

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下图包含每个数据集中的相关数据字段。

![受众模型的ERD](./images/cdp-insights/audience-model.png)

#### 受众规模用例

用于的逻辑 [!UICONTROL 受众规模] 构件会返回在生成最新快照时选定受众中合并的配置文件总数。 请参阅 [[!UICONTROL 受众规模] 构件文档](./guides/audiences.md#audience-size) 以了解更多信息。

生成 [!UICONTROL 受众规模] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT adwh_fact_profile_by_segment.date_key,
       adwh_dim_merge_policies.merge_policy_name,
       adwh_dim_segments.segment,
       adwh_dim_segments.segment_name,
       sum(adwh_fact_profile_by_segment.count_of_profiles)count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE adwh_fact_profile_by_segment.date_key ='${lastProcessDate}'
  AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY adwh_fact_profile_by_segment.date_key,
         adwh_dim_merge_policies.merge_policy_name,
         adwh_dim_segments.segment,
         adwh_dim_segments.segment_name
ORDER BY count_of_profiles DESC
LIMIT 20;
```

+++

#### 受众规模变化趋势用例

用于的逻辑 [!UICONTROL 受众规模变化趋势] 构件以折线图说明了最近每日快照之间符合给定受众条件的配置文件总数的差异。 请参阅 [[!UICONTROL 受众规模变化趋势] 构件文档](./guides/audiences.md#audience-size-change-trend) 以了解更多信息。

生成 [!UICONTROL 受众规模变化趋势] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT DISTINCT cast(adwh_dim_segments.create_date AS Date) Date_key, adwh_dim_merge_policies.merge_policy_name,
  count(DISTINCT adwh_dim_segments.segment_id)Segments_Added
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment
JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_fact_profile_by_segment.segment_id = adwh_dim_segments.segment_id
JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON adwh_fact_profile_by_segment.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
WHERE Cast(adwh_dim_segments.create_date AS date) >= dateadd(DAY, - ${dayRange}, '${lastProcessDate}')
AND adwh_fact_profile_by_segment.merge_policy_id=${mergePolicyId}
GROUP BY cast(adwh_dim_segments.create_date AS date), adwh_dim_merge_policies.merge_policy_name ;
```

+++

#### 最常用的目标用例

中使用的逻辑 [!UICONTROL 最常用的目标] 构件根据映射到贵组织最常用目标的受众数量列出这些目标。 此排名可让您深入了解哪些目标正在被利用，同时还可能会显示那些可能未被充分利用的目标。 请参阅有关以下内容的文档 [[!UICONTROL 最常用的目标] 构件](./guides/destinations.md#most-used-destinations) 以了解更多信息。

生成 [!UICONTROL 最常用的目标] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT
   adwh_dim_destination.destination_name, adwh_dim_destination.destination_id,
   count( distinct adwh_dim_br_segment_destinations.segment_id ) segment_count
FROM
   qsaccel.profile_agg.adwh_dim_destination
   join qsaccel.profile_agg.adwh_dim_br_segment_destinations
 ON
   adwh_dim_destination.destination_id = adwh_dim_br_segment_destinations.destination_id
 WHERE
   adwh_dim_destination.destination_name is not null
 group by
   adwh_dim_destination.destination_name,
   adwh_dim_destination.destination_id
   order by segment_count desc limit 5;
```

+++

#### 最近激活的受众用例

的逻辑 [!UICONTROL 最近激活的受众] 构件提供最近映射到目标的受众列表。 此列表提供系统中正使用的受众和目标的快照，并且可以帮助纠正任何错误的映射。请参阅 [[!UICONTROL 最近激活的受众] 构件文档](./guides/destinations.md#recently-activated-audiences) 以了解更多信息。

生成 [!UICONTROL 最近激活的受众] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT segment_name, segment, destination_name, a.create_time create_time
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY create_time desc, segment LIMIT 5;
```

+++

### 命名空间 — 受众模型

namespace-audience模型包含以下数据集：

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下图包含每个数据集中的相关数据字段。

![命名空间 — 受众模型的ERD。](./images/cdp-insights/namespace-audience-model.png)

#### 受众用例的按身份列出的配置文件

中使用的逻辑 [!UICONTROL 按身份列出的配置文件] 小组件提供给定受众的个人资料存储中所有合并个人资料的身份细分。 请参阅 [[!UICONTROL 按身份列出的配置文件] 构件文档](./guides/audiences.md#profiles-by-identity) 以了解更多信息。

生成 [!UICONTROL 按身份列出的配置文件] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT adwh_dim_namespaces.namespace_description,
  sum( adwh_fact_profile_by_segment_and_namespace.count_of_profiles) count_of_profiles
FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces
ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
WHERE adwh_fact_profile_by_segment_and_namespace.segment_id = {segment_id}
AND adwh_fact_profile_by_segment_and_namespace.merge_policy_id = {merge_policy_id}
AND adwh_fact_profile_by_segment_and_namespace.date_key = '{date}'
GROUP BY adwh_dim_namespaces.namespace_description;
```

+++

### 重叠命名空间模型

重叠命名空间模型由以下数据集组成：

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

下图包含每个数据集中的相关数据字段。

![重叠命名空间模型的ERD。](./images/cdp-insights/overlap-namespace-model.png)

#### 身份重叠（配置文件）用例

中使用的逻辑 [!UICONTROL 身份重叠] 小组件显示您的配置文件中重叠的 **配置文件存储** 包含两个所选身份的文件。 欲了解更多信息，请参见 [[!UICONTROL 身份重叠] 的小组件部分 [!UICONTROL 配置文件] 仪表板文档](./guides/profiles.md#identity-overlap).

生成 [!UICONTROL 身份重叠] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT Sum(overlap_col1) overlap_col1,
       Sum(overlap_col2) overlap_col2,
       coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
     WHERE adwh_fact_profile_overlap_of_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_overlap_of_namespace.date_key = '${lastProcessDate}'
       AND adwh_fact_profile_overlap_of_namespace.overlap_id IN
         (SELECT adwh_dim_overlap_namespaces.overlap_id
          FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
          WHERE adwh_dim_overlap_namespaces.merge_policy_id=${mergePolicyId}
            AND adwh_dim_overlap_namespaces.overlap_namespaces IN ('${namespace1}',
                                                                   '${namespace2}')
          GROUP BY adwh_dim_overlap_namespaces.overlap_id
          HAVING Count(*) > 1)
     UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace1}'
     UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
     FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace
     JOIN qsaccel.profile_agg.adwh_dim_namespaces ON
     adwh_fact_profile_by_namespace.namespace_id = adwh_dim_namespaces.namespace_id
     AND adwh_fact_profile_by_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
     WHERE adwh_fact_profile_by_namespace.merge_policy_id = ${mergePolicyId}
       AND adwh_fact_profile_by_namespace.date_key = '${lastProcessDate}'
       AND adwh_dim_namespaces.namespace_description = '${namespace2}' ) a;
```

+++

### 按受众模型重叠命名空间

按照受众模型，重叠命名空间由以下数据集组成：

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

下图包含每个数据集中的相关数据字段。

![按受众模型列出的重叠命名空间的ERD。](./images/cdp-insights/overlap-namespace-by-audience-model.png)

#### 身份重叠（受众）用例

中使用的逻辑 [!UICONTROL 受众] 仪表板 [!UICONTROL 身份重叠] 构件展示包含特定受众的两个选定身份的用户档案重叠。 欲了解更多信息，请参见 [[!UICONTROL 身份重叠] 的小组件部分 [!UICONTROL 受众] 仪表板文档](./guides/audiences.md#identity-overlap).

生成 [!UICONTROL 身份重叠] 可以在下面的可折叠部分中看到构件。

+++SQL查询

```sql
SELECT
   Sum(overlap_col1) overlap_col1,
   Sum( overlap_col2) overlap_col2,
   Sum(overlap_count) Overlap_count
FROM
   (
      SELECT
         0 overlap_col1,
         0 overlap_col2,
         Sum(count_of_profiles) Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
      WHERE
         adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = $ {segmentId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '${lastProcessDate}'
         and adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
         (
            SELECT
               adwh_dim_overlap_namespaces.overlap_id
            FROM
               qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE
               adwh_dim_overlap_namespaces.merge_policy_id =$ {mergePolicyId}
               AND adwh_dim_overlap_namespaces.overlap_namespaces IN
               (
                  '${namespace1}',
                  '${namespace2}'
               )
            GROUP BY
               adwh_dim_overlap_namespaces.overlap_id
            HAVING
               Count(*) > 1
         )
      UNION ALL
      SELECT
         count_of_profiles overlap_col1,
         0 overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace1}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
      UNION ALL
      SELECT
         0 overlap_col1,
         count_of_profiles overlap_col2,
         0 Overlap_count
      FROM
         qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace
         LEFT OUTER JOIN
            qsaccel.profile_agg.adwh_dim_namespaces
            ON adwh_fact_profile_by_segment_and_namespace.namespace_id = adwh_dim_namespaces.namespace_id
            and adwh_fact_profile_by_segment_and_namespace.merge_policy_id = adwh_dim_namespaces.merge_policy_id
      WHERE
         adwh_dim_namespaces.namespace_description = '${namespace2}'
         and adwh_fact_profile_by_segment_and_namespace.segment_id = $ {segmentId}
         and adwh_fact_profile_by_segment_and_namespace.merge_policy_id =$ {mergePolicyId}
         and adwh_fact_profile_by_segment_and_namespace.date_key = '${lastProcessDate}'
   )
   a;
```

+++
