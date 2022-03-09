---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；示例查询；示例查询；Adobe Target;
solution: Experience Platform
title: Adobe Target数据的查询示例
topic-legacy: queries
description: 来自Adobe Target的数据将转换为Experience Event XDM架构，并作为数据集摄取到Experience Platform。 本文档包含有关将查询服务与Adobe Target数据集结合使用的示例查询。
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
source-git-commit: c0e7ae8f65aa0373d35a55d4da46e0ffcb0e60f9
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# Adobe Target数据查询示例

来自Adobe Target的数据将转换为Experience Event XDM架构，并作为数据集摄取到Adobe Experience Platform。 Adobe Experience Platform查询服务有许多使用此数据的用例，以下示例查询应可与Adobe Target数据集配合使用。

在Experience Platform中，自动创建的数据集的名称为“Adobe Target体验事件”。 将此数据集与查询结合使用时，应使用名称 `adobe_target_experience_events`.

## 高级部分XDM字段映射

以下列表显示了映射到其相应XDM字段的Target字段。

>[!NOTE]
>
> 的使用 `[ ]` 在XDM字段中，表示数组。

- mboxName: `_experience.target.mboxname`
- 活动 ID: `_experience.target.activities.activityID`
- 体验 ID: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- 区段ID: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- 事件范围： `_experience.target.activities[].activityEvents[].eventScope`
   - 此字段跟踪新访客和访问。
- 步骤ID: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - 此字段是Adobe Campaign的自定义步骤ID。
- 总价： `commerce.order.priceTotal`

## 示例查询

以下查询显示了与Adobe Target一起使用的常见查询示例。

在以下示例中，您将需要编辑SQL以根据您感兴趣的评估数据集、变量或时间范围填写查询的预期参数。 无论您在何处看到，都提供参数 `{ }` 在SQL中。

### 给定日的每小时活动计数

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

### 特定活动在给定日期的每小时详细信息

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

### 特定活动在给定日期的体验ID

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
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
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
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### 给定日期内每个活动的访客数、访问次数和展示次数的回访计数

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### 给定日期的回访访客数、访问次数、体验ID、区段ID和EventScope的展示次数

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
