---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;sql;
solution: Experience Platform
title: Adobe定义函数
topic: functions
description: 此文档提供Adobe定义的功能在查询服务中可用的信息。
translation-type: tm+mt
source-git-commit: e15229601d35d1155fc9a8ab9296f8c41811ebf9
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 2%

---


# Adobe定义函数

Adobe定义的函数（在此称为ADF）是Adobe Experience Platform查询服务中的预建函数，可帮助对[!DNL Experience Event]数据执行与业务相关的常见任务。 这些函数包括[会话化](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)和[归因](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)的函数，如Adobe Analytics的函数。

此文档提供[!DNL Query Service]中提供的Adobe定义函数的信息。

## 窗口函数{#window-functions}

大多数业务逻辑要求为客户收集接触点并按时订购。 此支持由[!DNL Spark] SQL以窗口函数的形式提供。 窗口函数是标准SQL的一部分，并受许多其他SQL引擎支持。

窗口函数会更新聚合，并为有序子集中的每行返回单个项目。 最基本的聚合函数为`SUM()`。 `SUM()` 取行，总计给您一次。如果您改为将`SUM()`应用于窗口，将其转换为窗口函数，则每行将收到累积和。

大多数[!DNL Spark] SQL帮助程序是窗口函数，用于更新窗口中的每行，并添加该行的状态。

**查询语法**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 基于列或可用字段的行子组。 | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 用于对子集或行排序的列或可用字段。 | `ORDER BY timestamp` |
| `{FRAME}` | 分区中行的子组。 | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 会话化

当您处理来自网站、移动应用程序、交互语音应答系统或任何其他客户交互渠道的[!DNL Experience Event]数据时，如果事件可以围绕相关的活动期进行分组，则会有所帮助。 通常，您具有驱动活动的特定意图，如研究产品、支付账单、检查帐户余额、填写应用程序等。

这种数据分组或会话化有助于关联事件，从而揭示更多关于客户体验的情境。

有关Adobe Analytics会话化的详细信息，请参阅[上下文感知会话](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)的相关文档。

**查询语法**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{EXPIRATION_IN_SECONDS}` | 确定当前会话结束和新会话开始事件之间所需的秒数。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`session`列中给出。 `session`列由以下组件组成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 当前记录与先前记录之间的时间差（以秒为单位）。 |
| `{NUM}` | 窗口函数`PARTITION BY`中定义的键的唯一会话编号，从1开始。 |
| `{IS_NEW}` | 用于标识记录是否是会话的第一个的布尔值。 |
| `{DEPTH}` | 会话中当前记录的深度。 |

### SESS_开始_IF

此查询根据当前时间戳和给定的表达式返回当前行的会话状态，并将新会话与当前行开始。

**查询语法**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{TEST_EXPRESSION}` | 要检查数据字段的表达式。 例如，`application.launches > 0`。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**结果**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

对于给定的示例查询，结果在`session`列中给出。 `session`列由以下组件组成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 当前记录与先前记录之间的时间差（以秒为单位）。 |
| `{NUM}` | 窗口函数`PARTITION BY`中定义的键的唯一会话编号，从1开始。 |
| `{IS_NEW}` | 用于标识记录是否是会话的第一个的布尔值。 |
| `{DEPTH}` | 会话中当前记录的深度。 |

### SESS_END_IF

此查询根据当前时间戳和给定的表达式返回当前行的会话状态，结束当前会话，并在下一行开始新会话。

