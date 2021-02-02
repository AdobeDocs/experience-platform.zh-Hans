---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；sql语法；sql;ctas;CTAS；创建表作为选择
solution: Experience Platform
title: SQL语法
topic: syntax
description: 此文档显示查询服务支持的SQL语法。
translation-type: tm+mt
source-git-commit: 14cb1d304fd8aad2ca287f8d66ac6865425db4c5
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 0%

---


# SQL语法

[!DNL Query Service] 提供对语句和其他有限命令使 `SELECT` 用标准ANSI SQL的能力。此文档显示[!DNL Query Service]支持的SQL语法。

## 定义SELECT查询

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

其中，`from_item`可以是以下任一项：

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

和`grouping_element`可以是以下任一项：

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

和`with_query`为：

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### SNAPSHOT子句

此子句可用于根据快照id以增量方式读取表上的数据。 快照id是每次向数据表写入数据时，数据表上由“长”类型的数字标识的检查点标记。 SNAPSHOT子句将其自身附加到它旁边使用的表关系。

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 示例

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

请注意，SNAPSHOT子句可以与表或表别名一起使用，但不能在子查询或视图上。 SNAPHOST子句在可以应用表上的SELECT查询的任何位置都能工作。

### WHERE ILIKE子句

可以使用关键字ILIKE代替LIKE对SELECT查询不区分大小写的WHERE子句进行匹配。

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE和ILIKE子句的逻辑如下：
- ```WHERE condition LIKE pattern```, ```~~``` 等效于图案
- ```WHERE condition NOT LIKE pattern```, ```!~~``` 等效于图案
- ```WHERE condition ILIKE pattern```, ```~~*``` 等效于图案
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` 等效于图案


#### 示例

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

返回名称以“A”或“a”开头的客户。

## 连接

使用连接的`SELECT`查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## 合并、INTERSECT和EXCEPT

支持`UNION`、`INTERSECT`和`EXCEPT`子句，以组合或排除两个或多个表中类似的行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 按选择创建表

以下语法定义[!DNL Query Service]支持的`CREATE TABLE AS SELECT`(CTAS)查询:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

其中，
`target_schema_title`是XDM模式的标题。 仅当您希望对由CTAS模式创建的新数据集使用现有XDM查询时，才使用此子句
`rowvalidation`指定用户是否希望对为创建的新数据集摄取的每个新批进行行级别验证。 默认值为“true”

并且`select_query`是`SELECT`语句，其语法在此文档中定义。


### 示例

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

请注意，对于给定的CTAS查询:

1. `SELECT`语句必须具有聚合函数的别名，如`COUNT`、`SUM`、`MIN`等。
2. `SELECT`语句可以带括号()，也可以不带括号()。
3. `SELECT`语句可以提供SNAPSHOT子句以将增量增量增量增量读入目标表。

```sql
CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

## 插入

以下语法定义[!DNL Query Service]支持的`INSERT INTO`查询:

```sql
INSERT INTO table_name select_query
```

其中`select_query`是`SELECT`语句，其语法在此文档中定义。

### 示例

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

请注意，对于给定的插入查询:

1. `SELECT`语句不能括在括号()中。
2. `SELECT`语句结果的模式必须与`INSERT INTO`语句中定义的表符合。
3. `SELECT`语句可以提供SNAPSHOT子句以将增量增量增量增量读入目标表。

