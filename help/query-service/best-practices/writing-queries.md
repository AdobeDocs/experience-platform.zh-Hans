---
keywords: Experience Platform;home;popular topics;query service;Query service;writing queries;writing query;
solution: Experience Platform
title: 编写查询
topic: queries
type: Tutorial
description: 本文档详细介绍了在Adobe Experience Platform查询服务中编写查询时应了解的重要细节。
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 4%

---


# [!DNL Query Service]中查询执行的一般指南

此文档详细介绍了在Adobe Experience Platform[!DNL Query Service]编写查询时应了解的重要细节。

有关[!DNL Query Service]中使用的SQL语法的详细信息，请阅读[ SQL语法文档](../sql/syntax.md)。

## 查询执行模型

Adobe Experience Platform[!DNL Query Service]有两种查询执行模式：交互和非交互。 交互式执行用于商业智能工具中的查询开发和报告生成，而非交互式用于作为数据处理工作流的一部分的较大作业和操作查询。

### 交互式查询执行

通过[!DNL Query Service] UI或[通过连接的客户端](../clients/overview.md)提交查询，可以交互地执行这些操作。 当通过连接的客户端运行[!DNL Query Service]时，在客户端和[!DNL Query Service]之间运行活动会话，直到提交的查询返回或超时。

交互式查询执行有以下限制：

| 参数 | 限制 |
| --------- | ---------- |
| 查询超时 | 10 分钟 |
| 返回的最大行数 | 五万 |
| 最大并发查询 | 5 |

>[!NOTE]
>
>要覆盖最大行限制，请在您的查询中包含`LIMIT 0`。 查询超时仍适用10分钟。

默认情况下，交互式查询的结果将返回到客户端，并且&#x200B;**不会**&#x200B;被保留。 要将结果作为数据集保留在[!DNL Experience Platform]中，查询必须使用`CREATE TABLE AS SELECT`语法。

### 非交互式查询执行

通过[!DNL Query Service] API提交的查询将以非交互方式运行。 非交互式执行意味着[!DNL Query Service]接收API调用，并按接收顺序执行查询。 非交互式查询通常导致在[!DNL Experience Platform]中生成新数据集以接收结果，或将新行插入现有数据集。

## 访问对象中的特定字段

要访问查询中对象中的字段，可以使用点记号(`.`)或括号记号(`[]`)。 以下SQL语句使用点记号将`endUserIds`对象向下遍历到`mcid`对象。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名称。 |

以下SQL语句使用括号记号将`endUserIds`对象向下遍历到`mcid`对象。

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名称。 |

>[!NOTE]
>
>由于每个记号类型返回的结果相同，因此您选择使用的结果取决于您的偏好。

以上两个示例查询都返回一个拼合对象，而不是单个值：

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

当该列仅向对象声明时，它将整个对象返回为字符串。 要仅视图ID，请使用：

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 报价

单引号、多次引号和后引号在查询服务查询中有不同的用法。

### 单引号

单引号(`'`)用于创建文本字符串。 例如，它可用在`SELECT`语句中以返回结果中的静态文本值，在`WHERE`子句中以计算列的内容。

以下查询为列声明静态文本值(`'datasetA'`):

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

以下查询在其WHERE子句中使用单引号字符串(`'homepage'`)返回特定页面的事件。

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### 多次报价

多次引号(`"`)用于声明带空格的标识符。

当某列的标识符中包含空格时，以下查询使用多次引号从指定列返回值：

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
>多次引号&#x200B;**不能**&#x200B;与点记号字段访问一起使用。

### 后引号

使用点记号语法时，后引号`` ` ``用于转义保留列名称&#x200B;**仅**。 例如，由于`order`是SQL中的保留字，因此必须使用后引号访问字段`commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

返回引号还用于访问具有数字开始的字段。 例如，要访问字段`30_day_value`，您需要使用返回引号记号。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

如果使用括号——记号法，则后引号是&#x200B;**不**。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## 查看表信息

连接到查询服务后，您可以使用`\d`或`SHOW TABLES`命令查看平台上的所有可用表。

### 标准表视图

`\d`命令显示列表表的标准PostgreSQL视图。 此命令的输出示例如下所示：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 详细表视图

`SHOW TABLES` 命令是提供有关表的更多详细信息的自定义命令。此命令的输出示例如下所示：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 模式信息

要视图表中模式的更多详细信息，可以使用`\d {TABLE_NAME}`命令，其中`{TABLE_NAME}`是要视图其模式信息的表的名称。

以下示例显示`luma_midvalues`表的模式信息，该信息将通过使用`\d luma_midvalues`来查看：

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

此外，还可以通过将列名称附加到表名称来获取有关特定列的更多信息。 将以`\d {TABLE_NAME}_{COLUMN}`格式写入。

以下示例显示了`web`列的其他信息，并将通过以下命令调用：`\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 加入数据集

您可以将多个数据集连接在一起，以便将来自查询中其他数据集的数据包含在一起。

以下示例将连接以下两个数据集（`your_analytics_table`和`custom_operating_system_lookup`），并按页面视图数为前50个操作系统创建`SELECT`语句。

**查询**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**结果**

| 操作系统 | 页面视图 |
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
| Windows Server 2003 和 XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## 重复数据删除

查询服务支持外部重复数据删除或从数据中删除重复行。 有关外部重复数据删除的详细信息，请阅读[查询服务外部重复数据删除指南](./deduplication.md)。

## 后续步骤

通过阅读此文档，您在使用[!DNL Query Service]编写查询时已经注意到一些重要注意事项。 有关如何使用SQL语法编写您自己的查询的详细信息，请阅读[SQL语法文档](../sql/syntax.md)。

有关可在查询服务中使用的查询的更多示例，请阅读[Adobe Analytics示例查询](./adobe-analytics.md)、[Adobe Target示例查询](./adobe-target.md)或[ExperienceEvent示例查询](./experience-event-queries.md)上的指南。