**查询语法**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{TEST_EXPRESSION}` | 要检查数据字段的表达式。 例如，`application.launches > 0`。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**结果**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

对于给定的示例查询，结果在`session`列中给出。 `session`列由以下组件组成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 当前记录与先前记录之间的时间差（以秒为单位）。 |
| `{NUM}` | 窗口函数`PARTITION BY`中定义的键的唯一会话编号，从1开始。 |
| `{IS_NEW}` | 用于标识记录是否是会话的第一个的布尔值。 |
| `{DEPTH}` | 会话中当前记录的深度。 |

## 归因

将客户行动与成功关联是了解影响客户体验的因素的重要部分。 以下ADF通过不同的过期设置支持首次点击归因和最后点击归因。

有关Adobe Analytics归因的详细信息，请参阅[!DNL Analytics]归因面板指南中的[Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html)。

### 首次联系归因

此查询返回目标[!DNL Experience Event]数据集中单个渠道的首次触摸归因值和详细信息。 查询返回一个`struct`对象，其中具有为所选渠道返回的每行的首次触摸值、时间戳和属性。

如果您想了解哪些交互导致了一系列客户操作，此查询非常有用。 在以下示例中，将[!DNL Experience Event]数据中的初始跟踪代码(`em:946426`)归为客户操作的100%(`1.0`)责任，因为它是第一个交互。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为目标渠道的列或字段。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`first_touch`列中给出。 `first_touch`列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中输入为标签。 |
| `{VALUE}` | 来自`{CHANNEL_VALUE}`的值，它是[!DNL Experience Event]中的第一次触摸 |
| `{TIMESTAMP}` | 首次触摸发生的[!DNL Experience Event]的时间戳。 |
| `{FRACTION}` | 首次触摸的归因，表示为小数部分。 |

### 最近接触归因

此查询返回目标[!DNL Experience Event]数据集中单个渠道的上次触碰归因值和详细信息。 查询返回一个`struct`对象，该对象具有为所选渠道返回的每行的最后触摸值、时间戳和属性。

如果您希望在一系列客户操作中看到最终交互，此查询非常有用。 在以下示例中，返回对象中的跟踪代码是每个[!DNL Experience Event]记录中的最后一次交互。 每个代码都归于客户操作的100%(`1.0`)责任，因为它是上次交互。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为目标渠道的列或字段。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`last_touch`列中给出。 `last_touch`列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中输入为标签。 |
| `{VALUE}` | 来自`{CHANNEL_VALUE}`的值，它是[!DNL Experience Event]中的最后一次触摸 |
| `{TIMESTAMP}` | 使用`channelValue`的[!DNL Experience Event]时间戳。 |
| `{FRACTION}` | 上次触摸的归因，表示为小数部分。 |

### 具有过期条件的首次联系归因

此查询返回目标[!DNL Experience Event]数据集中单个渠道的首次触摸归因值和详细信息，该属性在条件后或之前过期。 查询返回一个`struct`对象，其中具有为所选渠道返回的每行的首次触摸值、时间戳和属性。

如果您想要查看在[!DNL Experience Event]数据集的某一部分中，哪些交互导致一系列客户操作是由您选择的条件决定的，则此查询很有用。 在以下示例中，将在结果（7月15日、21日、23日和29日）显示的四天中的每天记录(`commerce.purchases.value IS NOT NULL`)采购，并将每天的初始跟踪代码归为对客户操作的100%(`1.0`)责任。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为目标渠道的列或字段。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，指示渠道是否在指定条件`{EXP_CONDITION}`之前或之后过期。 这主要针对会话的到期条件启用，以确保不从上一个会话中选择第一次触摸。 默认情况下，此值设置为`false`。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`first_touch`列中给出。 `first_touch`列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中输入为标签。 |
| `{VALUE}` | 来自`CHANNEL_VALUE}`的值，该值是[!DNL Experience Event]中第一次触摸，位于`{EXP_CONDITION}`之前。 |
| `{TIMESTAMP}` | 首次触摸发生的[!DNL Experience Event]的时间戳。 |
| `{FRACTION}` | 首次触摸的归因，表示为小数部分。 |

### 具有过期超时的首次联系归因

此查询返回指定时间段内目标[!DNL Experience Event]数据集中单个渠道的首次触摸归因值和详细信息。 查询返回一个`struct`对象，其中具有为所选渠道返回的每行的首次触摸值、时间戳和属性。

如果您想要查看在选定时间间隔内导致客户操作的交互情况，此查询很有用。 在以下示例中，每次客户操作返回的第一次触摸是前七天内(`expTimeout = 86400 * 7`)的最早交互。

**规范**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为目标渠道的列或字段。 |
| `{EXP_TIMEOUT}` | 渠道事件之前的时间窗口，以秒为单位，查询搜索第一次触摸事件。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`first_touch`列中给出。 `first_touch`列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中输入为标签。 |
| `{VALUE}` | 在指定的`{EXP_TIMEOUT}`间隔内首次触摸的`CHANNEL_VALUE}`值。 |
| `{TIMESTAMP}` | 首次触摸发生的[!DNL Experience Event]的时间戳。 |
| `{FRACTION}` | 首次触摸的归因，表示为小数部分。 |

### 具有过期条件的最后联系归因

此查询返回目标[!DNL Experience Event]数据集中单个渠道的上次触碰归因值和详细信息，该属性在条件后或之前过期。 查询返回一个`struct`对象，该对象具有为所选渠道返回的每行的最后触摸值、时间戳和属性。

如果您想在[!DNL Experience Event]数据集的某一部分查看一系列客户操作中的最后一次交互（由您选择的条件确定），此查询很有用。 在以下示例中，将在结果（7月15日、21日、23日和29日）显示的四天中的每天记录(`commerce.purchases.value IS NOT NULL`)采购，并将每天的最后跟踪代码归为对客户操作的100%(`1.0`)责任。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为目标渠道的列或字段。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，指示渠道是否在指定条件`{EXP_CONDITION}`之前或之后过期。 这主要针对会话的到期条件启用，以确保不从上一个会话中选择第一次触摸。 默认情况下，此值设置为`false`。 |

**示例查询**

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

**示例结果**

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

对于给定的示例查询，结果在`last_touch`列中给出。 `last_touch`列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`，在ADF中输入为标签。 |
| `{VALUE}` | 来自`{CHANNEL_VALUE}`的值，该值是[!DNL Experience Event]中在`{EXP_CONDITION}`之前的最后一次触摸。 |
| `{TIMESTAMP}` | 上次触摸发生的[!DNL Experience Event]的时间戳。 |
| `{FRACTION}` | 上次触摸的归因，表示为小数部分。 |

