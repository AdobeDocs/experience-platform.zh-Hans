---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；sql语法；sql；ctas；CTAS；创建表作为选择
solution: Experience Platform
title: 查询服务中的SQL语法
description: 本文档显示了Adobe Experience Platform查询服务支持的SQL语法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 2a5dd20d99f996652de5ba84246c78a1f7978693
workflow-type: tm+mt
source-wordcount: '3706'
ht-degree: 2%

---

# 查询服务中的SQL语法

Adobe Experience Platform查询服务能够将标准ANSI SQL用于 `SELECT` 语句和其他有限命令。 本文档介绍了支持的SQL语法 [!DNL Query Service].

## 选择查询 {#select-queries}

以下语法定义 `SELECT` 支持查询 [!DNL Query Service]：

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

位置 `from_item` 可以是以下选项之一：

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

和 `grouping_element` 可以是以下选项之一：

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

和 `with_query` 为：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

以下小节提供了可在查询中使用的附加条款的详细信息，前提是它们遵循上述格式。

### SNAPSHOT子句

此子句可用于基于快照ID增量读取表中的数据。 快照ID是由Long类型数字表示的检查点标记，每次将数据写入快照时，都会将该标记应用于数据湖表。 此 `SNAPSHOT` 子句将其自身附加到它旁边使用的表关系上。

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 示例

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

请注意 `SNAPSHOT` 子句与表或表别名一起使用，但不用在子查询或视图的顶部。 A `SNAPSHOT` 子句适用于任何位置 `SELECT` 可对表应用查询。

此外，您还可以使用 `HEAD` 和 `TAIL` 作为快照子句的特殊偏移值。 使用 `HEAD` 是指第一个快照之前的偏移，而 `TAIL` 是指上一个快照之后的偏移。

>[!NOTE]
>
>如果在两个快照ID之间进行查询并且启动快照已过期，则可能会出现以下两种情况，具体取决于可选的回退行为标记(`resolve_fallback_snapshot_on_failure`)设置：
>
>- 如果设置了可选的回退行为标志，查询服务将选择最早可用的快照，将其设置为开始快照，并返回最早可用快照与指定的结束快照之间的数据。 此数据为 **包含** 最早的可用快照的。
>
>- 如果未设置可选的回退行为标记，则将返回错误。


### WHERE子句

默认情况下，由生成的匹配项 `WHERE` 子句 `SELECT` 查询区分大小写。 如果希望匹配项不区分大小写，则可以使用关键字 `ILIKE` 而不是 `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

下表解释了LIKE和ILIKE子句的逻辑：

| 子句 | 操作员 |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**示例**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

此查询返回名称以“A”或“a”开头的客户。

### 加入

A `SELECT` 使用联接的查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION、INTERSECT和EXCEPT

此 `UNION`， `INTERSECT`、和 `EXCEPT` 子句用于组合或排除两个或多个表中的类似行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 创建表作为选择 {#create-table-as-select}

以下语法定义 `CREATE TABLE AS SELECT` (CTAS)查询：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| 参数 | 描述 |
| ----- | ----- |
| `schema` | XDM架构的标题。 仅当您希望为CTAS查询创建的新数据集使用现有XDM架构时，才使用此子句。 |
| `rowvalidation` | （可选）指定用户是否希望对新创建的数据集摄取的每个新批次进行行级验证。 默认值为 `true`。 |
| `label` | 当您使用CTAS查询创建数据集时，请将此标签与的值一起使用 `profile` 将您的数据集标记为已为配置文件启用。 这意味着您的数据集会在创建时自动标记为用户档案。 有关使用的更多信息，请参阅派生的属性扩展文档 `label`. |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询位于 [选择查询部分](#select-queries). |

**示例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>此 `SELECT` 语句必须具有聚合函数的别名，例如 `COUNT`， `SUM`， `MIN`，等等。 此外， `SELECT` 语句可以带有或不带有括号()。 您可以提供 `SNAPSHOT` 子句将增量增量数据读入目标表。

## 插入到

此 `INSERT INTO` 命令定义如下：

```sql
INSERT INTO table_name select_query
```

| 参数 | 描述 |
| ----- | ----- |
| `table_name` | 要插入查询的表的名称。 |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询位于 [选择查询部分](#select-queries). |

**示例**

>[!NOTE]
>
>以下是一个精心设计的示例，仅用于指导目的。

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> 此 `SELECT` 语句 **不得** 括在圆括号()中。 此外， `SELECT` 语句必须符合 `INSERT INTO` 语句。 您可以提供 `SNAPSHOT` 子句将增量增量数据读入目标表。

在根级别未找到实际XDM架构中的大多数字段，并且SQL不允许使用点表示法。 要使用嵌套字段获得逼真的结果，您必须映射 `INSERT INTO` 路径。

至 `INSERT INTO` 嵌套路径，请使用以下语法：

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**示例**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## 放置表

此 `DROP TABLE` 命令删除现有表，如果它不是外部表，则从文件系统中删除与该表关联的目录。 如果该表不存在，则会发生异常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则当表执行了以下操作时，不会引发异常 **非** 存在。 |

## 创建数据库

此 `CREATE DATABASE` 命令创建ADLS数据库。

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 删除数据库

此 `DROP DATABASE` 命令从实例中删除数据库。

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则数据库不会引发异常 **非** 存在。 |

## 删除架构

此 `DROP SCHEMA` 命令删除现有架构。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则当架构执行了以下操作时，不会引发异常 **非** 存在。 |
| `RESTRICT` | 模式的默认值。 如果指定此项，则只有在指定项时，才会删除架构 **不会** 包含任意表。 |
| `CASCADE` | 如果指定此项，则将删除架构以及架构中存在的所有表。 |

## 创建视图

以下语法定义 `CREATE VIEW` 查询：

```sql
CREATE VIEW view_name AS select_query
```

| 参数 | 描述 |
| ------ | ------ |
| `view_name` | 要创建的视图的名称。 |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询位于 [选择查询部分](#select-queries). |

**示例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 放置视图

以下语法定义 `DROP VIEW` 查询：

```sql
DROP VIEW [IF EXISTS] view_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则当视图执行了以下操作时，不会引发异常： **非** 存在。 |
| `view_name` | 要删除的视图的名称。 |

