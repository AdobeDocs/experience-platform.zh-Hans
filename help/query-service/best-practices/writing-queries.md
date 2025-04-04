---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；编写查询；编写查询；
solution: Experience Platform
title: 有关查询服务中查询执行的一般指导
type: Tutorial
description: 本文档概述了在Adobe Experience Platform查询服务中编写查询时要了解的重要详细信息。
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 2%

---

# 在[!DNL Query Service]中执行查询的一般指导

本文档详细介绍了在Adobe Experience Platform [!DNL Query Service]中编写查询时要了解的重要详细信息。

有关[!DNL Query Service]中使用的SQL语法的详细信息，请阅读[SQL语法文档](../sql/syntax.md)。

## 查询执行模型

Adobe Experience Platform [!DNL Query Service]有两种查询执行模型：交互式和非交互式。 交互执行用于商务智能工具中的查询开发和报告生成，而非交互执行用于大型作业和作为数据处理工作流一部分的操作查询。

### 交互式查询执行

可以通过通过[!DNL Query Service] UI提交查询或通过连接的客户端](../clients/overview.md)提交[以交互方式执行查询。 通过连接的客户端运行[!DNL Query Service]时，在客户端与[!DNL Query Service]之间运行活动会话，直到提交的查询返回或超时。

交互式查询执行具有以下限制：

| 参数 | 限制 |
| --------- | ---------- |
| 查询超时 | 10 分钟 |
| 返回的最大行数 | 50,000 |
| 最大并发查询数 | 5 |

>[!NOTE]
>
>要覆盖最大行数限制，请在查询中包含`LIMIT 0`。 10分钟的查询超时仍然适用。

默认情况下，交互式查询的结果会返回到客户端，并且&#x200B;**不会**&#x200B;保留。 要将结果作为[!DNL Experience Platform]中的数据集保留，查询必须使用`CREATE TABLE AS SELECT`语法。

### 非交互式查询执行

通过[!DNL Query Service] API提交的查询以非交互方式运行。 非交互执行意味着[!DNL Query Service]接收API调用并按接收顺序执行查询。 非交互式查询始终会在[!DNL Experience Platform]中生成新数据集以接收结果，或在现有数据集中插入新行。

## 访问对象中的特定字段

要访问查询中对象内的字段，可以使用点表示法(`.`)或方括号表示法(`[]`)。 以下SQL语句使用点表示法将`endUserIds`对象向下遍历到`mcid`对象。

>[!NOTE]
>
>Experience Cloud ID (ECID)也称为MCID，将继续在命名空间中使用。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名称。 |

以下SQL语句使用括号表示法将`endUserIds`对象向下遍历到`mcid`对象。

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名称。 |

>[!NOTE]
>
>由于每种表示法类型返回的结果相同，因此您选择使用的表示法取决于您的偏好。

上述两个示例查询都返回一个拼合对象，而不是一个值：

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

返回的`endUserIds._experience.mcid`对象包含以下参数的相应值：

- `id`
- `namespace`
- `primary`

如果仅将该列声明为向下至该对象，则会将整个对象作为字符串返回。 要仅查看ID，请使用：

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 引号

单引号、双引号和后引号在Query Service查询中具有不同的用法。

### 单引号

单引号(`'`)用于创建文本字符串。 例如，它可以在`SELECT`语句中用于返回结果中的静态文本值，在`WHERE`子句中用于计算列的内容。

以下查询为列声明了一个静态文本值(`'datasetA'`)：

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

以下查询在其WHERE子句中使用单引号字符串(`'homepage'`)来返回特定页的事件。

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### 双引号

双引号(`"`)用于声明带有空格的标识符。

当一列的标识符中包含空格时，以下查询使用双引号返回指定列的值：

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>双引号&#x200B;**不能与点表示法字段访问一起使用**。

### 后引号

使用点表示法时，后引号`` ` ``仅用于转义保留列名&#x200B;**的**。 例如，由于`order`是SQL中的保留字，因此您必须使用后引号来访问字段`commerce.order`：

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

后引号也用于访问以数字开头的字段。 例如，要访问字段`30_day_value`，您需要使用后引号表示法。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

如果使用方括号表示法，则后引号&#x200B;**不需要**。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 查看表信息

连接到查询服务后，您可以使用`\d`或`SHOW TABLES`命令在Experience Platform上查看所有可用的表。

### 标准表格视图

`\d`命令显示用于列出表的标准[!DNL PostgreSQL]视图。 此命令的输出示例如下所示：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 详细的表视图

`SHOW TABLES`命令是一个自定义命令，它提供有关表的更多详细信息。 此命令的输出示例如下所示：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 架构信息

要查看表中架构的更多详细信息，您可以使用`\d {TABLE_NAME}`命令，其中`{TABLE_NAME}`是要查看其架构信息的表的名称。

以下示例显示了`luma_midvalues`表的架构信息，使用`\d luma_midvalues`可以看到该信息：

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

此外，您还可以通过将列的名称附加到表名来获取有关特定列的详细信息。 这将以`\d {TABLE_NAME}_{COLUMN}`格式编写。

以下示例显示了`web`列的附加信息，将使用以下命令调用： `\d luma_midvalues_web`：

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 连接数据集

您可以将多个数据集连接在一起，以在查询中包含来自其他数据集的数据。

以下示例将连接以下两个数据集（`your_analytics_table`和`custom_operating_system_lookup`），并按页面查看次数为前50个操作系统创建一个`SELECT`语句。

**查询**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**结果**

| 操作系统 | 页面查看次数 |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003和XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## 重复数据删除

查询服务支持重复数据删除，或从数据中删除重复行。 有关重复数据删除的详细信息，请参阅[查询服务重复数据删除指南](../key-concepts/deduplication.md)。

## 查询服务中的时区计算

查询服务使用UTC时间戳格式标准化Adobe Experience Platform中的持久数据。 有关如何将时区要求转换成UTC时间戳和从UTC时间戳转换成的更多信息，请参阅[常见问题解答部分，了解如何将时区更改为UTC时间戳，以及从UTC时间戳更改时区](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?)。

## 后续步骤

通过阅读本文档，您已了解使用[!DNL Query Service]编写查询时的一些重要注意事项。 有关如何使用SQL语法编写自己的查询的详细信息，请阅读[SQL语法文档](../sql/syntax.md)。

有关可在查询服务中使用的更多查询示例，请阅读以下用例文档：

- [Analytics分析](../use-cases/analytics-insights.md)
- [创建事件的趋势报表](../use-cases/trended-report-of-events.md)
- [查看访客的汇总报表](../use-cases/roll-up-report-of-a-visitor.md)
- [列出用户的页面查看次数](../use-cases/list-visitor-sessions.md)
- [按访客页面查看次数列出访客](../use-cases/visitors-by-number-of-page-views.md)
