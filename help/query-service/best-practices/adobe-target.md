---
keywords: Experience Platform;home;popular topics;query service;Query service;sample queries;sample query;adobe target;
solution: Experience Platform
title: 示例查询
topic: queries
description: 来自Adobe Target的数据将转换为体验事件XDM模式，并作为数据集引入Experience Platform。 此文档包含将查询服务用于Adobe Target数据集的示例查询。
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 1%

---


# Adobe Target数据查询示例

来自Adobe Target的数据将转换为体验事件XDM模式，并作为数据集引入Adobe Experience Platform。 Adobe Experience Platform查询服务使用此数据有许多用例，以下示例查询应使用您的Adobe Target数据集。

在Experience Platform中，自动创建的数据集的名称为“Adobe Target体验事件”。 将此数据集与查询一起使用时，应使用名称`adobe_target_experience_events`。

## 高级部分XDM场映射

以下列表显示映射到其相应XDM字段的目标字段。

>[!NOTE]
>
> 在XDM字段中使用`[ ]`表示数组。

- mboxName:`_experience.target.mboxname`
- 活动 ID: `_experience.target.activities.activityID`
- 体验 ID: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- 区段ID:`_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- 事件范围：`_experience.target.activities[].activityEvents[].eventScope`
   - 此字段跟踪新访客和访问。
- 步骤ID:`_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - 此字段是用于Adobe Campaign的自定义步骤ID。
- 价格合计：`commerce.order.priceTotal`

## 示例查询

以下查询显示了Adobe Target常用查询的示例。

在以下示例中，您将需要编辑SQL，以根据您感兴趣的数据集、变量或评估时间范围来填写查询的预期参数。 在SQL中显示`{ }`时提供参数。

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

### 特定活动的每小时详细信息

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

### 特定活动的特定体验ID

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

### 按每个列表ID在指定一天按实例返回事件范围(访客、访问、印象)的活动

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

### 给定一天内每个访客的活动、访问次数和展示次数的返回计数

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

### 在指定的一天内返回访客、访问、体验ID、区段ID和EventScope的展示次数

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

### 返回给定日的mbox名称和记录计数

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