**示例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 匿名块

匿名块由两部分组成：可执行部分和异常处理部分。 在匿名块中，可执行部分是必需的。 但是，“异常处理”部分是可选的。

以下示例说明如何创建包含一个或多个要一起执行的语句的块：

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

以下是使用匿名块的示例。

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### 自动转换为JSON {#auto-to-json}

查询服务支持可选会话级别设置，以便从JSON字符串形式的交互式SELECT查询返回顶级复杂字段。 此 `auto_to_json` 设置允许将复杂字段中的数据作为JSON返回，然后使用标准库解析为JSON对象。

设置功能标志 `auto_to_json` 更改为true，然后再执行包含复杂字段的SELECT查询。

```sql
set auto_to_json=true; 
```

#### 在设置之前 `auto_to_json` 标志

下表提供了在 `auto_to_json` 设置。 在这两种情景中，使用了同一个SELECT查询（如下所示），该查询用于定向具有复杂字段的表。

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

结果如下：

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### 在设置 `auto_to_json` 标志

下表显示了 `auto_to_json` 设置对生成的数据集有。 两种方案都使用了相同的SELECT查询。

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### 解决故障时的回退快照 {#resolve-fallback-snapshot-on-failure}

此 `resolve_fallback_snapshot_on_failure` 选项用于解决快照ID过期的问题。 快照元数据在两天后过期，过期的快照可能会使脚本的逻辑失效。 使用匿名块时可能会出现问题。

设置 `resolve_fallback_snapshot_on_failure` 选项为true时，会使用以前的快照ID覆盖快照。

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

以下代码行将覆盖 `@from_snapshot_id` 具有可用的最早版本 `snapshot_id` 来自元数据。

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## 数据资产组织

随着数据资产的增长，在Adobe Experience Platform数据湖中对它们进行逻辑组织非常重要。 查询服务扩展了SQL构造，使您能够在沙盒中将数据资产进行逻辑分组。 这种组织方法允许在架构之间共享数据资产，而无需在物理上移动它们。

您支持使用标准SQL语法来逻辑组织数据的以下SQL结构。

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

请参阅指南，网址为 [数据资产的逻辑组织](../best-practices/organize-data-assets.md) 有关查询服务最佳实践的更多详细说明。

## 表存在

