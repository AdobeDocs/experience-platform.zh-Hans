---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；Adobe定义的函数；SQL;
solution: Experience Platform
title: Adobe定义的查询服务中的SQL函数
topic-legacy: functions
description: 本文档提供了有关Adobe Experience Platform查询服务中可用的Adobe定义函数的信息。
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 63b6236a7e3689afb2ebaa763349b3102697424e
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 2%

---

# Adobe定义的查询服务中的SQL函数

Adobe定义的函数（在此称为ADF）是Adobe Experience Platform查询服务中的预建函数，可帮助在上执行与业务相关的常见任务 [!DNL Experience Event] 数据。 这些函数包括 [会话化](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) 和 [归因](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html) 就象在Adobe Analytics发现的。

本文档提供了Adobe定义的函数在 [!DNL Query Service].

## 窗口函数 {#window-functions}

大多数业务逻辑要求收集客户的接触点并按时订购。 此支持由 [!DNL Spark] 窗口函数形式的SQL。 窗口函数是标准SQL的一部分，受许多其他SQL引擎支持。

窗口函数会更新聚合，并为排序子集中的每一行返回一个项目。 最基本的聚合函数是 `SUM()`. `SUM()` 将您的行取出，并给出总计。 如果您改为 `SUM()` 将窗口转换为窗口函数后，您将收到每行的累计总和。

大多数 [!DNL Spark] SQL帮助程序是窗口函数，用于更新窗口中的每一行，并添加该行的状态。

**查询语法**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 基于列或可用字段的行子组。 | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 用于对子集或行进行排序的列或可用字段。 | `ORDER BY timestamp` |
| `{FRAME}` | 分区中行的子组。 | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 会话化

当您使用 [!DNL Experience Event] 来自网站、移动应用程序、交互式语音应答系统或任何其他客户交互渠道的数据，如果可以围绕相关活动时段对事件进行分组，则会很有帮助。 通常，您具有特定意图来驱动您的活动，例如研究产品、支付账单、检查帐户余额、填写应用程序等。

此数据分组或会话化有助于关联事件，以发现有关客户体验的更多上下文。

有关Adobe Analytics中会话化的更多信息，请参阅 [上下文感知会话](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html).

**查询语法**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{EXPIRATION_IN_SECONDS}` | 确定当前会话结束和新会话开始之间的事件所需的秒数。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `session` 列。 的 `session` 列由以下组件组成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 当前记录与先前记录之间的时间差（以秒为单位）。 |
| `{NUM}` | 唯一会话编号，从1开始，用于 `PARTITION BY` 的子菜单。 |
| `{IS_NEW}` | 一个布尔值，用于标识记录是否是会话的第一个记录。 |
| `{DEPTH}` | 会话中当前记录的深度。 |

### SESS_START_IF

此查询根据当前时间戳和给定的表达式返回当前行的会话状态，并与当前行启动新会话。

**查询语法**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{TEST_EXPRESSION}` | 要检查其数据字段的表达式。 例如：`application.launches > 0`。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `session` 列。 的 `session` 列由以下组件组成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 当前记录与先前记录之间的时间差（以秒为单位）。 |
| `{NUM}` | 唯一会话编号，从1开始，用于 `PARTITION BY` 的子菜单。 |
| `{IS_NEW}` | 一个布尔值，用于标识记录是否是会话的第一个记录。 |
| `{DEPTH}` | 会话中当前记录的深度。 |

### SESS_END_IF

此查询根据当前时间戳和给定的表达式返回当前行的会话状态，结束当前会话，并在下一行启动新会话。

