---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；SQL语法；SQL;CTAS;CTAS；选择创建表
solution: Experience Platform
title: 查询服务中的SQL语法
topic-legacy: syntax
description: 本文档显示Adobe Experience Platform查询服务支持的SQL语法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 26bd2abc998320245091b0917fb6f236ed09b95c
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 1%

---

# 查询服务中的SQL语法

Adobe Experience Platform查询服务提供了对`SELECT`语句和其他有限命令使用标准ANSI SQL的功能。 本文档介绍[!DNL Query Service]支持的SQL语法。

## 选择查询{#select-queries}

以下语法定义了[!DNL Query Service]支持的`SELECT`查询：

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

其中`from_item`可以是以下选项之一：

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

和`grouping_element`可以是以下选项之一：

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

`with_query`为：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

以下子部分提供了有关可在查询中使用的附加条款的详细信息，前提是这些条款遵循上述格式。

### SNAPSHOT子句

此子句可用于基于快照ID增量读取表上的数据。 快照ID是由长类型数字表示的检查点标记，每次向其写入数据时，该长类型数字都会应用于数据湖表。 `SNAPSHOT`子句将自身附加到它旁边使用的表关系。

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

请注意，`SNAPSHOT`子句可与表或表别名一起使用，但不能在子查询或视图上使用。 `SNAPSHOT`子句可以在任何可以应用表`SELECT`查询的位置使用。

此外，还可以将`HEAD`和`TAIL`用作快照子句的特殊偏移值。 使用`HEAD`表示第一个快照之前的偏移，而使用`TAIL`表示最后一个快照之后的偏移。

### WHERE子句

默认情况下，由`SELECT`查询上的`WHERE`子句生成的匹配区分大小写。 如果希望匹配项不区分大小写，则可以使用关键字`ILIKE`而不是`LIKE`。

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

使用连接的`SELECT`查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 并集、交叉和除外

`UNION`、`INTERSECT`和`EXCEPT`子句用于组合或排除两个或多个表中类似的行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 创建选定表

以下语法定义了`CREATE TABLE AS SELECT`(CTAS)查询：

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**参数**