此 `table_exists` SQL命令用于确认系统中当前是否存在表。 该命令返回一个布尔值： `true` 如果表 **是** 存在，并且 `false` 如果表有 **非** 存在。

通过在运行语句之前验证表是否存在， `table_exists` 功能简化了编写匿名块以同时涵盖 `CREATE` 和 `INSERT INTO` 用例。

以下语法定义 `table_exists` 命令：

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## 内联 {#inline}

此 `inline` 函数将结构数组的元素分隔并生成值到表中。 它只能放置在 `SELECT` 列表或 `LATERAL VIEW`.

此 `inline` 函数 **无法** 放在有其他生成器函数的选择列表中。

默认情况下，生成的列名为“col1”、“col2”，依此类推。 如果表达式为 `NULL` 则不生成行。

>[!TIP]
>
>列名可使用进行重命名 `RENAME` 命令。

**示例**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

此示例返回以下内容：

```text
1  a Spark SQL
2  b Spark SQL
```

第二个示例进一步演示了 `inline` 函数。 下图说明了示例的数据模型。

![productListItems的架构图。](../images/sql/productListItems.png)

**示例**

```sql
select inline(productListItems) from source_dataset limit 10;
```

值取自 `source_dataset` 用于填充目标表。

| SKU | _experience（体验） | 数量 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (“(”(“(A，pass，B，NULL)”)“)”) | 5 | 10.5 |
| product-id-5 | (“(”(“（A，通过， B，NULL）”)”)”) |  |  |
| product-id-2 | (“(”(“(AF， C， D，NULL)”)”)”) | 6 | 40 |
| product-id-4 | (“(”(“(BM，pass， NA，NULL)”)”)”) | 3 | 12 |

## [!DNL Spark] SQL命令

下面的子部分介绍了查询服务支持的Spark SQL命令。

### SET

此 `SET` command设置一个属性，并返回现有属性的值或列出所有现有属性。 如果为现有属性键提供了值，则会覆盖旧值。

```sql
SET property_key = property_value
```

| 参数 | 描述 |
| ------ | ------ |
| `property_key` | 要列出或更改的属性的名称。 |
| `property_value` | 您希望属性设置为的值。 |

要返回任何设置的值，请使用 `SET [property key]` 没有 `property_value`.

## [!DNL PostgreSQL] 命令

以下各小节涵盖 [!DNL PostgreSQL] 查询服务支持的命令。

### 分析表 {#analyze-table}

此 `ANALYZE TABLE` 命令计算加速存储上表的统计信息。 统计是在加速存储上给定表的已执行CTAS或ITAS查询上计算的。

**示例**

```sql
ANALYZE TABLE <original_table_name>
```

以下是使用之后可用的统计计算列表 `ANALYZE TABLE` 命令：-

| 计算值 | 描述 |
|---|---|
| `field` | 表中列的名称。 |
| `data-type` | 每列可接受的数据类型。 |
| `count` | 包含此字段的非null值的行数。 |
| `distinct-count` | 此字段的唯一值或非重复值的数量。 |
| `missing` | 此字段具有null值的行数。 |
| `max` | 分析表中的最大值。 |
| `min` | 分析表的最小值。 |
| `mean` | 分析表的平均值。 |
| `stdev` | 分析表的标准偏差。 |

#### 计算统计信息 {#compute-statistics}

您现在可以计算列级别统计信息 [!DNL Azure Data Lake Storage] (ADLS)数据集具有 `COMPUTE STATISTICS` 和 `SHOW STATISTICS` sql命令。 计算整个数据集、数据集子集、所有列或列子集上的列统计信息。

`COMPUTE STATISTICS` 扩展 `ANALYZE TABLE` 命令。 但是， `COMPUTE STATISTICS`， `FILTERCONTEXT`， `FOR COLUMNS`、和 `SHOW STATISTICS` data warehouse表不支持命令。 的这些扩展 `ANALYZE TABLE` 命令当前仅支持ADLS表。

**示例**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

>[!NOTE]
>
>`FILTER CONTEXT` 根据提供的筛选条件计算数据集子集的统计信息，并且 `FOR COLUMNS` 定位特定的列以供分析。

控制台输出如下所示。

```console
  Statistics ID 
------------------
 ULKQiqgUlGbTJWhO
(1 row)
```

然后，可以使用返回的统计数据ID查找计算出的统计数据，其中 `SHOW STATISTICS` 命令。