**查询语法**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{TEST_EXPRESSION}` | 要检查其数据字段的表达式。 例如：`application.launches > 0`。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `session` 列。 的 `session` 列由以下组件组成：

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 参数 | 描述 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 当前记录与先前记录之间的时间差（以秒为单位）。 |
| `{NUM}` | 唯一会话编号，从1开始，用于 `PARTITION BY` 的子菜单。 |
| `{IS_NEW}` | 一个布尔值，用于标识记录是否是会话的第一个记录。 |
| `{DEPTH}` | 会话中当前记录的深度。 |

## 归因

将客户操作与成功关联是了解影响客户体验的因素的重要部分。 以下ADF支持具有不同过期设置的首次联系归因和最近联系归因。

有关Adobe Analytics中归因的更多信息，请参阅 [Attribution IQ概述](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=zh-Hans) 在 [!DNL Analytics] 归因面板指南。

### 首次联系归因

此查询返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 数据集。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的首次联系值、时间戳和归因。

如果您想要了解哪些交互导致了一系列客户操作，此查询非常有用。 在以下示例中，初始跟踪代码(`em:946426`) [!DNL Experience Event] 数据被归因为100%(`1.0`)对客户操作负责，因为它是首次交互。

**查询语法**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |

对 `OVER()` 可在 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `first_touch` 列。 的 `first_touch` 列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在ADF中作为标签输入。 |
| `{VALUE}` | 值来自 `{CHANNEL_VALUE}` 这是 [!DNL Experience Event] |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 首次接触的地方。 |
| `{FRACTION}` | 首次接触的归因，以小数部分表示。 |

### 最近联系归因

此查询返回目标中单个渠道的最近联系归因值和详细信息 [!DNL Experience Event] 数据集。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的最近联系值、时间戳和归因。

如果您想要查看一系列客户操作中的最终交互，则此查询非常有用。 在以下示例中，返回对象中的跟踪代码是每个对象中的最后一次交互 [!DNL Experience Event] 记录。 每个代码的归因为100%(`1.0`)对客户操作负责，因为这是最后一次交互。

**查询语法**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在数据集中找到的时间戳字段。 |
| `{CHANNEL_NAME}` | 返回对象的标签。 |
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |

对 `OVER()` 可在 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `last_touch` 列。 的 `last_touch` 列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在ADF中作为标签输入。 |
| `{VALUE}` | 值来自 `{CHANNEL_VALUE}` 这是 [!DNL Experience Event] |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 其中 `channelValue` 已使用。 |
| `{FRACTION}` | 最近联系的归因，以小数部分表示。 |

### 具有过期条件的首次联系归因

此查询返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 数据集，在条件之后或之前过期。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的首次联系值、时间戳和归因。

如果您想要了解哪些交互导致了 [!DNL Experience Event] 由您选择的条件确定的数据集。 在以下示例中，记录了购买(`commerce.purchases.value IS NOT NULL`)，并且每天的初始跟踪代码均被归因为100%(`1.0`)对客户操作负责。

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
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，用于指示渠道在指定条件之前还是之后过期， `{EXP_CONDITION}`，则不会。 这主要针对会话的到期条件启用，以确保未从上一个会话中选择首次联系。 默认情况下，此值设置为 `false`. |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `first_touch` 列。 的 `first_touch` 列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在ADF中作为标签输入。 |
| `{VALUE}` | 值来自 `CHANNEL_VALUE}` 这是 [!DNL Experience Event]，在 `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 首次接触的地方。 |
| `{FRACTION}` | 首次接触的归因，以小数部分表示。 |

### 具有过期超时的首次联系归因

此查询返回目标中单个渠道的首次联系归因值和详细信息 [!DNL Experience Event] 数据集。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的首次联系值、时间戳和归因。

如果您想要查看在选定时间间隔内导致客户操作的交互，则此查询非常有用。 在以下示例中，每个客户操作返回的首次联系是前七天内最早的交互(`expTimeout = 86400 * 7`)。

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
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |
| `{EXP_TIMEOUT}` | 查询搜索首次联系事件之前的渠道事件时间窗口（以秒为单位）。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `first_touch` 列。 的 `first_touch` 列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在ADF中作为标签输入。 |
| `{VALUE}` | 值来自 `CHANNEL_VALUE}` 即指定 `{EXP_TIMEOUT}` 间隔。 |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 首次接触的地方。 |
| `{FRACTION}` | 首次接触的归因，以小数部分表示。 |

### 具有过期条件的最近联系归因

此查询返回目标中单个渠道的最近联系归因值和详细信息 [!DNL Experience Event] 数据集，在条件之后或之前过期。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的最近联系值、时间戳和归因。

如果您想要查看 [!DNL Experience Event] 由您选择的条件确定的数据集。 在以下示例中，记录了购买(`commerce.purchases.value IS NOT NULL`)，并且每天的最后一个跟踪代码都被归因为100%(`1.0`)对客户操作负责。

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
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段。 |
| `{EXP_CONDITION}` | 确定渠道到期点的条件。 |
| `{EXP_BEFORE}` | 一个布尔值，用于指示渠道在指定条件之前还是之后过期， `{EXP_CONDITION}`，则不会。 这主要针对会话的到期条件启用，以确保未从上一个会话中选择首次联系。 默认情况下，此值设置为 `false`. |

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

对于给定的示例查询，将在 `last_touch` 列。 的 `last_touch` 列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在ADF中作为标签输入。 |
| `{VALUE}` | 值来自 `{CHANNEL_VALUE}` 这是 [!DNL Experience Event]，在 `{EXP_CONDITION}`. |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 最后接触的地方。 |
| `{FRACTION}` | 最近联系的归因，以小数部分表示。 |

### 具有过期超时的最近联系归因