### 具有过期超时的最近联系归因

此查询返回指定时间段内目标[!DNL Experience Event]数据集中单个渠道的上次联系归因值和详细信息。 查询返回一个`struct`对象，该对象具有为所选渠道返回的每行的最后触摸值、时间戳和属性。

如果要查看所选时间间隔内的最后一次交互，此查询很有用。 在下面的示例中，每次客户操作返回的最后一次触摸是后七天内(`expTimeout = 86400 * 7`)的最终交互。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签 |
| `{CHANNEL_VALUE}` | 作为目标渠道的列或字段 |
| `{EXP_TIMEOUT}` | 渠道事件后的时间窗口，以秒为单位，查询搜索最后一次触摸事件。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`last_touch`列中给出。 `last_touch`列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | `{CHANNEL_NAME}`在ADF中输入为标签。 |
| `{VALUE}` | 在指定的`{EXP_TIMEOUT}`间隔内，作为最后一次触摸的`{CHANNEL_VALUE}`值 |
| `{TIMESTAMP}` | 上次触摸发生的[!DNL Experience Event]的时间戳 |
| `{FRACTION}` | 上次触摸的归因，表示为小数部分。 |

## 路径分析

寻路功能可用于了解客户的深度参与度、确认体验的预期步骤是否按设计方式运行并确定影响客户的潜在痛点。

以下ADF支持根据先前和下一个关系建立路径视图。 您将能够创建上一页和下一页，或者遍历多个事件以创建路径。

### 上一页

确定特定字段的上一个值以及在窗口内定义的多个步骤。 请注意，在示例中，`WINDOW`函数配置了一帧`ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`设置ADF查看当前行和所有后续行。

**查询语法**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{KEY}` | 事件中的列或字段。 |
| `{SHIFT}` | （可选）离当前事件的事件数。 默认情况下，值为1。 |
| `{IGNORE_NULLS}` | （可选）指示是否应忽略null `{KEY}`值的布尔值。 默认情况下，该值为`false`。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**结果**

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

对于给定的示例查询，结果在`previous_page`列中给出。 `previous_page`列中的值基于ADF中使用的`{KEY}`。

### 下一页

确定特定字段的下一个值，即在窗口内定义数量的步骤。 请注意，在示例中，`WINDOW`函数配置了一帧`ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING`设置ADF查看当前行和所有后续行。

**查询语法**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{KEY}` | 事件中的列或字段。 |
| `{SHIFT}` | （可选）离当前事件的事件数。 默认情况下，值为1。 |
| `{IGNORE_NULLS}` | （可选）指示是否应忽略null `{KEY}`值的布尔值。 默认情况下，该值为`false`。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**结果**

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

对于给定的示例查询，结果在`previous_page`列中给出。 `previous_page`列中的值基于ADF中使用的`{KEY}`。

## 中间时间

中间时间允许您在发生事件之前或之后的某个时间段内探索潜在客户行为。

### 上次匹配的时间间隔

此查询返回一个数字，表示自看到上一个匹配事件以来的时间单位。 如果找不到匹配事件，则返回null。

**查询语法**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件上填充的数据集中找到时间戳字段。 |
| `{EVENT_DEFINITION}` | 表达式，以限定前一个事件。 |
| `{TIME_UNIT}` | 输出单位。 可能的值包括天、小时、分钟和秒。 默认情况下，该值为秒。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`average_minutes_since_registration`列中给出。 `average_minutes_since_registration`列中的值是当前事件与先前数据之间的时间差。 以前在`{TIME_UNIT}`中定义了时间单位。

### 下次匹配的时间间隔

此查询返回一个负数，表示下一个匹配事件后的时间单位。 如果找不到匹配事件，则返回null。

**查询语法**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件上填充的数据集中找到时间戳字段。 |
| `{EVENT_DEFINITION}` | 表达式可确定下一个事件。 |
| `{TIME_UNIT}` | （可选）输出单位。 可能的值包括天、小时、分钟和秒。 默认情况下，该值为秒。 |

在[窗口函数部分](#window-functions)中可以找到对`OVER()`函数中参数的说明。

**示例查询**

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

**结果**

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

对于给定的示例查询，结果在`average_minutes_until_order_confirmation`列中给出。 `average_minutes_until_order_confirmation`列中的值是当前事件和下一个数据之间的时间差。 以前在`{TIME_UNIT}`中定义了时间单位。

## 后续步骤

使用此处描述的函数，您可以编写查询以使用[!DNL Query Service]访问您自己的[!DNL Experience Event]数据集。 有关在[!DNL Query Service]中创作查询的更多信息，请参阅有关创建查询](../best-practices/writing-queries.md)的文档。[

## Journey Orchestration

以下视频演示如何在Adobe Experience Platform接口和PSQL客户端中运行查询。 此外，视频还使用涉及XDM对象中各个属性的示例，使用Adobe定义的函数，以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)