```sql
INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

### 删除表

如果表不是EXTERNAL表，则从文件系统中删除与表关联的目录。 如果要删除的表不存在，则会发生异常。

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 参数

- `IF EXISTS`:如果表不存在，则不会发生任何情况
- `TEMP`:临时表

## 创建视图

以下语法定义[!DNL Query Service]支持的`CREATE VIEW`查询:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

其中`view_name`是要创建的视图的名称
并且`select_query`是`SELECT`语句，其语法在此文档中定义。

示例：

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP视图

以下语法定义[!DNL Query Service]支持的`DROP VIEW`查询:

```sql
DROP VIEW [IF EXISTS] view_name
```

其中`view_name`是要删除的视图的名称

示例：

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL命令

### 设置

设置属性、返回现有属性的值或列表所有现有属性。 如果为现有属性键提供了值，则旧值将被覆盖。

```sql
SET property_key [ To | =] property_value
```

要返回任何设置的值，请使用`SHOW [setting name]`。

## PostgreSQL命令

### 开始

将解析此命令并将完成的命令发送回客户端。 这与`START TRANSACTION`命令相同。

```sql
BEGIN [ TRANSACTION ]
```

#### 参数

- `TRANSACTION`:可选关键字。监听它，不会对此执行任何操作。

### 关闭

`CLOSE` 释放与打开的游标关联的资源。关闭光标后，不允许对其执行后续操作。 当不再需要光标时，应关闭它。

```sql
CLOSE { name }
```

#### 参数

- `name`:要关闭的打开游标的名称。

### 提交

在[!DNL Query Service]中不会执行任何操作作为对commit事务语句的响应。

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### 参数

- `WORK`
- `TRANSACTION`:可选关键字。它们没有作用。

### 取消分配

使用`DEALLOCATE`取消分配先前准备的SQL语句。 如果不显式取消分配准备语句，则会在会话结束时取消分配该语句。

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 参数

- `Prepare`:忽略此关键字。
- `name`:要取消分配的已准备语句的名称。
- `ALL`:取消分配所有准备的语句。

### DECLARE

`DECLARE` 允许用户创建游标，该游标可用于在较大查询中一次检索少量行。创建游标后，使用`FETCH`从游标读取行。

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 参数

- `name`:要创建的光标的名称。
- `WITH HOLD`:指定在创建游标的事务成功提交后，游标可以继续使用。
- `query`:提供 `SELECT` 游 `VALUES` 标要返回的行的或命令。

### 执行

`EXECUTE` 用于执行先前准备的语句。由于预准备语句仅存在于会话的持续时间，因此预准备语句必须由在当前会话之前执行的`PREPARE`语句创建。

如果创建该语句的`PREPARE`语句指定了一些参数，则必须向`EXECUTE`语句传递一组兼容的参数，否则将引发错误。 请注意，预准备语句（与函数不同）不会根据其参数的类型或数量而过载。 准备语句的名称在数据库会话中必须是唯一的。

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 参数

- `name`:要执行的准备语句的名称。
- `parameter`:准备语句的参数的实际值。这必须是一个表达式，其生成的值与此参数的数据类型兼容，这取决于创建预准备语句时确定的值。

### 说明

此命令显示PostgreSQL计划程序为提供的语句生成的执行计划。 执行计划显示如何通过简单顺序扫描、索引扫描等扫描语句所引用的表；如果引用了多个表，则使用哪些连接算法将每个输入表中所需的行相结合。

显示的最关键部分是估计的语句执行成本，这是计划员对运行语句需要多长时间的猜测（以任意但通常平均磁盘页读取的成本单位衡量）。 实际上，显示了两个数字：返回第一行之前的开始成本，以及返回所有行的总成本。 对于大多数查询，总成本是重要的，但在上下文（如EXISTS中的子查询）中，计划员选择最小的开始增加成本而不是最小的总成本（因为执行器在获得一行后停止）。 此外，如果使用`LIMIT`子句限制返回的行数，计划员会在端点成本之间进行适当的插值，以估计哪个计划真的最便宜。

`ANALYZE`选项导致语句被执行，而不仅是计划语句。 然后，将实际运行时间统计信息添加到显示中，包括每个计划节点内花费的总已用时间（以毫秒为单位）以及它返回的总行数。 这有助于了解规划者的估计是否接近现实。

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 参数

- `ANALYZE`:执行命令并显示实际运行时间和其他统计信息。此参数默认为`FALSE`。
- `FORMAT`:指定输出格式，可以是TEXT、XML、JSON或YAML。非文本输出包含的信息与文本输出格式相同，但对项目来说更容易进行分析。 此参数默认为`TEXT`。
- `statement`:任何 `SELECT`、、 `INSERT`、 `UPDATE`、、 `DELETE`或您想要 `VALUES`看到的 `EXECUTE` `DECLARE` `CREATE TABLE AS` `CREATE MATERIALIZED VIEW AS` 、、、或者的执行计划。

>[!IMPORTANT]
>
>请记住，使用`ANALYZE`选项时，语句实际会执行。 尽管`EXPLAIN`会丢弃`SELECT`返回的任何输出，但语句的其他副作用会如常发生。

#### 示例

要在表上显示具有单个`integer`列和10000行的简单查询的计划：

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 提取

`FETCH` 使用先前创建的游标检索行。

光标具有关联的位置，由`FETCH`使用。 光标位置可以位于查询结果的第一行之前、结果的任何特定行上或结果的最后一行之后。 创建时，光标将放在第一行之前。 读取某些行后，光标将位于最近检索到的行上。 如果`FETCH`在可用行的末尾处运行，则光标将保留在最后一行之后。 如果没有这样的行，则返回空结果，并根据需要将光标放在第一行之前或最后一行之后。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 参数

- `num_of_rows`:可能带符号的整数常数，用于确定要提取的行的位置或数目。
- `cursor_name`:打开的光标的名称。

### 准备

`PREPARE` 创建预准备语句。预准备语句是服务器端对象，可用于优化性能。 执行`PREPARE`语句时，将分析、分析和重写指定的语句。 随后发出`EXECUTE`命令时，将计划并执行准备的语句。 这种分工避免了重复的分析分析工作，同时允许执行计划依赖于提供的特定参数值。

预准备的语句可以采用参数，即执行语句时替换到语句中的值。 创建准备语句时，请按位置使用$1、$2等参数。 可以选择地指定参数列表类型的对应。 当参数的数据类型未指定或声明为未知时，类型会根据首次引用参数的上下文推断（如果可能）。 执行语句时，在`EXECUTE`语句中指定这些参数的实际值。

准备的语句仅在当前数据库会话的持续时间内持续。 当会话结束时，会忘记准备的语句，因此必须重新创建它才能再次使用。 这也意味着单个准备语句不能被多个同时的数据库客户端使用。 但是，每个客户端都可以创建自己准备好的语句来使用。 可以使用`DEALLOCATE`命令手动清除准备的语句。

当使用单个会话执行大量类似语句时，准备语句可能具有最大的性能优势。 如果语句在规划或重写方面很复杂，例如，查询涉及多个表的连接或需要应用多个规则，则性能差异尤其显着。 如果语句的规划和重写相对简单，但执行起来相对昂贵，则预准备语句的性能优势就不那么明显。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 参数

- `name`:为此特定准备语句指定的任意名称。它在单个会话中必须是唯一的，并且随后用于执行或取消分配先前准备的语句。
- `data-type`:准备语句的参数的数据类型。如果特定参数的数据类型未指定或指定为未知，则从首次引用该参数的上下文推断该数据类型。 要引用准备语句本身中的参数，请使用$1、$2等。


### 回滚

`ROLLBACK` 回退当前事务，并导致丢弃该事务所做的所有更新。

```sql
ROLLBACK [ WORK ]
```

#### 参数

- `WORK`

### 选择范围

`SELECT INTO` 创建新表，并用查询计算的数据填充它。数据不会返回给客户端，因为它与普通`SELECT`数据一样。 新表的列具有与`SELECT`的输出列关联的名称和数据类型。

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

#### 参数

- `TEMPORARAY` 或 `TEMP`:如果指定，则将表创建为临时表。
- `UNLOGGED:` 如果指定，则表将创建为未记录的表。
- `new_table` 要创建的表的名称(可选模式限定)。

#### 示例

新建一个表`films_recent`，其中只包含表`films`中最近的条目：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

`SHOW` 显示运行时参数的当前设置。这些变量可以使用`SET`语句、通过`PGOPTIONS`环境变量（使用libpq或基于libpq的应用程序时）编辑postgresql.conf配置文件或通过命令行标志来设置。

```sql
SHOW name
```

#### 参数

- `name`：
   - `SERVER_VERSION`:显示服务器的版本号。
   - `SERVER_ENCODING`:显示服务器端字符集编码。目前，可以显示此参数，但不能设置此参数，因为编码是在创建数据库时确定的。
   - `LC_COLLATE`:显示数据库的归类区域设置（文本排序）。目前，可以显示此参数，但不能设置，因为设置是在创建数据库时确定的。
   - `LC_CTYPE`:显示数据库的字符分类区域设置。目前，可以显示此参数，但不能设置，因为设置是在创建数据库时确定的。
      `IS_SUPERUSER`:如果当前角色具有超级用户权限，则为true。
- `ALL`:通过说明显示所有配置参数的值。

#### 示例

显示参数`DateStyle`的当前设置

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 开始事务

将解析此命令并将完成的命令发送回客户端。 这与`BEGIN`命令相同。

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### 复制

此命令将任何SELECT查询的输出转储到指定位置。 用户必须具有访问此位置的权限，此命令才能成功。

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>完整的输出路径将为`adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`


### ALTER

此命令有助于向表添加或删除主键或外键约束。

```sql
Alter TABLE table_name ADD CONSTRAINT Primary key ( column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name ( primary_column_name )

Alter TABLE table_name ADD CONSTRAINT Foreign key ( column_name ) references referenced_table_name Namespace 'namespace'

Alter TABLE table_name DROP CONSTRAINT Primary key ( column_name )

Alter TABLE table_name DROP CONSTRAINT  Foreign key ( column_name )
```

>[!NOTE]
>表模式应是唯一的，并且不在多个表之间共享。 此外，命名空间是强制的。


### 显示主键

此命令列表给定数据库的所有主键约束。

```sql
SHOW PRIMARY KEYS
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```


### 显示外键

此命令列表给定数据库的所有外键约束。

```sql
SHOW FOREIGN KEYS
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
