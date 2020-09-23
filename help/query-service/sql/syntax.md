---
keywords: Experience Platform;home;popular topics;query service;Query service;sql syntax;sql;ctas;CTAS;Create table as select
solution: Experience Platform
title: SQL语法
topic: syntax
description: 此文档显示查询服务支持的SQL语法。
translation-type: tm+mt
source-git-commit: 2672d0bdf1f34deb715415e7b660a35076edb06b
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 1%

---


# SQL语法

[!DNL Query Service] 提供对语句和其他有限命令使 `SELECT` 用标准ANSI SQL的能力。 此文档显示支持的SQL语 [!DNL Query Service]法。

## 定义SELECT查询

以下语法定义 `SELECT` 支持的查询 [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

其中 `from_item` 可以是：

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

并 `grouping_element` 且可以是：

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

是 `with_query` :

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE子句

可以使用关键字ILIKE代替LIKE对SELECT查询不区分大小写的WHERE子句进行匹配。

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE和ILIKE子句的逻辑如下：
- ```WHERE condition LIKE pattern```, ```~~``` 等效于图案
- ```WHERE condition NOT LIKE pattern```, ```!~~``` 等效于图案
- ```WHERE condition ILIKE pattern```，等 ```~~*``` 效于图案
- ```WHERE condition NOT ILIKE pattern```，等 ```!~~*``` 效于图案


#### 示例

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

返回名称以“A”或“a”开头的客户。

## 连接

使用 `SELECT` 联接的查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## 合并、INTERSECT和EXCEPT

支持 `UNION`以下 `INTERSECT`、和子 `EXCEPT` 句来组合或排除两个或多个表中类似的行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 按选择创建表

以下语法定义 `CREATE TABLE AS SELECT` 支持的(CTAS)查询 [!DNL Query Service]:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

其中`target_schema_title` ，是XDM模式的标题。 仅当您希望对由CTAS模式创建的新数据集使用现有XDM查询时`rowvalidation` ，才使用此子句指定用户是否希望对为创建的新数据集摄取的每个新批次进行行级别验证。 默认值为“false”

和 `select_query` 是一 `SELECT` 个语句，其语法在此文档中定义。


### 示例

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

请注意，对于给定的CTAS查询:

1. 语句 `SELECT` 必须具有聚合函数的别名， `COUNT`如 `SUM`、、 `MIN`等等。
2. 语 `SELECT` 句可以带括号()，也可以不带括号()。

## 插入

以下语法定义 `INSERT INTO` 支持的查询 [!DNL Query Service]:

```sql
INSERT INTO table_name select_query
```

其中 `select_query` 是 `SELECT` 一个语句，其语法在此文档中定义。

### 示例

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

请注意，对于给定的插入查询:

1. 语 `SELECT` 句MUST NOT be incroined in parenthes()。
2. 语句结果的模式 `SELECT` 必须与语句中定义的表的 `INSERT INTO` 一致。

### 删除表

如果表不是EXTERNAL表，则从文件系统中删除与表关联的目录。 如果要删除的表不存在，则会发生异常。

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 参数

- `IF EXISTS`:如果表不存在，则不会发生任何情况
- `TEMP`:临时表

## 创建视图

以下语法定义 `CREATE VIEW` 支持的查询 [!DNL Query Service]:

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

其 `view_name` 中是要创建的视图的名 `select_query` 称， `SELECT` 是语句，其语法在此文档中定义。

示例：

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP视图

以下语法定义 `DROP VIEW` 支持的查询 [!DNL Query Service]:

```sql
DROP VIEW [IF EXISTS] view_name
```

其 `view_name` 中是要删除的视图的名称

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

要返回任何设置的值，请使用 `SHOW [setting name]`。

## PostgreSQL命令

### 开始

将解析此命令并将完成的命令发送回客户端。 这与命令相 `START TRANSACTION` 同。

```sql
BEGIN [ TRANSACTION ]
```

#### 参数

- `TRANSACTION`:可选关键字。 监听它，不会对此执行任何操作。

### 关闭

`CLOSE` 释放与打开的游标关联的资源。 关闭光标后，不允许对其执行后续操作。 当不再需要光标时，应关闭它。

```sql
CLOSE { name }
```

#### 参数

- `name`:要关闭的打开游标的名称。

### 提交

不执行任何操 [!DNL Query Service] 作作为对commit事务语句的响应。

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### 参数

- `WORK`
- `TRANSACTION`:可选关键字。 它们没有作用。

### 取消分配

使用 `DEALLOCATE` 取消分配以前准备的SQL语句。 如果不显式取消分配准备语句，则会在会话结束时取消分配该语句。

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 参数

- `Prepare`:忽略此关键字。
- `name`:要取消分配的已准备语句的名称。
- `ALL`:取消分配所有准备的语句。

### DECLARE

`DECLARE` 允许用户创建游标，该游标可用于在较大查询中一次检索少量行。 创建游标后，使用从它获取行 `FETCH`。

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 参数

- `name`:要创建的光标的名称。
- `WITH HOLD`:指定在创建游标的事务成功提交后，游标可以继续使用。
- `query`:提 `SELECT` 供游 `VALUES` 标要返回的行的或命令。

### 执行

`EXECUTE` 用于执行先前准备的语句。 由于预准备语句仅存在于会话的持续时间中，所以预准备语句必须是由在当前会话之前 `PREPARE` 执行的语句创建的。

如果创 `PREPARE` 建语句的语句指定了一些参数，则必须向该语句传递一组兼容的 `EXECUTE` 参数，否则会引发错误。 请注意，预准备语句（与函数不同）不会根据其参数的类型或数量而过载。 准备语句的名称在数据库会话中必须是唯一的。

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 参数

- `name`:要执行的准备语句的名称。
- `parameter`:准备语句的参数的实际值。 这必须是一个表达式，其生成的值与此参数的数据类型兼容，这取决于创建预准备语句时确定的值。

### 说明

此命令显示PostgreSQL计划程序为提供的语句生成的执行计划。 执行计划显示如何通过简单顺序扫描、索引扫描等扫描语句所引用的表；如果引用了多个表，则使用哪些连接算法将每个输入表中所需的行相结合。

显示的最关键部分是估计的语句执行成本，这是计划员对运行语句需要多长时间的猜测（以任意但通常平均磁盘页读取的成本单位衡量）。 实际上，显示了两个数字：返回第一行之前的开始成本，以及返回所有行的总成本。 对于大多数查询，总成本是重要的，但在上下文（如EXISTS中的子查询）中，计划员选择最小的开始增加成本而不是最小的总成本（因为执行器在获得一行后停止）。 此外，如果限制返回行数并带有子句，计划 `LIMIT` 员会在端点成本之间进行适当的插值，以估计哪个计划真的最便宜。

该选 `ANALYZE` 项会导致执行语句，而不仅是计划语句。 然后，将实际运行时间统计信息添加到显示中，包括每个计划节点内花费的总已用时间（以毫秒为单位）以及它返回的总行数。 这有助于了解规划者的估计是否接近现实。

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 参数

- `ANALYZE`:执行命令并显示实际运行时间和其他统计信息。 此参数默认为 `FALSE`。
- `FORMAT`:指定输出格式，可以是TEXT、XML、JSON或YAML。 非文本输出包含的信息与文本输出格式相同，但对项目来说更容易进行分析。 此参数默认为 `TEXT`。
- `statement`:任何 `SELECT`、、 `INSERT`、 `UPDATE`、、 `DELETE`或您想 `VALUES`要查看的 `EXECUTE``DECLARE``CREATE TABLE AS``CREATE MATERIALIZED VIEW AS` 、、、或者说明的执行计划。

>[!IMPORTANT]
>
>请记住，使用该选项时，语句会 `ANALYZE` 实际执行。 尽管 `EXPLAIN` 放弃返回的任何输 `SELECT` 出，但语句的其他副作用仍如常发生。

#### 示例

要在表上显示简单查询的计划(单列 `integer` 和10000行):

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 提取

`FETCH` 使用先前创建的游标检索行。

光标具有关联的位置，该位置由使用 `FETCH`。 光标位置可以位于查询结果的第一行之前、结果的任何特定行上或结果的最后一行之后。 创建时，光标将放在第一行之前。 读取某些行后，光标将位于最近检索到的行上。 如 `FETCH` 果在可用行的末尾处运行，则光标将保留在最后一行之后。 如果没有这样的行，则返回空结果，并根据需要将光标放在第一行之前或最后一行之后。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 参数

- `num_of_rows`:可能带符号的整数常数，用于确定要提取的行的位置或数目。
- `cursor_name`:打开的光标的名称。

### 准备

`PREPARE` 创建预准备语句。 预准备语句是服务器端对象，可用于优化性能。 执行该 `PREPARE` 语句时，将分析、分析和重写指定的语句。 当随后发 `EXECUTE` 出命令时，计划并执行所准备的语句。 这种分工避免了重复的分析分析工作，同时允许执行计划依赖于提供的特定参数值。

预准备的语句可以采用参数，即执行语句时替换到语句中的值。 创建准备语句时，请按位置使用$1、$2等参数。 可以选择地指定参数列表类型的对应。 当参数的数据类型未指定或声明为未知时，类型会根据首次引用参数的上下文推断（如果可能）。 执行语句时，在语句中指定这些参数的实际 `EXECUTE` 值。

准备的语句仅在当前数据库会话的持续时间内持续。 当会话结束时，会忘记准备的语句，因此必须重新创建它才能再次使用。 这也意味着单个准备语句不能被多个同时的数据库客户端使用。 但是，每个客户端都可以创建自己准备好的语句来使用。 可以使用命令手动清除准备的 `DEALLOCATE` 语句。

当使用单个会话执行大量类似语句时，准备语句可能具有最大的性能优势。 如果语句在规划或重写方面很复杂，例如，查询涉及多个表的连接或需要应用多个规则，则性能差异尤其显着。 如果语句的规划和重写相对简单，但执行起来相对昂贵，则预准备语句的性能优势就不那么明显。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 参数

- `name`:为此特定准备语句指定的任意名称。 它在单个会话中必须是唯一的，并且随后用于执行或取消分配先前准备的语句。
- `data-type`:准备语句的参数的数据类型。 如果特定参数的数据类型未指定或指定为未知，则从首次引用该参数的上下文推断该数据类型。 要引用准备语句本身中的参数，请使用$1、$2等。


### 回滚

`ROLLBACK` 回退当前事务，并导致丢弃该事务所做的所有更新。

```sql
ROLLBACK [ WORK ]
```

#### 参数

- `WORK`

### 选择范围

`SELECT INTO` 创建新表，并用查询计算的数据填充它。 数据不会像正常情况一样返回到客户端 `SELECT`。 新表的列具有与输出列关联的名称和数据类型 `SELECT`。

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

新建一个仅 `films_recent` 包含表中最近条目的表 `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

`SHOW` 显示运行时参数的当前设置。 这些变量可以使用语 `SET` 句进行设置，方法是编辑postgresql.conf配置文件，通过环境变量 `PGOPTIONS` （使用libpq或基于libpq的应用程序时），或者通过命令行标记启动postgres服务器。

```sql
SHOW name
```

#### 参数

- `name`：
   - `SERVER_VERSION`:显示服务器的版本号。
   - `SERVER_ENCODING`:显示服务器端字符集编码。 目前，可以显示此参数，但不能设置此参数，因为编码是在创建数据库时确定的。
   - `LC_COLLATE`:显示数据库的归类区域设置（文本排序）。 目前，可以显示此参数，但不能设置，因为设置是在创建数据库时确定的。
   - `LC_CTYPE`:显示数据库的字符分类区域设置。 目前，可以显示此参数，但不能设置，因为设置是在创建数据库时确定的。
      `IS_SUPERUSER`:如果当前角色具有超级用户权限，则为true。
- `ALL`:通过说明显示所有配置参数的值。

#### 示例

显示参数的当前设置 `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 开始事务

将解析此命令并将完成的命令发送回客户端。 这与命令相 `BEGIN` 同。

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
>完整的输出路径将 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`