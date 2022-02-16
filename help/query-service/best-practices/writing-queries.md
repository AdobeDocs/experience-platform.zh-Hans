---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；编写查询；编写查询；
solution: Experience Platform
title: 查询服务中查询执行的一般指导
topic-legacy: queries
type: Tutorial
description: 本文档详细介绍了在Adobe Experience Platform查询服务中编写查询时要了解的重要详细信息。
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: c36ef1d5f5e5f7875da2b7a878c86b449d46c3c5
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 3%

---

# 在中执行查询的一般指导 [!DNL Query Service]

本文档详细介绍了在Adobe Experience Platform中编写查询时要了解的重要详细信息 [!DNL Query Service].

有关中使用的SQL语法的详细信息 [!DNL Query Service]，请阅读 [SQL语法文档](../sql/syntax.md).

## 查询执行模型

Adobe Experience Platform [!DNL Query Service] 具有两种查询执行模型：交互式和非交互式。 交互式执行用于商业智能工具中的查询开发和报告生成，而非交互式执行用于作为数据处理工作流的一部分的较大作业和操作查询。

### 交互式查询执行

通过 [!DNL Query Service] UI或 [通过连接的客户端](../clients/overview.md). 运行时 [!DNL Query Service] 通过连接的客户端，活动会话在客户端和 [!DNL Query Service] 直到提交的查询返回或超时。

交互式查询执行具有以下限制：

| 参数 | 限制 |
| --------- | ---------- |
| 查询超时 | 10 分钟 |
| 返回的最大行数 | 50,000 |
| 最大并发查询数 | 5 |

>[!NOTE]
>
>要覆盖最大行数限制，请包括 `LIMIT 0` 中。 10分钟的查询超时仍适用。

默认情况下，交互式查询的结果将返回给客户端，并且 **not** 保留。 要将结果作为数据集保留在 [!DNL Experience Platform]，则查询必须使用 `CREATE TABLE AS SELECT` 语法。

### 非交互式查询执行

通过 [!DNL Query Service] API以非交互方式运行。 非交互式执行表示 [!DNL Query Service] 接收API调用，并按收到查询的顺序执行查询。 非交互式查询始终会导致在 [!DNL Experience Platform] 接收结果，或将新行插入现有数据集。

## 访问对象中的特定字段

要访问查询中对象中的字段，可以使用点表示法(`.`)或括号(`[]`)。 以下SQL语句使用点表示法遍历 `endUserIds` 对象 `mcid` 对象。

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

以下SQL语句使用括号表示法遍历 `endUserIds` 对象 `mcid` 对象。

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
>由于每个记数类型返回相同的结果，因此您选择使用的结果取决于您的偏好。

上述两个示例查询都返回一个扁平对象，而不是单个值：

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

返回的 `endUserIds._experience.mcid` 对象包含以下参数的相应值：

- `id`
- `namespace`
- `primary`

当列仅向下声明到对象时，它将以字符串形式返回整个对象。 要仅查看ID，请使用：

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

## 报价

单引号、双引号和后引号在查询服务查询中具有不同的用法。

### 单引号

单引号(`'`)来创建文本字符串。 例如，它可用于 `SELECT` 语句返回结果中的静态文本值，以及 `WHERE` 用于评估列内容的子句。

以下查询声明一个静态文本值(`'datasetA'`):

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

以下查询使用单引号字符串(`'homepage'`)来返回特定页面的事件。

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

当某列的标识符中包含空格时，以下查询会使用双引号从指定的列返回值：

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
>双引号 **无法** 用于点表示法字段访问。

### 反引号

后引号 `` ` `` 用于转义保留的列名称 **仅** 使用点符号语法时。 例如，自 `order` 是SQL中的保留字，必须使用反引号来访问该字段 `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

还使用前引号访问以数字开头的字段。 例如，访问字段 `30_day_value`，则需要使用反引号符号。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

后引号为 **not** 使用括号符号时需要此参数。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 查看表信息

连接到查询服务后，您可以使用 `\d` 或 `SHOW TABLES` 中。

### 标准表视图

的 `\d` 命令显示用于列表的标准PostgreSQL视图。 此命令的输出示例如下所示：

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 详细的表视图

`SHOW TABLES` 命令是一个自定义命令，可提供有关表的更多详细信息。 此命令的输出示例如下所示：

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 架构信息

要查看表中有关架构的更多详细信息，您可以使用 `\d {TABLE_NAME}` 命令，其中 `{TABLE_NAME}` 是要查看其架构信息的表的名称。

以下示例显示了 `luma_midvalues` 表格，使用 `\d luma_midvalues`:

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

此外，您还可以通过将列的名称附加到表名称后，来获取有关特定列的更多信息。 将以格式写入 `\d {TABLE_NAME}_{COLUMN}`.

以下示例显示了 `web` 列中，并将使用以下命令调用： `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 连接数据集

您可以将多个数据集合在一起，以将来自其他数据集的数据包含到查询中。

以下示例将连接以下两个数据集(`your_analytics_table` 和 `custom_operating_system_lookup`)并创建 `SELECT` 按页面查看次数列出的前50个操作系统的语句。

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
| Windows Server 2003 和 XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 9221.0 |

## 重复数据删除

查询服务支持重复数据删除或从数据中删除重复行。 有关重复数据删除的详细信息，请阅读 [查询服务重复数据删除指南](./deduplication.md).

## 查询服务中的时区计算

查询服务使用UTC时间戳格式对Adobe Experience Platform中持久数据进行标准化。 有关如何将时区要求转换为UTC时间戳和从UTC时间戳转换时区要求的详细信息，请参阅 [有关如何将时区更改为UTC时间戳和从UTC时间戳更改为常见问题解答部分](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## 后续步骤

通过阅读本文档，您在使用 [!DNL Query Service]. 有关如何使用SQL语法编写您自己的查询的详细信息，请阅读 [SQL语法文档](../sql/syntax.md).

有关查询服务中可使用的查询示例，请阅读 [Adobe Analytics示例查询](./adobe-analytics.md), [Adobe Target示例查询](./adobe-target.md)或 [ExperienceEvent示例查询](./experience-event-queries.md).
