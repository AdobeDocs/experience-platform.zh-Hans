---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；SQL语法；SQL;CTAS;CTAS；选择创建表
solution: Experience Platform
title: 查询服务中的SQL语法
topic-legacy: syntax
description: 本文档显示Adobe Experience Platform查询服务支持的SQL语法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 25953a5a1f5b32de7d150dbef700ad06ce6014df
workflow-type: tm+mt
source-wordcount: '2747'
ht-degree: 2%

---

# 查询服务中的SQL语法

Adobe Experience Platform查询服务提供使用标准ANSI SQL的功能 `SELECT` 语句和其他有限命令。 本文档介绍支持的SQL语法 [!DNL Query Service].

## 选择查询 {#select-queries}

以下语法定义 `SELECT` 支持的查询 [!DNL Query Service]:

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

where `from_item` 可以是以下选项之一：

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

以下子部分提供了有关可在查询中使用的附加条款的详细信息，前提是这些条款遵循上述格式。

### SNAPSHOT子句

此子句可用于基于快照ID增量读取表上的数据。 快照ID是由长类型数字表示的检查点标记，每次向其写入数据时，该长类型数字都会应用于数据湖表。 的 `SNAPSHOT` 子句将自身附加到它旁边使用的表关系。

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

请注意， `SNAPSHOT` 子句可与表或表别名一起使用，但不能在子查询或视图的顶部使用。 A `SNAPSHOT` 子句在a `SELECT` 可以对表应用查询。

此外，您还可以使用 `HEAD` 和 `TAIL` 作为快照子句的特殊偏移值。 使用 `HEAD` 是指第一个快照之前的偏移，而 `TAIL` 指上次快照后的偏移。

>[!NOTE]
>
>如果您在两个快照ID之间进行查询，并且启动快照已过期，则可能会出现以下两种情况，具体取决于可选的回退行为标记(`resolve_fallback_snapshot_on_failure`):
>
>- 如果设置了可选的回退行为标志，查询服务将选择最早的可用快照，将其设置为开始快照，并返回最早可用快照和指定的结束快照之间的数据。 此数据为 **包含** 最早可用快照。
>
>- 如果未设置可选的回退行为标记，则将返回错误。


### WHERE子句

默认情况下，由 `WHERE` 子句 `SELECT` 查询区分大小写。 如果希望匹配项不区分大小写，则可以使用关键字 `ILIKE` 而不是 `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

下表说明了LIKE和ILIKE子句的逻辑：

| 子句 | 运算符 |
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

此查询会返回名称以“A”或“a”开头的客户。

### 加入

A `SELECT` 使用连接的查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 并集、交叉和除外

的 `UNION`, `INTERSECT`和 `EXCEPT` 子句用于组合或排除两个或多个表中的类似行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 创建选定表

以下语法定义 `CREATE TABLE AS SELECT` (CTAS)查询：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| 参数 | 描述 |
| ----- | ----- |
| `schema` | XDM架构的标题。 仅当您希望对由CTAS查询创建的新数据集使用现有XDM架构时，才使用此子句。 |
| `rowvalidation` | （可选）指定用户是否希望对为新创建数据集摄取的每个新批次进行行级别验证。 默认值为 `true`。 |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询可在 [“选择查询”部分](#select-queries). |

**示例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>的 `SELECT` 语句必须具有聚合函数的别名，如 `COUNT`, `SUM`, `MIN`，等等。 此外， `SELECT` 语句可以带有或不带括号()。 您可以提供 `SNAPSHOT` 用于将增量增量增量读取到目标表中的子句。

## 插入到

的 `INSERT INTO` 命令的定义如下：

```sql
INSERT INTO table_name select_query
```

| 参数 | 描述 |
| ----- | ----- |
| `table_name` | 要将查询插入到的表的名称。 |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询可在 [“选择查询”部分](#select-queries). |

**示例**

>[!NOTE]
>
>下面是一个辅助示例，仅用于指导目的。

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> 的 `SELECT` 语句 **必须** 括在括号()中。 此外， `SELECT` 语句必须符合 `INSERT INTO` 语句。 您可以提供 `SNAPSHOT` 用于将增量增量增量读取到目标表中的子句。

实际XDM架构中的大多数字段在根级别未找到，并且SQL不允许使用点表示法。 要使用嵌套字段获得真实的结果，必须映射 `INSERT INTO` 路径。

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

## 拖放表

的 `DROP TABLE` 命令会删除现有表，如果该表不是外部表，则会从文件系统中删除与该表关联的目录。 如果表不存在，则会发生异常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此值，则在表执行此操作时不会引发异常 **not** 存在。 |

## 创建数据库

的 `CREATE DATABASE` 命令创建ADLS数据库。

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 删除数据库

的 `DROP DATABASE` 命令从实例中删除数据库。

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此值，则在数据库执行 **not** 存在。 |

## 删除架构

的 `DROP SCHEMA` 命令会删除现有架构。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此设置，则在架构执行此设置时不会引发异常 **not** 存在。 |
| `RESTRICT` | 模式的默认值。 如果指定了此设置，则仅当架构 **does&#39;t** 包含任何表。 |
| `CASCADE` | 如果指定了此值，则将删除架构以及架构中存在的所有表。 |

## 创建视图

以下语法定义 `CREATE VIEW` 查询：

```sql
CREATE VIEW view_name AS select_query
```

| 参数 | 描述 |
| ------ | ------ |
| `view_name` | 要创建的视图的名称。 |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询可在 [“选择查询”部分](#select-queries). |

**示例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 下拉视图

以下语法定义 `DROP VIEW` 查询：

```sql
DROP VIEW [IF EXISTS] view_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定了此值，则在视图为 **not** 存在。 |
| `view_name` | 要删除的视图名称。 |