```sql
SHOW STATISTICS FOR <statistics_ID>
```

>[!NOTE]
>
>`COMPUTE STATISTICS` 不支持数组或映射数据类型。 您可以设置 `skip_stats_for_complex_datatypes` 如果输入数据流具有带数组和映射数据类型的列，则标记为通知或出错。 默认情况下，该标记设置为true。 要启用通知或错误，请使用以下命令： `SET skip_stats_for_complex_datatypes = false`.

请参阅 [数据集统计文档](../essential-concepts/dataset-statistics.md) 了解更多信息。

#### 表示例 {#tablesample}

Adobe Experience Platform查询服务在其近似的查询处理功能中提供示例数据集。
当不需要对数据集进行聚合操作的确切答案时，最好使用数据集示例。 此功能允许您通过发出近似查询以返回近似答案，对大型数据集执行更有效的探索查询。

使用来自现有样本的均匀随机样本创建样本数据集 [!DNL Azure Data Lake Storage] (ADLS)数据集，仅使用来自原始数据集记录的一个百分比。 数据集示例功能对 `ANALYZE TABLE` 命令和 `TABLESAMPLE` 和 `SAMPLERATE` sql命令。

在以下示例中，第一行演示了如何计算表格的5%样本。 第二行演示了如何从表中数据的过滤视图中计算5%的样本。

**示例**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

请参阅 [数据集示例文档](../essential-concepts/dataset-samples.md) 了解更多信息。

### 开始

此 `BEGIN` 命令，或者 `BEGIN WORK` 或 `BEGIN TRANSACTION` 命令，启动事务块。 在begin命令之后输入的任何语句将在单个事务中执行，直到给出明确的COMMIT或ROLLBACK命令。 此命令与 `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 关闭

此 `CLOSE` command可释放与打开游标相关联的资源。 游标关闭后，不允许对其执行任何后续操作。 当不再需要游标时，应将其关闭。

```sql
CLOSE name
CLOSE ALL
```

如果 `CLOSE name` 已使用， `name` 表示需要关闭的打开游标的名称。 如果 `CLOSE ALL` 将关闭所有打开的游标。

### 取消分配

此 `DEALLOCATE` 命令允许您取消分配以前准备的SQL语句。 如果未显式取消分配预准备语句，则会在会话结束时取消分配该语句。 有关预准备语句的更多信息，请参见 [PREPARE命令](#prepare) 部分。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果 `DEALLOCATE name` 已使用， `name` 表示需要取消分配的准备语句的名称。 如果 `DEALLOCATE ALL` ，则所有已准备的语句都将取消分配。

### 声明

此 `DECLARE` 命令允许用户创建游标，该游标可用于从较大的查询中检索少量行。 创建游标后，将使用从游标中获取行 `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要创建的游标的名称。 |
| `query` | A `SELECT` 或 `VALUES` 命令提供游标要返回的行。 |

### 执行

