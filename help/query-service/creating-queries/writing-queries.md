---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 编写查询
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 1%

---


# 查询服务中执行查询的一般指南

本文档详细介绍了在Adobe Experience Platform查询服务中编写查询时应了解的重要信息。

有关查询服务中使用的SQL语法的详细信息，请阅读 [SQL语法文档](../sql/syntax.md)。

## 查询执行模型

Adobe Experience Platform查询服务有两种查询执行模式： 交互和非交互。 交互式执行用于商业智能工具中的查询开发和报告生成，而非交互式用于作为数据处理工作流的一部分的较大作业和操作查询。

### 交互式查询执行

查询可以通过查询服务UI或连接的客户端提交，从 [而以交互方式执行](../clients/overview.md)。 当通过连接的客户端运行查询服务时，在客户端和查询服务之间运行一个活动会话，直到提交的查询返回或超时。

交互式查询执行有以下限制：

| 参数 | 限制 |
| --------- | ---------- |
| 查询超时 | 10 分钟 |
| 返回的最大行数 | 50,000 |
| 最大并发查询 | 5 |

>[!NOTE]
>
>要覆盖最大行限制，请在 `LIMIT 0` 查询中包含。 查询超时仍适用10分钟。

默认情况下，交互式查询的结果将返回给客户端并且不 **会** 保留。 要将结果作为Experience Platform数据集保留，查询必须使用语 `CREATE TABLE AS SELECT` 法。

### 非交互式查询执行

通过查询服务API提交的查询将以非交互方式运行。 非交互式执行是指查询服务接收API调用并按其接收顺序执行查询。 非交互式查询通常导致在Experience Platform中生成新数据集以接收结果，或将新行插入现有数据集。

## 访问对象中的特定字段

要访问查询中对象中的字段，可以使用点记号()`.`或括号记号(`[]`)。 以下SQL语句使用点记号将对 `endUserIds` 象向下遍历对 `mcid` 象。

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 属性 | 描述 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 分析表的名称。 |

以下SQL语句使用括号记号将对 `endUserIds` 象向下遍历对 `mcid` 象。

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

返回的 `endUserIds._experience.mcid` 对象包含以下参数的相应值：

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

## 何时使用单引号、多次引号和后引号

本节介绍何时在查询中使用单引号、多次引号和后引号。

### 单引号

单引号(`'`)用于创建文本字符串。 例如，它可用在语句 `SELECT` 中返回结果中的静态文本值，在子句 `WHERE` 中用于计算列的内容。

以下查询为列声明静态`'datasetA'`文本值():

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

以下查询在其WHERE子句中使用单引`'homepage'`号字符串()返回特定页面的事件。

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
>多次引 **号不能** 与点记号字段访问一起使用。

### 后引号

后引号仅 `` ` `` 在使用点记号语法 **时用** 于转义保留列名。 例如，由于 `order` SQL中是保留字，因此必须使用后引号访问该字段 `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

返回引号还用于访问具有数字开始的字段。 例如，要访问该字 `30_day_value`段，您需要使用返回引号记号。

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

如果使用括 **号** ，则不需要后引号。

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## 后续步骤

阅读本文档，您在使用查询服务编写查询时已经受到一些重要考虑。 有关如何使用SQL语法编写您自己的查询的详细信息，请阅读SQL [语法文档](../sql/syntax.md)。