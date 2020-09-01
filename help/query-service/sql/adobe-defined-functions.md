---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: Adobe定义函数
topic: functions
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 3%

---


# Adobe定义函数

Adobe定义的函数(ADF)是预建的函数，可 [!DNL Query Service] 帮助对数据执行常见的业务相关 [!DNL ExperienceEvent] 任务。 这些功能包括会话化和归因功能，如Adobe Analytics的功能。 请参阅 [Adobe Analytics文档](https://docs.adobe.com/content/help/zh-Hans/analytics/landing/home.html) ，进一步了解Adobe Analytics以及本页中定义的ADF背后的概念。 此文档提供中提供的Adobe定义函数的信息 [!DNL Query Service]。

## 窗口函数

大多数业务逻辑要求为客户收集接触点并按时订购。 此支持由SQL以 [!DNL Spark] 窗口函数的形式提供。 窗口函数是标准SQL的一部分，并受许多其他SQL引擎支持。

窗口函数会更新聚合，并为有序子集中的每行返回单个项目。 最基本的聚合函数是 `SUM()`。 `SUM()` 取行，总计给您一次。 如果改为应 `SUM()` 用到窗口，将其转换为窗口函数，则每行将收到累计和。

大多数SQL帮 [!DNL Spark] 助程序都是窗口函数，可更新窗口中的每一行，并添加该行的状态。

### 规范

语法：`OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| [分区] | 基于列或可用字段的行的子组。 示例, `PARTITION BY endUserIds._experience.mcid.id` |
| [订单] | 用于对子集或行排序的列或可用字段。 示例, `ORDER BY timestamp` |
| [帧] | 分区中行的子组。 示例, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 会话化

当您处理来自网站 [!DNL ExperienceEvent] 、移动应用程序、交互语音应答系统或任何其他客户交互渠道的数据时，如果事件可以围绕相关的活动周期进行分组，则会有所帮助。 通常，您具有驱动活动的特定意图，如研究产品、支付账单、检查帐户余额、填写应用程序等。 此分组有助于关联事件，以发现有关客户体验的更多上下文。

有关Adobe Analytics会话的更多信息，请参阅上下文感 [知会话的相关文档](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)。

### 规范

语法：`SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `expirationInSeconds` | 事件之间需要的秒数，以确定当前会话的结束和新会话的开始 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `timestamp_diff` | 当前记录与先前记录之间的时间（以秒为单位） |
| `num` | 窗口函数中定义的键的唯一会话编号，从 `PARTITION BY` 1开始。 |
| `is_new` | 用于标识记录是否是会话的第一个的布尔值 |
| `depth` | 会话中当前记录的深度 |

#### 示例查询

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

#### 结果

```console
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

## 归因

将客户行动与成功关联是了解影响客户体验的因素的重要部分。 以下ADF支持具有不同过期设置的“第一个”和“最后一个”属性。

有关Adobe Analytics归因的更多信息，请参 [阅分析指](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html) 南中的 [!DNL Analytics] Attribution IQ概述。

### 首次触碰归因

返回渠道数据集中单个目标的首次触摸归因值和详细 [!DNL ExperienceEvent] 信息。 该查询返回一 `struct` 个对象，该对象具有为选定渠道返回的每行返回的首次触摸值、时间戳和属性。

如果您想了解哪些交互导致了一系列客户操作，此查询非常有用。 在以下示例中，数据中的初始跟踪`em:946426`代码( [!DNL ExperienceEvent] )由客户操作的100%(`1.0`)责任来归因，因为它是第一次交互。

### 规范

语法：`ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 在返回的对象中用作标签的友好名称 |
| `channelValue` | 作为目标渠道的列或字段 |


| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 来自的 `channelValue` 值是 [!DNL ExperienceEvent] |
| `timestamp` | 首次触 [!DNL ExperienceEvent] 摸的时间戳 |
| `fraction` | 首次接触的归因表示为分数信用 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

#### 结果

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

### 上次联系归因

返回目标数据集中单个渠道的上次触摸归因值和详细 [!DNL ExperienceEvent] 信息。 查询返回一个 `struct` 对象，该对象具有为所选渠道返回的每行的上次触摸值、时间戳和属性。

如果您希望在一系列客户操作中看到最终交互，此查询非常有用。 在以下示例中，返回对象中的跟踪代码是每个记录中的最后一次 [!DNL ExperienceEvent] 交互。 每个代码都由客户行`1.0`动的100%()责任来承担，因为它是上次交互。

### 规范

语法：`ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 在返回的对象中用作标签的友好名称 |
| `channelValue` | 作为目标渠道的列或字段 |


| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 该值 `channelValue` 是 [!DNL ExperienceEvent] |
| `timestamp` | 使用时间 [!DNL ExperienceEvent] 的时 `channelValue` 间戳 |
| `fraction` | 最后一次接触的归因表示为分数信用 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### 结果

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

### 具有过期条件的首次联系归因

返回渠道数据集中单个目标的首次触摸归因值和详细信息，该在某个条 [!DNL ExperienceEvent] 件之后或之前过期。 该查询返回一 `struct` 个对象，该对象具有为选定渠道返回的每行返回的首次触摸值、时间戳和属性。

如果您想要查看哪些交互导致在数据集中由选择条件决定的一部分内执行一系列 [!DNL ExperienceEvent] 客户操作，此查询很有用。 在以下示例中，将(`commerce.purchases.value IS NOT NULL`)在结果（7月15日、21日、23日和29日）显示的四天中的每天记录购买，并且每天的初始跟踪代码将对客户操作承担100%(`1.0`)责任。

#### 规范

语法：`ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 在返回的对象中用作标签的友好名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expCondition` | 确定渠道到期点的条件 |
| `expBefore` | 默认为 `false`。用于指示渠道在满足指定条件之前还是之后过期的布尔值。 主要针对会话到期条件启用( `sess.depth = 1, true`例如)，以确保不从上一个会话中选择第一次触摸。 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 该值 `channelValue`[!DNL ExperienceEvent] 是 `expCondition` |
| `timestamp` | 首次触 [!DNL ExperienceEvent] 摸的时间戳 |
| `fraction` | 首次接触的归因表示为分数信用 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### 结果

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### 具有过期超时的首次触摸归因

返回指定时间段内渠道数据集中单个目标的首次触 [!DNL ExperienceEvent] 摸归因值和详细信息。 该查询返回一 `struct` 个对象，该对象具有为选定渠道返回的每行返回的首次触摸值、时间戳和属性。 如果您想要查看在选定时间间隔内导致客户操作的交互情况，此查询很有用。 在以下示例中，每次客户操作返回的第一次接触是前七天()内的最早交互`expTimeout = 86400 * 7`操作。

#### 规范

语法：`ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 在返回的对象中用作标签的友好名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expTimeout` | 渠道事件前查询搜索第一次触摸事件的时间窗口（以秒为单位） |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 在指定 `channelValue` 间隔内首次触摸的值 `expTimeout` 。 |
| `timestamp` | 首次触 [!DNL ExperienceEvent] 摸的时间戳 |
| `fraction` | 首次接触的归因表示为分数信用 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### 结果

```console
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### 具有过期条件的上次联系归因

返回渠道数据集中单个目标的上次触摸归因值和详细信 [!DNL ExperienceEvent] 息，该值在条件之后或之前过期。 查询返回一个 `struct` 对象，该对象具有为所选渠道返回的每行的上次触摸值、时间戳和属性。 如果您希望查看由选择条件决定的数据集的一部分中的一系列客户操作中的 [!DNL ExperienceEvent] 最后一次交互，此查询很有用。 在以下示例中，将(`commerce.purchases.value IS NOT NULL`)在结果（7月15日、21日、23日和29日）显示的四天中的每天记录购买，并将每天的最后跟踪代码归为客户操作的100%(`1.0`)责任。

#### 规范

语法：`ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 在返回的对象中用作标签的友好名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expCondition` | 确定渠道到期点的条件 |
| `expBefore` | 默认为 `false`。用于指示渠道在满足指定条件之前还是之后过期的布尔值。 主要针对会话到期条件启用( `sess.depth = 1, true`例如)，以确保不从上一个会话中选择上次触摸。 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 该值 `channelValue`[!DNL ExperienceEvent] 是 `expCondition` |
| `timestamp` | 上次触 [!DNL ExperienceEvent] 摸的时间戳 |
| `percentage` | 最后一次接触的归因表示为分数信用 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### 结果

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### 具有过期超时的上次联系归因

返回指定时间段内渠道数据集中单个目标的上次触 [!DNL ExperienceEvent] 摸归因值和详细信息。 查询返回一个 `struct` 对象，该对象具有为所选渠道返回的每行的上次触摸值、时间戳和属性。 如果要查看所选时间间隔内的最后一次交互，此查询很有用。 在以下示例中，每次客户操作返回的最后一次联系是后七天()内的最终交互`expTimeout = 86400 * 7`操作。

#### 规范

语法：`ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 在返回的对象中用作标签的友好名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expTimeout` | 渠道在事件搜索最后一次触摸事件后的时间窗口（以秒为单位） |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 在指定 `channelValue` 间隔内的上次触摸的值 `expTimeout` 。 |
| `timestamp` | 上次触 [!DNL ExperienceEvent] 摸的时间戳 |
| `percentage` | 最后一次接触的归因表示为分数信用 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### 结果

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

## 上一次／下一次触摸

了解客户如何在体验中导航非常重要。 它可用于了解客户的深度参与度、确认体验的预期步骤是否按设计方式运行并确定影响客户的潜在痛点。 以下ADF支持根据“上一个”和“下一个”关系建立路径视图。 您将能够创建上一页和下一页，或分步创建多个事件。

### 上一次触摸

确定特定字段的上一个值以及在窗口内定义的多个步骤。 在示例中，请注 `WINDOW` 意，“函数”配置了一 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 个框架，设置ADF查看当前行以及之前的所有行。

#### 规范

语法：`PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `key` | 事件中的列或字段。 |
| `shift` | （可选）远离当前事件的事件数。 默认值为1。 |
| `ingnoreNulls` | 要指示是否应忽 `key` 略null值的布尔值。 Default is `false`. |


| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `value` | 基于ADF中 `key` 使用的值 |

#### 示例查询

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### 结果

```console
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

### 下一次触摸

确定特定字段的下一个值，即在窗口内定义数量的步骤。 在示例中，请注 `WINDOW` 意，“函数”配置了 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 一个框架，设置ADF查看当前行，并查看其后的所有行。

#### 规范

语法：`NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `key` | 事件中的列或字段 |
| `shift` | （可选）远离当前事件的事件数。 默认值为1。 |
| `ingnoreNulls` | 要指示是否应忽 `key` 略null值的布尔值。 Default is `false`. |


| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `value` | 基于ADF中 `key` 使用的值 |

#### 示例查询

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### 结果

```console
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

## 中间时间

中间时间允许您在事件发生之前或之后的一段时间内探索潜在的客户行为。 查看所有客户在活动或其他类型事件后7天内的事件。

### 上次匹配的时间间隔

提供新的维度，它测量自特定事件以来经过的时间。

#### 规范

语法：`TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在所有事件上填充的数据集中找到时间戳字段。 |
| `eventDefintion` | 表达式，以限定前一个事件。 |
| `timeUnit` | 输出单位：天、小时、分钟和秒。 默认为秒。 |

输出：返回一个数字，表示自查看上一个匹配事件以来的时间单位；如果未找到匹配事件，则返回为null。

#### 示例查询

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

#### 结果

```console
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

### 下次匹配的时间间隔

提供新维度，它测量特定事件发生前的时间。

#### 规范

语法：`TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在所有事件上填充的数据集中找到时间戳字段。 |
| `eventDefintion` | 表达式以确定下一个事件。 |
| `timeUnit` | 输出单位：天、小时、分钟和秒。 默认为秒。 |

输出：返回一个负数，表示下一个匹配事件后的时间单位；如果找不到匹配事件，则返回null。

#### 示例查询

```sql
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

#### 结果

```console
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

## 后续步骤

使用此处描述的函数，您可以编写查询来使用访问您自己 [!DNL ExperienceEvent] 的数据集 [!DNL Query Service]。 有关在中创作查询的详 [!DNL Query Service]细信息，请参阅有关创建 [查询的文档](../creating-queries/creating-queries.md)。
