---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe定义的函数
topic: functions
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Adobe定义的函数

Adobe定义的功能(ADF)是查询服务中预建的功能，可帮助对ExperienceEvent数据执行常见的业务相关任务。 这些功能包括会话化和归因功能，如Adobe Analytics中的功能。 有关Adobe Analytics的更多信息 [](https://docs.adobe.com/content/help/en/analytics/landing/home.html) ，请参阅Adobe Analytics文档以及本页中定义的ADF背后的概念。 本文档提供查询服务中可用的Adobe定义功能的信息。

## 窗口功能

大部分业务逻辑需要为客户收集接触点并按时订购。 此支持由Spark SQL以窗口函数的形式提供。 Window函数是标准SQL的一部分，并受许多其他SQL引擎的支持。

窗口功能可更新汇总，并为有序子集中的每行返回一个项目。 最基本的聚合函数是 `SUM()`。 `SUM()` 将您的行取出，并总计给您一个。 如果改为应 `SUM()` 用到窗口，将其转换为窗口函数，则每行将收到累积总和。

大多数Spark SQL帮助程序都是窗口函数，可更新窗口中每一行，并添加该行的状态。

### 规范

语法：`OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| [分区] | 基于列或可用字段的行的子组。 示例, `PARTITION BY endUserIds._experience.mcid.id` |
| [order] | 用于对子集或行排序的列或可用字段。 示例, `ORDER BY timestamp` |
| [帧] | 分区中行的子组。 示例, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 会话化

当您处理源自网站、移动应用程序、交互式语音响应系统或任何其他客户交互渠道的ExperienceEvent数据时，如果可以围绕相关的活动期对事件进行分组，则会有所帮助。 通常，您有一个特定意图驱动您的活动，如研究产品、支付账单、检查帐户余额、填写应用程序等。 此分组有助于关联事件，以揭示更多关于客户体验的上下文。

有关Adobe Analytics中会话化的更多信息，请参阅有关上下文感 [知会话的文档](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)。

### 规范

语法：`SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `expirationInSeconds` | 事件结束当前会话和开始新会话之间需要的秒数 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `timestamp_diff` | 当前记录与先前记录之间的时间（以秒为单位） |
| `num` | 窗口函数中定义的键的唯一会话编号，从1 `PARTITION BY` 开始。 |
| `is_new` | 用于标识记录是否是会话中的第一个的布尔值 |
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

```
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

将客户行动与成功关联起来，是了解影响客户体验的因素的重要部分。 以下ADF支持“第一个”和“最后一个”归因，其过期设置不同。

有关Adobe Analytics中归因的更多信息，请参阅《分析 [指南》中的“归因](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html) IQ”概述。

### 首次联系归因

返回目标ExperienceEvent数据集中单个渠道的首次触摸归因值和详细信息。 查询返回一个对 `struct` 象，该对象具有为所选渠道返回的每行的首次触摸值、时间戳和属性。

如果您想了解哪些交互导致了一系列客户操作，此查询非常有用。 在以下示例中，ExperienceEvent数据中的初始跟踪代码(`em:946426`)被归为客户操作的100%(`1.0`)责任，因为它是第一次交互。

### 规范

语法：`ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 要用作返回对象中标签的易记名称 |
| `channelValue` | 作为目标渠道的列或字段 |


| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | ExperienceEvent中 `channelValue` 首次触及的值 |
| `timestamp` | 发生首次触摸的ExperienceEvent的时间戳 |
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

```
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

返回目标ExperienceEvent数据集中单个渠道的上次触摸归因值和详细信息。 查询返回一个对 `struct` 象，该对象具有为所选渠道返回的每行的上次触摸值、时间戳和属性。

如果您希望查看一系列客户操作中的最终交互，此查询非常有用。 在以下示例中，返回对象中的跟踪代码是每个ExperienceEvent记录中的上次交互。 每个代码都归因于客户操作的100%(`1.0`)责任，因为这是最后一次交互。

### 规范

语法：`ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 要用作返回对象中标签的易记名称 |
| `channelValue` | 作为目标渠道的列或字段 |


| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | ExperienceEvent中 `channelValue` 的上次触摸值 |
| `timestamp` | 使用ExperienceEvent的时 `channelValue` 间戳 |
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

```
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

### 具有到期条件的首次联系归因

返回目标ExperienceEvent数据集中单个渠道的首次触摸归因值和详细信息，该属性值在条件之后或之前过期。 查询返回一个对 `struct` 象，该对象具有为所选渠道返回的每行的首次触摸值、时间戳和属性。

如果您想要查看哪些交互导致了ExperienceEvent数据集的一部分中的一系列客户操作（由您选择的条件决定），此查询非常有用。 在以下示例中，将(`commerce.purchases.value IS NOT NULL`)在结果（7月15日、21日、23日和29日）中显示的四天中的每天记录购买，并且每天的初始跟踪代码将对客户操作承担100%(`1.0`)责任。

#### 规范

语法：`ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 要用作返回对象中标签的易记名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expCondition` | 确定渠道到期点的条件 |
| `expBefore` | 默认为 `false`。用于指示渠道在满足指定条件之前还是之后过期的布尔值。 主要针对会话到期条件(例如 `sess.depth = 1, true`)启用，以确保不从上一会话中选择第一次触摸。 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 该值是 `channelValue` ExperienceEvent中在 `expCondition` |
| `timestamp` | 发生首次触摸的ExperienceEvent的时间戳 |
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

```
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

### 具有过期超时的首次联系归因

返回指定时间段内目标ExperienceEvent数据集中单个渠道的首次触摸归因值和详细信息。 查询返回一个对 `struct` 象，该对象具有为所选渠道返回的每行的首次触摸值、时间戳和属性。 如果您希望查看在选定的时间间隔内导致客户操作的交互情况，此查询非常有用。 在以下示例中，每次客户操作返回的第一次接触是前七天(`expTimeout = 86400 * 7`)内最早的交互。

#### 规范

语法：`ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 要用作返回对象中标签的易记名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expTimeout` | 渠道事件前的时间窗口（以秒为单位）,查询搜索第一次触摸事件 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 在指定 `channelValue` 间隔内首次触摸的值 `expTimeout` 。 |
| `timestamp` | 发生首次触摸的ExperienceEvent的时间戳 |
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

```
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

返回目标ExperienceEvent数据集中单个渠道的上次触摸归因值和详细信息，该属性值在条件之后或之前过期。 查询返回一个对 `struct` 象，该对象具有为所选渠道返回的每行的上次触摸值、时间戳和属性。 如果您希望查看ExperienceEvent数据集的一部分中由您选择的条件确定的一系列客户操作中的最后一次交互，则此查询很有用。 在以下示例中，将(`commerce.purchases.value IS NOT NULL`)在结果（7月15日、21日、23日和29日）中显示的四天中的每天记录购买，并且每天的最后跟踪代码将客户操作的100%(`1.0`)责任归于其中。

#### 规范

语法：`ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 要用作返回对象中标签的易记名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expCondition` | 确定渠道到期点的条件 |
| `expBefore` | 默认为 `false`。用于指示渠道在满足指定条件之前还是之后过期的布尔值。 主要针对会话到期条件(例如 `sess.depth = 1, true`)启用，以确保不从上一会话中选择上次触摸。 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 该值是 `channelValue` ExperienceEvent中在 `expCondition` |
| `timestamp` | 发生上次触摸的ExperienceEvent的时间戳 |
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

```
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

返回指定时间段内目标ExperienceEvent数据集中单个渠道的上次触摸归因值和详细信息。 查询返回一个对 `struct` 象，该对象具有为所选渠道返回的每行的上次触摸值、时间戳和属性。 如果您希望查看所选时间间隔内的上次交互，此查询很有用。 在以下示例中，每次客户操作的上次触碰返回是后七天(`expTimeout = 86400 * 7`)内的最终交互。

#### 规范

语法：`ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在数据集中找到时间戳字段 |
| `channelName` | 要用作返回对象中标签的易记名称 |
| `channelValue` | 作为目标渠道的列或字段 |
| `expTimeout` | 渠道事件之后的时间窗口（以秒为单位）,查询会搜索最后一次触摸事件 |

| 返回的对象参数 | 描述 |
| ---------------------- | ------------- |
| `name` | 在 `channelName` ADF中输入为标签 |
| `value` | 在指定的 `channelValue` 间隔内的上次触摸的值 `expTimeout` 。 |
| `timestamp` | 发生上次触摸的ExperienceEvent的时间戳 |
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

```
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

了解客户如何在体验中导航非常重要。 它可用于了解客户的深度参与度、确认体验的预期步骤是否按设计运行并确定影响客户的潜在痛点。 以下ADF支持根据其“上一个”和“下一个”关系建立路径视图。 您将能够创建上一页和下一页，或者遍历多个事件以创建路径。

### 上一次触摸

确定特定字段的上一个值，该值在窗口内定义的步骤数。 在示例中，请注意， `WINDOW` “函数”配置了一个框架，该框架将ADF设 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 置为查看当前行以及前面的所有行。

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

```
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

### 下一次触控

确定特定字段的下一个值，该值在窗口内定义的步骤数。 在示例中，请注意， `WINDOW` “函数”配置了一个框架，该框架将ADF设置为查看当 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 前行以及它之后的所有行。

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

```
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

中间时间允许您探索事件发生前后的某个时间段内的潜在客户行为。 查看所有客户在活动或其他类型事件后7天内的事件情况。

### 上次匹配的间隔时间

提供新的维度，该维度测量自特定事件以来经过的时间。

#### 规范

语法：`TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在所有事件上填充的数据集中找到时间戳字段。 |
| `eventDefintion` | 表达式以符合上一事件。 |
| `timeUnit` | 输出单位：天、小时、分钟和秒。 默认为秒。 |

输出：返回一个数字，表示自查看上一个匹配事件以来的时间单位；如果找不到匹配事件，则返回数字保留为空。

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

```
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

### 下次匹配时间间隔

提供新的维度，它测量特定事件发生前的时间。

#### 规范

语法：`TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 参数 | 描述 |
| --- | --- |
| `timestamp` | 在所有事件上填充的数据集中找到时间戳字段。 |
| `eventDefintion` | 表达式以符合下一个事件。 |
| `timeUnit` | 输出单位：天、小时、分钟和秒。 默认为秒。 |

输出：返回一个负数，表示下一个匹配事件后的时间单位；如果找不到匹配事件，则返回null。

#### 示例查询

```
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

```
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

使用此处描述的函数，您可以编写查询来使用查询服务访问您自己的ExperienceEvent数据集。 有关在查询服务中创作查询的更多信息，请参阅有关创建查询 [的文档](../creating-queries/creating-queries.md)。
