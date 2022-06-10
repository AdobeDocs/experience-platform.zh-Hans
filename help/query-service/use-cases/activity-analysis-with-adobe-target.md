---
title: 使用Adobe Target进行活动分析
description: 本文档介绍如何使用查询服务从使用Adobe Target数据创建的数据集创建可操作的分析。
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 3%

---

# 使用Adobe Target进行活动分析

Adobe Experience Platform允许您使用体验数据模型(XDM)字段从Adobe Target中摄取数据，以创建数据集以与查询服务结合使用。 由于Adobe Target旨在自定义内容和个性化用户体验，因此在这些数据集上运行的查询通过SQL分析用户活动可获得高度个性化且重点突出的洞察。

本文档提供了各种基于客户行为和特征的示例SQL查询，以演示常见用例。

## 快速入门

对于以下每个用例，都提供了参数化SQL查询示例作为模板供您进行自定义。 无论您在何处看到，都提供参数 `{ }` 在SQL示例中，您希望进行评估。

## 高级部分XDM字段映射

下表列出了常用的Target字段及其映射到的相应XDM字段。

>[!NOTE]
>
>的使用 `[ ]` 在XDM字段中，表示数组。

| 目标字段名称 | XDM字段名称 | 注释 |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | 不适用 |
| 活动 ID | `_experience.target.activities.activityID` | 不适用 |
| 体验 ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | 不适用 |
| 区段ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | 不适用 |
| 事件范围 | `_experience.target.activities[].activityEvents[].eventScope` | 此字段跟踪新访客和访问。 |
| 步骤ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | 此字段是Adobe Campaign的自定义步骤ID。 |
| 总价 | commerce.order.priceTotal | 不适用 |

>[!IMPORTANT]
>
>使用Target数据自动创建的数据集的名称为“Adobe Target Experience Events”。 在使用此数据集进行查询时，请使用名称 `adobe_target_experience_events`.

## 目标

通过分析用户活动，您可以为特定受众个性化内容，并为单个实体测试内容的不同版本。 此外，通过分析给定时间段内或针对单个用户的特定活动，可以更清楚地了解每个活动的性能。 可以利用此组合分析的结果来了解每个活动的性能。

以下个性化用例是使用Adobe Target数据创建的，其重点是用户活动，以便对客户在业务应用程序上的行为提供有价值的分析。

本指南通过用例示例说明了以下关键概念：

* 要了解活动ID在给定日期的性能，例如计数、详细信息和关联的体验ID。
* 确定活动的访客和事件范围。
* 收集体验ID、区段ID和活动ID的访客计数、访问次数和展示次数信息。

### 为给定日期生成每小时活动计数

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### 生成特定特定的每小时详细信息

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### 确定特定活动在给定日期的体验ID列表

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 返回给定日内每个活动ID的事件范围（访客、访问、展示次数）列表（按实例）

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 确定给定日期内每个活动的访客数、访问次数和展示次数

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### 确定给定日期的体验ID、区段ID和EventScope的访客数、访问次数和展示次数

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

### 返回给定日期的mbox名称和记录计数

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