**示例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 匿名块

匿名块包含两个部分：可执行和异常处理部分。 在匿名块中，可执行文件部分是强制性的。 但是，异常处理部分是可选的。

以下示例显示如何使用一个或多个语句创建块以一起执行：

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

以下示例使用匿名块。

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
```

## 数据资产组织

在Adobe Experience Platform数据湖中按逻辑组织数据资产，这一点非常重要。 查询服务扩展了SQL结构，使您能够在沙盒中对数据资产进行逻辑分组。 这种组织方法允许在架构之间共享数据资产，而无需实际移动它们。

支持以下使用标准SQL语法的SQL结构，以便对数据进行逻辑组织。

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

请参阅 [数据资产的逻辑组织](../best-practices/organize-data-assets.md) 以详细说明查询服务最佳实践。

## 表存在

的 `table_exists` SQL命令用于确认系统中当前是否存在表。 该命令返回一个布尔值： `true` 如果表 **does** 存在，并且 `false` 如果表格显示 **not** 存在。

通过在运行语句之前验证表是否存在， `table_exists` 该功能简化了编写匿名块以涵盖 `CREATE` 和 `INSERT INTO` 用例。

以下语法定义了 `table_exists` 命令：

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

的 `inline` 函数将结构数组的元素分离，并将值生成到表中。 它只能放在 `SELECT` 列表或 `LATERAL VIEW`.

的 `inline` 函数 **无法** 被置于一个选择列表中，该列表中还有其他生成器函数。

默认情况下，生成的列将命名为“col1”、“col2”等。 如果表达式为 `NULL` 则不会生成任何行。

>[!TIP]
>
>列名称可以使用 `RENAME` 命令。

**示例**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

该示例返回以下内容：

```text
1  a Spark SQL
2  b Spark SQL
```

第二个示例进一步演示了 `inline` 函数。 该示例的数据模型如下图所示。

![productListItems的架构图](../images/sql/productListItems.png)

**示例**

```sql
select inline(productListItems) from source_dataset limit 10;
```

从 `source_dataset` 用于填充target表。

| SKU | _experience（体验） | 数量 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A，pass，B，NULL)&quot;)&quot;) | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(A， pass， B，NULL)&quot;)&quot;) |  |  |
| product-id-2 | (&quot;(&quot;(AF， C， D，NULL)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;（BM，传递， NA，NULL）&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL命令

以下子部分涵盖查询服务支持的Spark SQL命令。

### 设置

的 `SET` 命令会设置属性，并返回现有属性的值或列出所有现有属性。 如果为现有属性键值提供了，则会覆盖旧值。

```sql
SET property_key = property_value
```

| 参数 | 描述 |
| ------ | ------ |
| `property_key` | 要列出或更改的属性的名称。 |
| `property_value` | 您希望将属性设置为的值。 |

要返回任何设置的值，请使用 `SET [property key]` 没有 `property_value`.

## PostgreSQL命令

以下子部分涵盖查询服务支持的PostgreSQL命令。

### 开始

的 `BEGIN` 或 `BEGIN WORK` 或 `BEGIN TRANSACTION` 命令启动事务块。 在开始命令之后输入的任何语句将在单个事务中执行，直到给出明确的COMMIT或ROLLBACK命令。 此命令与 `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 关闭

