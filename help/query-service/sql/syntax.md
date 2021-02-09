---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；sql语法；sql;ctas;CTAS；创建表作为选择
solution: Experience Platform
title: 查询服务中的SQL语法
topic: syntax
description: 此文档显示Adobe Experience Platform查询服务支持的SQL语法。
translation-type: tm+mt
source-git-commit: 78707257c179101b29e68036bf9173d74f01e03a
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 1%

---


# 查询服务中的SQL语法

Adobe Experience Platform查询服务为`SELECT`语句和其他有限命令提供使用标准ANSI SQL的功能。 此文档涵盖[!DNL Query Service]支持的SQL语法。

## SELECT查询{#select-queries}

以下语法定义[!DNL Query Service]支持的`SELECT`查询:

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

和`with_query`为：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

以下子部分提供了您可以在查询中使用的其他条款的详细信息，前提是这些条款遵循上述格式。

### SNAPSHOT子句

此子句可用于根据快照ID增量读取表上的数据。 快照ID是由长类型数字表示的检查点标记，每次向数据湖表写入数据时，该长类型数字都应用于该数据湖表。 `SNAPSHOT`子句将其自身附加到它旁边使用的表关系。

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

请注意，`SNAPSHOT`子句可用于表或表别名，但不能用于子查询或视图。 `SNAPSHOT`子句在任何可以应用表上`SELECT`查询的地方都有效。

此外，还可以使用`HEAD`和`TAIL`作为快照子句的特殊偏移值。 使用`HEAD`表示第一个快照之前的偏移，而`TAIL`表示最后一个快照之后的偏移。

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

此查询返回名称以“A”或“a”开头的客户。

### 加入

使用连接的`SELECT`查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 合并、INTERSECT和EXCEPT

`UNION`、`INTERSECT`和`EXCEPT`子句用于组合或排除两个或多个表中类似的行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 按选择创建表

以下语法定义`CREATE TABLE AS SELECT`(CTAS)查询:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

**参数**