此查询返回目标中单个渠道的最近联系归因值和详细信息 [!DNL Experience Event] 数据集。 查询会返回 `struct` 对象，其中包含为选定渠道返回的每行的最近联系值、时间戳和归因。

如果您希望查看选定时间间隔内的最后一次交互，则此查询非常有用。 在以下示例中，针对每个客户操作返回的最近联系是随后七天(`expTimeout = 86400 * 7`)。

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
| `{CHANNEL_VALUE}` | 作为查询目标渠道的列或字段 |
| `{EXP_TIMEOUT}` | 查询在渠道事件后搜索最近联系事件的时间范围（以秒为单位）。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `last_touch` 列。 的 `last_touch` 列由以下组件组成：

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{NAME}` | 的 `{CHANNEL_NAME}`，在ADF中作为标签输入。 |
| `{VALUE}` | 值来自 `{CHANNEL_VALUE}` 即指定 `{EXP_TIMEOUT}` 间隔 |
| `{TIMESTAMP}` | 的时间戳 [!DNL Experience Event] 最近联系发生的地方 |
| `{FRACTION}` | 最近联系的归因，以小数部分表示。 |

## 路径分析

路径分析可用于了解客户的参与深度、确认体验的预期步骤是否按预期工作以及确定影响客户的潜在棘手问题。

以下ADF支持根据其先前和后续关系建立路径视图。 您将能够创建上一页和下一页，或分步处理多个事件以创建路径。

### 上一页

确定特定字段的上一个值，该值在窗口内的一定数量之外。 请注意，在示例中， `WINDOW` 函数配置了 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 设置ADF以查看当前行和所有后续行。

**查询语法**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{KEY}` | 事件中的列或字段。 |
| `{SHIFT}` | （可选）当前事件之外的事件数。 默认情况下，值为1。 |
| `{IGNORE_NULLS}` | （可选）指示是否为null的布尔值 `{KEY}` 值应被忽略。 默认情况下，值为 `false`. |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `previous_page` 列。 中的值 `previous_page` 列基于 `{KEY}` 在ADF中使用。

### 下一页

确定特定字段的下一个值，该值在窗口内定义的步骤数之外。 请注意，在示例中， `WINDOW` 函数配置了 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 设置ADF以查看当前行和所有后续行。

**查询语法**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{KEY}` | 事件中的列或字段。 |
| `{SHIFT}` | （可选）当前事件之外的事件数。 默认情况下，值为1。 |
| `{IGNORE_NULLS}` | （可选）指示是否为null的布尔值 `{KEY}` 值应被忽略。 默认情况下，值为 `false`. |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `previous_page` 列。 中的值 `previous_page` 列基于 `{KEY}` 在ADF中使用。

## 间隔时间

间隔时间允许您探索事件发生之前或之后某个时间段内客户的潜在行为。

### 上次匹配的间隔时间

此查询会返回一个数字，表示自上次出现匹配事件后所经过的时间单位。 如果未找到匹配的事件，则返回null。

**查询语法**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件上填充的数据集中找到的时间戳字段。 |
| `{EVENT_DEFINITION}` | 用于限定上一个事件的表达式。 |
| `{TIME_UNIT}` | 输出单位。 可能的值包括天、小时、分钟和秒。 默认情况下，值为秒。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `average_minutes_since_registration` 列。 中的值 `average_minutes_since_registration` 列是当前事件与先前事件之间的时间差。 以前在 `{TIME_UNIT}`.

### 下次匹配之间的时间

此查询返回一个负数，表示下一个匹配事件后的时间单位。 如果未找到匹配的事件，则返回null。

**查询语法**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TIMESTAMP}` | 在所有事件上填充的数据集中找到的时间戳字段。 |
| `{EVENT_DEFINITION}` | 用于限定下一个事件的表达式。 |
| `{TIME_UNIT}` | （可选）输出单位。 可能的值包括天、小时、分钟和秒。 默认情况下，值为秒。 |

对 `OVER()` 函数 [窗口函数部分](#window-functions).

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

对于给定的示例查询，将在 `average_minutes_until_order_confirmation` 列。 中的值 `average_minutes_until_order_confirmation` 列是当前事件与后续事件之间的时间差。 以前在 `{TIME_UNIT}`.

## 后续步骤

使用此处描述的函数，您可以编写查询以访问您自己的 [!DNL Experience Event] 使用数据集 [!DNL Query Service]. 有关在中创作查询的更多信息 [!DNL Query Service]，请参阅 [创建查询](../best-practices/writing-queries.md).

## 其他资源

以下视频演示如何在Adobe Experience Platform界面和PSQL客户端中运行查询。 此外，视频还使用涉及XDM对象中各个属性的示例、使用Adobe定义的函数以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