- `schema`:XDM架构的标题。仅当您希望对由CTAS查询创建的新数据集使用现有XDM架构时，才使用此子句。
- `rowvalidation`:（可选）指定用户是否希望对为新创建数据集摄取的每个新批次进行行级别验证。默认值为 `true`。
- `select_query`:一个 `SELECT` 声明。`SELECT`查询的语法可在[SELECT查询部分](#select-queries)中找到。

**示例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>`SELECT`语句必须具有聚合函数的别名，如`COUNT`、`SUM`、`MIN`等。 此外，`SELECT`语句可以带有或不带括号()。 您可以提供`SNAPSHOT`子句，以将增量增量增量读取到目标表中。

## 插入到

`INSERT INTO`命令的定义如下：

```sql
INSERT INTO table_name select_query
```

**参数**

- `table_name`:要将查询插入到的表的名称。
- `select_query`:一个 `SELECT` 声明。`SELECT`查询的语法可在[SELECT查询部分](#select-queries)中找到。

**示例**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> `SELECT`语句&#x200B;**不得**&#x200B;包含在括号()中。 此外，`SELECT`语句结果的模式必须符合`INSERT INTO`语句中定义的表的模式。 您可以提供`SNAPSHOT`子句，以将增量增量增量读取到目标表中。

## 拖放表

`DROP TABLE`命令会删除一个现有表，如果该表不是外部表，则会从文件系统中删除与该表关联的目录。 如果表不存在，则会发生异常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**参数**

- `IF EXISTS`:如果指定了此值，则如果表没有文本列表，则不会引发任 **** 何异常。

## 删除数据库

`DROP DATABASE`命令会删除现有数据库。

```sql
DROP DATABASE [IF EXISTS] db_name
```

**参数**

- `IF EXISTS`:如果指定了此值，则如果数据库没有文本列表，则不会引发任 **** 何异常。

## 删除架构

`DROP SCHEMA`命令会删除现有架构。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

**参数**

- `IF EXISTS`:如果指定了此设置，则如果架构没有文本列表，则不会引发任 **** 何异常。

- `RESTRICT`:模式的默认值。如果指定了此值，则仅当&#x200B;**不**&#x200B;包含任何表时，才会删除架构。

- `CASCADE`:如果指定了此值，则将删除架构以及架构中存在的所有表。

## 创建视图

以下语法定义`CREATE VIEW`查询：

```sql
CREATE VIEW view_name AS select_query
```

**参数**

- `view_name`:要创建的视图的名称。
- `select_query`:一个 `SELECT` 声明。`SELECT`查询的语法可在[SELECT查询部分](#select-queries)中找到。

**示例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 下拉视图

以下语法定义`DROP VIEW`查询：

```sql
DROP VIEW [IF EXISTS] view_name
```

**参数**

- `IF EXISTS`:如果指定了此值，则如果视图没有文本列表，则不会引发 **** 异常。
- `view_name`:要删除的视图名称。

**示例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL命令

以下子部分涵盖查询服务支持的Spark SQL命令。

### 设置

`SET`命令可设置属性，并返回现有属性的值或列出所有现有属性。 如果为现有属性键值提供了，则会覆盖旧值。

```sql
SET property_key = property_value
```

**参数**

- `property_key`:要列出或更改的属性的名称。
- `property_value`:您希望将属性设置为的值。

要返回任何设置的值，请使用不带`property_value`的`SET [property key]`。

## PostgreSQL命令

以下子部分涵盖查询服务支持的PostgreSQL命令。

### 开始

`BEGIN`命令或`BEGIN WORK`或`BEGIN TRANSACTION`命令会启动事务块。 在开始命令之后输入的任何语句将在单个事务中执行，直到给出明确的COMMIT或ROLLBACK命令。 此命令与`START TRANSACTION`相同。

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 关闭

`CLOSE`命令释放与打开游标相关的资源。 光标关闭后，不允许对其执行后续操作。 当不再需要游标时，应该将其关闭。

```sql
CLOSE name
CLOSE ALL
```

如果使用`CLOSE name`，则`name`表示需要关闭的打开游标的名称。 如果使用`CLOSE ALL`，则所有打开的游标都将关闭。

### 取消分配

使用`DEALLOCATE`命令可以取消分配以前准备的SQL语句。 如果未明确取消分配预准备语句，则会在会话结束时取消分配该语句。 有关准备语句的更多信息，请参见[PREPARE命令](#prepare)一节。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果使用`DEALLOCATE name`，则`name`表示需要取消分配的准备语句的名称。 如果使用`DEALLOCATE ALL`，则所有准备的语句都将被取消分配。

### 声明

`DECLARE`命令允许用户创建游标，该游标可用于从较大的查询中检索少量行。 创建游标后，使用`FETCH`从游标中获取行。

```sql
DECLARE name CURSOR FOR query
```

**参数**

- `name`:要创建的游标的名称。
- `query`:提 `SELECT` 供游 `VALUES` 标要返回的行的或命令。

### 执行

`EXECUTE`命令用于执行先前准备的语句。 由于准备语句仅在会话期间存在，因此准备语句必须由在当前会话之前执行的`PREPARE`语句创建。 有关使用预准备语句的更多信息，请参阅[`PREPARE`命令](#prepare)部分。

如果创建该语句的`PREPARE`语句指定了一些参数，则必须将一组兼容的参数传递到`EXECUTE`语句中。 如果未传递这些参数，则会引发错误。

```sql
EXECUTE name [ ( parameter ) ]
```

**参数**

- `name`:要执行的准备语句的名称。
- `parameter`:准备语句的参数的实际值。这必须是一个表达式，其中生成的值与此参数的数据类型兼容，这取决于创建预准备语句时所确定的值。  如果准备语句有多个参数，则它们之间用逗号分隔。

### 解释

`EXPLAIN`命令显示所提供语句的执行计划。 执行计划显示如何扫描语句引用的表。  如果引用了多个表，则将显示用于将每个输入表中的所需行汇总在一起的联接算法。

```sql
EXPLAIN option statement
```

其中`option`可以是以下任一值：

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**参数**

- `ANALYZE`:如果包 `option` 含 `ANALYZE`，则会显示运行时间和其他统计信息。
- `FORMAT`:如果包 `option` 含 `FORMAT`，则会指定输出格式，格式可以 `TEXT` 为或 `JSON`。非文本输出包含与文本输出格式相同的信息，但便于程序解析。 此参数默认为`TEXT`。
- `statement`:要查看 `SELECT`其执行计划的任 `INSERT`何、 `UPDATE`、 `DELETE`、 `VALUES` `EXECUTE`、 `DECLARE` `CREATE TABLE AS`或 `CREATE MATERIALIZED VIEW AS` 语句。

>[!IMPORTANT]
>
>请记住，当使用`ANALYZE`选项时，实际会执行该语句。 尽管`EXPLAIN`会丢弃`SELECT`返回的任何输出，但语句的其他副作用会照常发生。

**示例**

以下示例显示了在具有单个`integer`列和10000行的表上执行简单查询的计划：

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

`FETCH`命令使用先前创建的游标检索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**参数**

- `num_of_rows`:要获取的行数。
- `cursor_name`:从中检索信息的游标的名称。

### 准备 {#prepare}

使用`PREPARE`命令可以创建准备语句。 准备语句是服务器端对象，可用于模板类似的SQL语句。

预准备语句可以采用参数，这些参数是执行语句时替换到语句中的值。 在使用准备的语句时，参数按位置（使用$1、$2等）引用。

或者，您也可以指定参数数据类型列表。 如果未列出参数的数据类型，则可以从上下文推断该类型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**参数**

- `name`:准备语句的名称。
- `data_type`:准备语句参数的数据类型。如果未列出参数的数据类型，则可以从上下文推断该类型。 如果需要添加多个数据类型，可以将其添加到逗号分隔列表中。

### 回滚

`ROLLBACK`命令将取消当前事务，并丢弃该事务所做的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 选择到

`SELECT INTO`命令会创建一个新表，并使用查询计算的数据填充该表。 数据不会返回给客户端，因为它使用普通的`SELECT`命令。 新表的列具有与`SELECT`命令的输出列关联的名称和数据类型。

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

**参数**

有关标准SELECT查询参数的更多信息，请参见[SELECT查询节](#select-queries)。 此部分将仅列出`SELECT INTO`命令专用的参数。

- `TEMPORARY` 或： `TEMP`可选参数。如果指定，则所创建的表将是临时表。
- `UNLOGGED`:可选参数。如果指定，则创建为的表将是一个未记录的表。 有关未记录表的详细信息，请参阅[PostgreSQL文档](https://www.postgresql.org/docs/current/sql-createtable.html)。
- `new_table`:要创建的表的名称。

**示例**

以下查询将创建一个新表`films_recent`，该表仅包含表`films`中的最近条目：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

`SHOW`命令显示运行时参数的当前设置。 这些变量可以使用`SET`语句进行设置，方法是：编辑`postgresql.conf`配置文件，通过`PGOPTIONS`环境变量（使用libpq或基于libpq的应用程序时）进行设置，或者在启动Postgres服务器时通过命令行标记进行设置。

```sql
SHOW name
SHOW ALL
```

**参数**

- `name`:要了解相关信息的运行时参数的名称。运行时参数的可能值包括以下值：
   - `SERVER_VERSION`:此参数显示服务器的版本号。
   - `SERVER_ENCODING`:此参数显示服务器端字符集编码。
   - `LC_COLLATE`:此参数显示数据库的归类区域设置（文本排序）。
   - `LC_CTYPE`:此参数显示字符分类的数据库区域设置。
      `IS_SUPERUSER`:此参数显示当前角色是否具有超级用户权限。
- `ALL`:显示所有配置参数的值及说明。

**示例**

以下查询显示参数`DateStyle`的当前设置。

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

`COPY`命令将任何`SELECT`查询的输出转储到指定位置。 用户必须有权访问此位置，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**参数**

- `query`:要复制的查询。
- `format_name`:要在中复制查询的格式。`format_name`可以是`parquet`、`csv`或`json`之一。 默认情况下，值为`parquet`。

>[!NOTE]
>
>完整的输出路径将为`adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

使用`ALTER TABLE`命令可以添加或删除主键或外键约束，以及向表中添加列。

#### 添加或删除约束

以下SQL查询显示了向表添加或删除约束的示例。

```sql
ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT constraint_name PRIMARY KEY column_name NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT constraint_name PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT constraint_name FOREIGN KEY ( column_name )
```

**参数**

- `table_name`:要编辑的表的名称。
- `constraint_name`:要添加或删除的约束的名称。
- `column_name`:要向其添加约束的列的名称。
- `referenced_table_name`:外键引用的表的名称。
- `primary_column_name`:外键引用的列的名称。

>[!NOTE]
>
>表架构应是唯一的，且不会在多个表之间共享。 此外，对于主键约束，命名空间是必填的。

#### 添加列

以下SQL查询显示了向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**参数**

- `table_name`:要编辑的表的名称。
- `column_name`:要添加的列的名称。
- `data_type`:要添加的列的数据类型。支持的数据类型包括：bigint， char， string， date， datetime， double， double precision，整数， smallint， tinyint， varchar。

### 显示主键

`SHOW PRIMARY KEYS`命令列出了给定数据库的所有主键约束。

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

`SHOW FOREIGN KEYS`命令列出给定数据库的所有外键约束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