的 `CLOSE` 命令可释放与打开的游标关联的资源。 光标关闭后，不允许对其执行后续操作。 当不再需要游标时，应该将其关闭。

```sql
CLOSE name
CLOSE ALL
```

如果 `CLOSE name` , `name` 表示需要关闭的打开游标的名称。 如果 `CLOSE ALL` ，则所有打开的游标都将关闭。

### 取消分配

的 `DEALLOCATE` 命令允许您取消分配以前准备的SQL语句。 如果未明确取消分配预准备语句，则会在会话结束时取消分配该语句。 有关准备语句的更多信息，请参阅 [准备命令](#prepare) 中。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果 `DEALLOCATE name` , `name` 表示需要取消分配的已准备语句的名称。 如果 `DEALLOCATE ALL` ，所有准备的语句都将被取消分配。

### 声明

的 `DECLARE` 命令允许用户创建游标，该游标可用于从较大的查询中检索少量行。 创建游标后，将使用 `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要创建的游标的名称。 |
| `query` | A `SELECT` 或 `VALUES` 命令，该命令提供游标要返回的行。 |

### 执行

的 `EXECUTE` 命令用于执行先前准备的语句。 由于准备的语句仅在会期期间存在，因此准备的语句必须由 `PREPARE` 语句在当前会话之前执行。 有关使用预准备语句的更多信息，请参阅 [`PREPARE` 命令](#prepare) 中。

如果 `PREPARE` 创建语句的语句指定了一些参数，则必须将一组兼容的参数传递到 `EXECUTE` 语句。 如果未传递这些参数，则会引发错误。

```sql
EXECUTE name [ ( parameter ) ]
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要执行的准备语句的名称。 |
| `parameter` | 准备语句的参数的实际值。 这必须是一个表达式，其中生成的值与此参数的数据类型兼容，这取决于创建预准备语句时所确定的值。  如果准备语句有多个参数，则它们之间用逗号分隔。 |

### 解释

的 `EXPLAIN` 命令显示所提供语句的执行计划。 执行计划显示如何扫描语句引用的表。  如果引用了多个表，则将显示用于将每个输入表中的所需行汇总在一起的联接算法。

```sql
EXPLAIN option statement
```

其中 `option` 可以是以下之一：

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

| 参数 | 描述 |
| ------ | ------ |
| `ANALYZE` | 如果 `option` 包含 `ANALYZE`，则会显示运行时间和其他统计信息。 |
| `FORMAT` | 如果 `option` 包含 `FORMAT`，它指定输出格式，格式可以是 `TEXT` 或 `JSON`. 非文本输出包含与文本输出格式相同的信息，但便于程序解析。 此参数默认为 `TEXT`. |
| `statement` | 任意 `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`或 `CREATE MATERIALIZED VIEW AS` 语句，您希望查看其执行计划。 |

>[!IMPORTANT]
>
>请记住，当 `ANALYZE` 选项。 尽管 `EXPLAIN` 会丢弃 `SELECT` 返回时，语句的其他副作用会照常发生。

**示例**

以下示例显示了对单个表进行简单查询的计划 `integer` 列和10000行：

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 获取

的 `FETCH` 命令使用之前创建的游标检索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 参数 | 描述 |
| ------ | ------ |
| `num_of_rows` | 要获取的行数。 |
| `cursor_name` | 从中检索信息的游标的名称。 |

### 准备 {#prepare}

的 `PREPARE` 命令可创建准备语句。 准备语句是服务器端对象，可用于模板类似的SQL语句。

预准备语句可以采用参数，这些参数是执行语句时替换到语句中的值。 在使用准备的语句时，参数按位置（使用$1、$2等）引用。

或者，您也可以指定参数数据类型列表。 如果未列出参数的数据类型，则可以从上下文推断该类型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 准备语句的名称。 |
| `data_type` | 准备语句参数的数据类型。 如果未列出参数的数据类型，则可以从上下文推断该类型。 如果需要添加多个数据类型，可以将其添加到逗号分隔列表中。 |

### 回滚

的 `ROLLBACK` 命令将取消当前事务，并丢弃该事务所做的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 选择到

的 `SELECT INTO` 命令会创建一个新表，并使用由查询计算的数据填充该表。 数据不会返回给客户端，因为它是正常的 `SELECT` 命令。 新表的列具有与 `SELECT` 命令。

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

有关标准SELECT查询参数的更多信息，请参阅 [选择查询节](#select-queries). 此部分将仅列出 `SELECT INTO` 命令。

| 参数 | 描述 |
| ------ | ------ |
| `TEMPORARY` 或 `TEMP` | 可选参数。 如果指定，则所创建的表将是临时表。 |
| `UNLOGGED` | 可选参数。 如果指定，则创建为的表将是一个未记录的表。 有关未记录表格的更多信息，请参阅 [PostgreSQL文档](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | 要创建的表的名称。 |

**示例**

以下查询将创建一个新表 `films_recent` 只包含表中最近的条目 `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

的 `SHOW` 命令显示运行时参数的当前设置。 这些变量可以使用 `SET` 语句，通过编辑 `postgresql.conf` 配置文件，通过 `PGOPTIONS` 环境变量（使用libpq或基于libpq的应用程序时），或者在启动Postgres服务器时通过命令行标记。

```sql
SHOW name
SHOW ALL
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要了解相关信息的运行时参数的名称。 运行时参数的可能值包括以下值：<br>`SERVER_VERSION`:此参数显示服务器的版本号。<br>`SERVER_ENCODING`:此参数显示服务器端字符集编码。<br>`LC_COLLATE`:此参数显示数据库的归类区域设置（文本排序）。<br>`LC_CTYPE`:此参数显示字符分类的数据库区域设置。<br>`IS_SUPERUSER`:此参数显示当前角色是否具有超级用户权限。 |
| `ALL` | 显示所有配置参数的值及说明。 |

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

的 `COPY` 命令复制任何 `SELECT` 查询到指定位置。 用户必须有权访问此位置，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 参数 | 描述 |
| ------ | ------ |
| `query` | 要复制的查询。 |
| `format_name` | 要在中复制查询的格式。 的 `format_name` 可以是 `parquet`, `csv`或 `json`. 默认情况下，值为 `parquet`. |

>[!NOTE]
>
>完整的输出路径将为 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

的 `ALTER TABLE` 命令允许您添加或删除主键或外键约束，以及向表中添加列。


#### 添加或删除约束

以下SQL查询显示了向表添加或删除约束的示例。

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

| 参数 | 描述 |
| ------ | ------ |
| `table_name` | 要编辑的表的名称。 |
| `constraint_name` | 要添加或删除的约束的名称。 |
| `column_name` | 要向其添加约束的列的名称。 |
| `referenced_table_name` | 外键引用的表的名称。 |
| `primary_column_name` | 外键引用的列的名称。 |

>[!NOTE]
>
>表架构应是唯一的，且不会在多个表之间共享。 此外，对于主键约束，命名空间是必填的。

#### 添加列

以下SQL查询显示了向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

#### 添加架构

以下SQL查询显示了向数据库/模式添加表的示例。

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS表和视图无法添加到DWH数据库/模式。


#### 删除架构

以下SQL查询显示了从数据库/模式中删除表的示例。

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 不能从物理链接的DWH数据库/模式中删除DWH表和视图。


**参数**

| 参数 | 描述 |
| ------ | ------ |
| `table_name` | 要编辑的表的名称。 |
| `column_name` | 要添加的列的名称。 |
| `data_type` | 要添加的列的数据类型。 支持的数据类型包括：bigint， char， string， date， datetime， double， double precision，整数， smallint， tinyint， varchar。 |

### 显示主键

的 `SHOW PRIMARY KEYS` 命令列出了给定数据库的所有主键约束。

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

的 `SHOW FOREIGN KEYS` 命令列出了给定数据库的所有外键约束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### 显示DATAGROUPS

的 `SHOW DATAGROUPS` 命令返回所有关联数据库的表。 对于每个数据库，表都包括架构、组类型、子类型、子名称和子ID。

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


### 为表显示数据组

的 `SHOW DATAGROUPS FOR` “table_name”命令返回所有关联数据库的表，这些数据库包含参数作为其子参数。 对于每个数据库，表都包括架构、组类型、子类型、子名称和子ID。

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**参数**

- `table_name`:要为其查找关联数据库的表的名称。

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