- `schema`:XDM模式的标题。仅当您希望对由CTAS模式创建的新数据集使用现有XDM查询时，才使用此子句。
- `rowvalidation`:（可选）指定用户是否希望对新创建的数据集摄取的每个新批进行行级验证。默认值为 `true`。
- `select_query`:一份 `SELECT` 声明。[SELECT查询部分](#select-queries)中可以找到`SELECT`查询的语法。

**示例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>`SELECT`语句必须具有聚合函数的别名，如`COUNT`、`SUM`、`MIN`等。 此外，`SELECT`语句可以带有或不带括号()。 可以提供`SNAPSHOT`子句，将增量增量增量读入目标表。

## 插入

`INSERT INTO`命令定义如下：

```sql
INSERT INTO table_name select_query
```

**参数**

- `table_name`:要将查询插入的表的名称。
- `select_query`:一份 `SELECT` 声明。[SELECT查询部分](#select-queries)中可以找到`SELECT`查询的语法。

**示例**

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!NOTE]
> `SELECT`语句&#x200B;**不得**&#x200B;括在括号()中。 此外，`SELECT`语句结果的模式必须与`INSERT INTO`语句中定义的表符合。 可以提供`SNAPSHOT`子句，将增量增量增量读入目标表。

## 删除表

`DROP TABLE`命令删除现有表，并从文件系统中删除与该表关联的目录（如果它不是外部表）。 如果表不存在，则会发生异常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

**参数**

- `IF EXISTS`:如果指定了此值，则表不显示任何异常 **** 情况。

## 创建视图

以下语法定义`CREATE VIEW`查询:

```sql
CREATE VIEW view_name AS select_query
```

**参数**

- `view_name`:要创建的视图的名称。
- `select_query`:一份 `SELECT` 声明。[SELECT查询部分](#select-queries)中可以找到`SELECT`查询的语法。

**示例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## DROP视图

以下语法定义`DROP VIEW`查询:

```sql
DROP VIEW [IF EXISTS] view_name
```

**参数**

- `IF EXISTS`:如果指定了此值，则视图不显示任何异常 **** 情况。
- `view_name`:要删除的视图的名称。

**示例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL命令

以下子部分介绍查询服务支持的Spark SQL命令。

### 设置

`SET`命令设置一个属性，并返回现有属性的值或列表所有现有属性。 如果为现有属性键提供了值，则旧值将被覆盖。

```sql
SET property_key = property_value
```

**参数**

- `property_key`:要列表或更改的属性的名称。
- `property_value`:您希望将属性设置为的值。

要返回任何设置的值，请使用不带`property_value`的`SET [property key]`。

## PostgreSQL命令

以下子部分介绍查询服务支持的PostgreSQL命令。

### 开始

`BEGIN`命令或`BEGIN WORK`或`BEGIN TRANSACTION`命令将启动事务块。 在开始命令之后输入的任何语句将在单个事务中执行，直到给出显式COMMIT或ROLLBACK命令。 此命令与`START TRANSACTION`相同。

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 关闭

`CLOSE`命令释放与打开的游标关联的资源。 关闭光标后，不允许对其执行后续操作。 当不再需要光标时，应关闭它。

```sql
CLOSE name
CLOSE ALL
```

如果使用`CLOSE name`,`name`表示需要关闭的打开游标的名称。 如果使用`CLOSE ALL`，将关闭所有打开的游标。

### 取消分配

`DEALLOCATE`命令允许您取消分配以前准备的SQL语句。 如果不显式取消分配准备语句，则会在会话结束时取消分配该语句。 有关预准备语句的详细信息，请参阅[PREPARE命令](#prepare)部分。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果使用`DEALLOCATE name`,`name`表示需要取消分配的预准备语句的名称。 如果使用`DEALLOCATE ALL`，将取消分配所有准备的语句。

### DECLARE

`DECLARE`命令允许用户创建游标，该游标可用于从较大查询中检索少量行。 创建游标后，使用`FETCH`从游标读取行。

```sql
DECLARE name CURSOR FOR query
```

**参数**

- `name`:要创建的光标的名称。
- `query`:提供 `SELECT` 游 `VALUES` 标要返回的行的或命令。

### 执行

`EXECUTE`命令用于执行先前准备的语句。 由于准备语句仅在会话期间存在，所以准备语句必须由在当前会话之前执行的`PREPARE`语句创建。 有关使用预准备语句的详细信息，请参阅[`PREPARE`命令](#prepare)部分。

如果创建该语句的`PREPARE`语句指定了一些参数，则必须向`EXECUTE`语句传递一组兼容的参数。 如果未传入这些参数，则会引发错误。

```sql
EXECUTE name [ ( parameter ) ]
```

**参数**

- `name`:要执行的准备语句的名称。
- `parameter`:准备语句的参数的实际值。这必须是一个表达式，其生成的值与此参数的数据类型兼容，这取决于创建预准备语句时确定的值。  如果准备语句有多个参数，则这些参数之间用逗号分隔。

### 说明

`EXPLAIN`命令显示所提供语句的执行计划。 执行计划显示如何扫描语句引用的表。  如果引用了多个表，它将显示使用哪些连接算法将每个输入表中所需的行相结合。

```sql
EXPLAIN option statement
```

其中`option`可以是以下任一值：

```sql
ANALYZE
FORMAT { TEXT | JSON }
```

**参数**

- `ANALYZE`:如果包 `option` 含 `ANALYZE`，则显示运行时间和其他统计信息。
- `FORMAT`:如果包 `option` 含 `FORMAT`，则它指定输出格式，可以是 `TEXT` 或 `JSON`。非文本输出包含的信息与文本输出格式相同，但对项目来说更容易进行分析。 此参数默认为`TEXT`。
- `statement`:任何 `SELECT`、、 `INSERT`、 `UPDATE`、、 `DELETE`或您想要 `VALUES`看到的 `EXECUTE` `DECLARE` `CREATE TABLE AS` `CREATE MATERIALIZED VIEW AS` 、、、或者的执行计划。

>[!IMPORTANT]
>
>请记住，使用`ANALYZE`选项时，语句实际会执行。 尽管`EXPLAIN`会丢弃`SELECT`返回的任何输出，但语句的其他副作用会如常发生。

**示例**

以下示例显示了在表上具有单个`integer`列和10000行的简单查询的计划：

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 提取

`FETCH`命令使用先前创建的游标检索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

**参数**

- `num_of_rows`:要提取的行数。
- `cursor_name`:要从中检索信息的光标的名称。

### 准备{#prepare}

使用`PREPARE`命令可以创建预准备语句。 预准备语句是服务器端对象，可用于模拟类似的SQL语句。

预准备的语句可以采用参数，这些参数是执行语句时替换到语句中的值。 参数按位置来引用，使用$1、$2等，使用准备的语句。

（可选）您可以指定参数列表类型。 如果未列出参数的数据类型，则可以从上下文推断该类型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

**参数**

- `name`:准备语句的名称。
- `data_type`:预准备语句的参数的数据类型。如果未列出参数的数据类型，则可以从上下文推断该类型。 如果需要添加多个数据类型，可以以逗号分隔的列表添加这些数据类型。

### 回滚

`ROLLBACK`命令将取消当前事务，并放弃该事务所做的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 选择范围

`SELECT INTO`命令创建一个新表，并用查询计算的数据填充它。 数据不会返回给客户端，因为它使用普通`SELECT`命令。 新表的列具有与`SELECT`命令的输出列关联的名称和数据类型。

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

有关标准SELECT查询参数的详细信息，请参阅[SELECT查询部分](#select-queries)。 此部分将仅列表`SELECT INTO`命令专有的参数。

- `TEMPORARY` 或 `TEMP`:可选参数。如果指定，则创建的表将是临时表。
- `UNLOGGED`:可选参数。如果指定，则创建为的表将是未记录的表。 有关未记录表的详细信息，请参阅[PostgreSQL文档](https://www.postgresql.org/docs/current/sql-createtable.html)。
- `new_table`:要创建的表的名称。

**示例**

以下查询创建一个新表`films_recent`，其中只包含表`films`中最近的条目：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

`SHOW`命令显示运行时参数的当前设置。 这些变量可以使用`SET`语句进行设置，方法是编辑`postgresql.conf`配置文件，通过`PGOPTIONS`环境变量（使用libpq或基于libpq的应用程序时），或者在启动Postgres服务器时通过命令行标记。

```sql
SHOW name
SHOW ALL
```

**参数**

- `name`:要获得相关信息的运行时参数的名称。运行时参数的可能值包括以下值：
   - `SERVER_VERSION`:此参数显示服务器的版本号。
   - `SERVER_ENCODING`:此参数显示服务器端字符集编码。
   - `LC_COLLATE`:此参数显示数据库的归类区域设置（文本排序）。
   - `LC_CTYPE`:此参数显示数据库的字符分类区域设置。
      `IS_SUPERUSER`:此参数显示当前角色是否具有超级用户权限。
- `ALL`:通过说明显示所有配置参数的值。

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

`COPY`命令将任何`SELECT`查询的输出转储到指定位置。 用户必须具有访问此位置的权限，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

**参数**

- `query`:要复制的查询。
- `format_name`:要复制查询的格式。`format_name`可以是`parquet`、`csv`或`json`之一。 默认情况下，该值为`parquet`。

>[!NOTE]
>
>完整的输出路径将为`adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE

使用`ALTER TABLE`命令可以添加或删除主键约束或外键约束，以及向表中添加列。

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
>表模式应是唯一的，并且不在多个表之间共享。 此外，对于主键约束，命名空间是必填项。

#### 添加列

以下SQL查询显示了向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

**参数**

- `table_name`:要编辑的表的名称。
- `column_name`:要添加的列的名称。
- `data_type`:要添加的列的数据类型。支持的数据类型包括：bigint、char、string、date、datetime、多次、多次精度、整数、smallint、tinyint、varchar。

### 显示主键

`SHOW PRIMARY KEYS`命令列表给定数据库的所有主键约束。

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

`SHOW FOREIGN KEYS`命令列表给定数据库的所有外键约束。

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