此 `EXECUTE` 命令用于执行以前准备的语句。 由于准备的语句仅存在于会话期间，因此必须由创建该准备语句的 `PREPARE` 语句在当前会话中较早执行。 有关使用预准备语句的更多信息，请参阅 [`PREPARE` 命令](#prepare) 部分。

如果 `PREPARE` 创建语句的语句指定了某些参数，必须将一组兼容的参数传递给 `EXECUTE` 语句。 如果未传入这些参数，则会引发错误。

```sql
EXECUTE name [ ( parameter ) ]
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要执行的准备语句的名称。 |
| `parameter` | 准备语句的参数实际值。 这必须是生成一个与此参数的数据类型兼容的值的表达式，该值在创建预准备语句时确定。  如果预准备语句有多个参数，则用逗号分隔。 |

### 说明

此 `EXPLAIN` 命令显示提供的语句的执行计划。 执行计划显示如何扫描语句引用的表。  如果引用了多个表，它将显示使用哪些连接算法来汇集每个输入表中的所需行。

```sql
EXPLAIN statement
```

使用 `FORMAT` 带有的关键字 `EXPLAIN` 命令来定义响应的格式。

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| 参数 | 描述 |
| ------ | ------ |
| `FORMAT` | 使用 `FORMAT` 命令指定输出格式。 可用选项包括 `TEXT` 或 `JSON`. 非文本输出包含的信息与文本输出格式相同，但程序更容易解析。 此参数默认为 `TEXT`. |
| `statement` | 任意 `SELECT`， `INSERT`， `UPDATE`， `DELETE`， `VALUES`， `EXECUTE`， `DECLARE`， `CREATE TABLE AS`，或 `CREATE MATERIALIZED VIEW AS` 语句，您希望查看其执行计划。 |

>[!IMPORTANT]
>
>任何输出 `SELECT` 使用运行时，可能返回的语句会被丢弃 `EXPLAIN` 关键字。 该声明的其他副作用照常发生。

**示例**

以下示例显示了对具有单个的表的简单查询的计划 `integer` 列和10000行：

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### FETCH

此 `FETCH` command使用以前创建的游标检索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 参数 | 描述 |
| ------ | ------ |
| `num_of_rows` | 要提取的行数。 |
| `cursor_name` | 从中检索信息的游标的名称。 |

### 准备 {#prepare}

此 `PREPARE` 命令用于创建预准备语句。 预准备语句是服务器端对象，可用于对类似的SQL语句进行模板化。

预准备语句可以接受参数，这些参数是在执行语句时替换到该语句中的值。 使用预准备语句时，参数由位置引用，使用$1、$2等。

或者，您可以指定参数数据类型的列表。 如果未列出参数的数据类型，则可以从上下文推断该类型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 预准备语句的名称。 |
| `data_type` | 预准备语句参数的数据类型。 如果未列出参数的数据类型，则可以从上下文推断该类型。 如果需要添加多个数据类型，可以将其添加到以逗号分隔的列表中。 |

### 回滚

此 `ROLLBACK` 命令撤消当前事务并丢弃该事务进行的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 选择范围

此 `SELECT INTO` 命令创建一个新表，并使用查询计算的数据填充该表。 数据不会返回到客户端，因为它与普通数据一样 `SELECT` 命令。 新表的列具有与的输出列关联的名称和数据类型 `SELECT` 命令。

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

有关标准SELECT查询参数的更多信息，请参阅 [选择查询节](#select-queries). 此部分将仅列出特定于的参数 `SELECT INTO` 命令。

| 参数 | 描述 |
| ------ | ------ |
| `TEMPORARY` 或 `TEMP` | 可选参数。 如果指定，则创建的表将是一个临时表。 |
| `UNLOGGED` | 可选参数。 如果指定，则创建为的表将是一个未记录的表。 有关未记录表的详细信息，请参见 [[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | 要创建的表的名称。 |

**示例**

以下查询创建一个新表 `films_recent` 仅由表中的最近条目组成 `films`：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

此 `SHOW` 命令显示运行时参数的当前设置。 这些变量可以使用以下代码进行设置 `SET` 语句，通过编辑 `postgresql.conf` 配置文件，通过 `PGOPTIONS` 环境变量（在使用libpq或基于libpq的应用程序时），或在启动Postgres服务器时通过命令行标志。

```sql
SHOW name
SHOW ALL
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 您希望了解其相关信息的运行时参数的名称。 运行时参数的可能值包括以下值：<br>`SERVER_VERSION`：此参数显示服务器的版本号。<br>`SERVER_ENCODING`：此参数显示服务器端字符集编码。<br>`LC_COLLATE`：此参数显示数据库的归类（文本排序）区域设置。<br>`LC_CTYPE`：此参数显示数据库的字符分类区域设置。<br>`IS_SUPERUSER`：此参数显示当前角色是否具有超级用户权限。 |
| `ALL` | 显示所有配置参数的值及其说明。 |

**示例**

以下查询显示参数的当前设置 `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 复制

此 `COPY` 命令复制任何 `SELECT` 查询到指定的位置。 用户必须有权访问此位置，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 参数 | 描述 |
| ------ | ------ |
| `query` | 要复制的查询。 |
| `format_name` | 您希望在其中复制查询的格式。 此 `format_name` 可以是 `parquet`， `csv`，或 `json`. 默认情况下，该值为 `parquet`. |

>[!NOTE]
>
>完整的输出路径将为 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### 更改表 {#alter-table}

此 `ALTER TABLE` 命令允许您添加或删除主键或外键约束，以及向表中添加列。


#### 添加或删除约束

以下SQL查询显示了向表添加或删除约束的示例。

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| 参数 | 描述 |
| ------ | ------ |
| `table_name` | 正在编辑的表的名称。 |
| `column_name` | 要向其添加约束的列的名称。 |
| `referenced_table_name` | 外键引用的表的名称。 |
| `primary_column_name` | 外键引用的列的名称。 |


>[!NOTE]
>
>表架构应是唯一的，并且不在多个表之间共享。 此外，对于主键、主标识和标识约束，命名空间是必需的。

#### 添加或删除主要标识和次要标识

此 `ALTER TABLE` 命令允许您直接通过SQL添加或删除主标识表和辅助标识表列的约束条件。

以下示例通过添加约束来添加主标识和辅助标识。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

也可以通过删除约束来删除身份，如下面的示例所示。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

查看文档 [在临时数据集中设置身份](../data-governance/ad-hoc-schema-identities.md) 以了解更多详细信息。

#### 添加列

以下SQL查询显示向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### 支持的数据类型

下表列出了向表中添加列时接受的数据类型，使用的是 [!DNL Postgres SQL]、 XDM和 [!DNL Accelerated Database Recovery] (ADR)。

| — | PSQL客户端 | XDM | ADR | 描述 |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | 用于存储大整数的数字数据类型，范围从 — 9,223,372,036,854,775,807到9,223,372,036,854,775,807，以8字节为单位。 |
| 2 | `integer` | `int4` | `integer` | 用于存储 — 2,147,483,648到2,147,483,647范围内（4字节）的整数的数字数据类型。 |
| 3 | `smallint` | `int2` | `smallint` | 用于存储–32,768到215-1 32,767 （以2字节为单位）的整数的数字数据类型。 |
| 4 | `tinyint` | `int1` | `tinyint` | 用于存储0到255之间的整数（以1字节为单位）的数字数据类型。 |
| 5 | `varchar(len)` | `string` | `varchar(len)` | 可变大小的字符数据类型。 `varchar` 最适合在列数据条目大小差别很大时使用。 |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` 和 `FLOAT` 是的有效同义词 `DOUBLE PRECISION`. `double precision` 是浮点数据类型。 浮点值以8字节为单位存储。 |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` 是的有效同义词 `double precision`.`double precision` 是浮点数据类型。 浮点值以8字节为单位存储。 |
| 8 | `date` | `date` | `date` | 此 `date` 数据类型是4字节存储的日历日期值，没有任何时间戳信息。 有效日期的范围为01-01-0001到12-31-9999。 |
| 9 | `datetime` | `datetime` | `datetime` | 一种数据类型，用于存储以日历日期和时间表示的时间瞬间。 `datetime` 包括year、month、day、hour、second和fraction的限定符。 A `datetime` 声明可以包括这些时间单位中在顺序中连接任何子集，或者甚至包括单个时间单位。 |
| 10 | `char(len)` | `string` | `char(len)` | 此 `char(len)` 关键字用于指示项目是固定长度的字符。 |

#### 添加架构

以下SQL查询显示向数据库/模式添加表的示例。

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 无法将ADLS表和视图添加到DWH数据库/架构中。


#### 删除架构

以下SQL查询显示从数据库/模式中删除表的示例。

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 无法从物理链接的DWH数据库/架构中删除DWH表和视图。


**参数**

| 参数 | 描述 |
| ------ | ------ |
| `table_name` | 正在编辑的表的名称。 |
| `column_name` | 要添加列的名称。 |
| `data_type` | 要添加列的数据类型。 支持的数据类型包括：bigint、char、string、date、datetime、double、double precision、integer、smallint、tinyint、varchar。 |

### 显示主键

此 `SHOW PRIMARY KEYS` command列出给定数据库的所有主键约束。

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### 显示外键

此 `SHOW FOREIGN KEYS` command列出给定数据库的所有外键约束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### 显示数据组

此 `SHOW DATAGROUPS` 命令返回所有关联数据库的表。 对于每个数据库，该表包括方案、组类型、子类型、子名称和子ID。

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### 显示表的数据组

此 `SHOW DATAGROUPS FOR` &#39;table_name&#39;命令返回一个表，其中包含作为子参数的全部相关数据库。 对于每个数据库，该表包括方案、组类型、子类型、子名称和子ID。

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**参数**

- `table_name`：要为其查找关联数据库的表的名称。

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
