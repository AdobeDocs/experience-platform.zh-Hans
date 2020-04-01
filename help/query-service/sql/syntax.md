---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SQL语法
topic: syntax
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# SQL语法

查询服务提供了对语句和其他有限命令使用标 `SELECT` 准ANSI SQL的能力。 此文档显示查询服务支持的SQL语法。

## 定义SELECT查询

以下语法定义了查询服 `SELECT` 务支持的查询:

```
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

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

并 `grouping_element` 且可以是：

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

并且 `with_query` 是：

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE子句

可以使用关键字ILIKE而不是LIKE在SELECT查询的WHERE子句上进行匹配。

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE和ILIKE子句的逻辑如下：
- ```WHERE condition LIKE pattern```, ```~~``` 等效于图案
- ```WHERE condition NOT LIKE pattern```, ```!~~``` 等效于图案
- ```WHERE condition ILIKE pattern```，等 ```~~*``` 效于图案
- ```WHERE condition NOT ILIKE pattern```，等 ```!~~*``` 效于图案


#### 示例

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

返回名称以“A”或“a”开头的客户。

## 加入

使用 `SELECT` 连接的查询具有以下语法：

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## 合并、交叉和除外

支 `UNION`持 `INTERSECT`、 `EXCEPT` 和子句组合或排除两个或多个表中的类似行：

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 按选择创建表

以下语法定义了 `CREATE TABLE AS SELECT` 查询服务支持的(CTAS)查询:

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

其中 `target_schema_title` 是XDM模式的标题。 仅当您希望对由CTAS模式创建的新数据集使用现有XDM查询时，才使用此子句。

and `select_query` 是一 `SELECT` 个语句，其语法在此文档中定义。


### 示例

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

请注意，对于给定的CTAS查询:

1. 该 `SELECT` 语句必须为聚合函数（如、、、等）具 `COUNT`有 `SUM`别名 `MIN`。
2. 该语 `SELECT` 句可以带括号()或不带括号()。

## 插入

以下语法定义了查询服 `INSERT INTO` 务支持的查询:

```
INSERT INTO table_name select_query
```

其中 `select_query` 是一 `SELECT` 个语句，其语法在此文档中定义。

### 示例

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

请注意，对于给定的插入查询:

1. 语 `SELECT` 句MUST NOT be incrounded in parentheses()。
2. 语句结果的模式必 `SELECT` 须与语句中定义的表的一致 `INSERT INTO` 。

### 拖放表

如果表不是EXTERNAL表，则从文件系统中拖放一个表并删除与该表关联的目录。 如果要删除的表不存在，则会发生异常。

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 参数

- `IF EXISTS`:如果表不存在，则不会发生任何情况
- `TEMP`:临时表

## 创建视图

以下语法定义了查询服 `CREATE VIEW` 务支持的查询:

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

其 `view_name` 中是要创建的视图的名称， `select_query` 是 `SELECT` 一个语句，其语法在此文档中定义。

示例：

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### DROP视图

以下语法定义了查询服 `DROP VIEW` 务支持的查询:

```
DROP VIEW [IF EXISTS] view_name
```

其 `view_name` 中是要删除的视图的名称

示例：

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Spark SQL命令

### SET

设置属性、返回现有属性的值或列表所有现有属性。 如果为现有属性键提供了值，则旧值将被覆盖。

```
SET property_key [ To | =] property_value
```

要返回任何设置的值，请使用 `SHOW [setting name]`。

## PostgreSQL命令

### 开始

将解析此命令并将完成的命令发送回客户端。 这与命令相同 `START TRANSACTION` 。

```
BEGIN [ TRANSACTION ]
```

#### 参数

- `TRANSACTION`:可选关键字。 监听它，不会对此执行任何操作。

### 关闭

`CLOSE` 释放与打开的光标关联的资源。 关闭光标后，不允许对其执行后续操作。 当不再需要光标时，应关闭光标。

```
CLOSE { name }
```

#### 参数

- `name`:要关闭的打开的光标的名称。

### 提交

在查询服务中，不会执行任何操作作为对commit事务语句的响应。

```
COMMIT [ WORK | TRANSACTION ]
```

#### 参数

- `WORK`
- `TRANSACTION`:可选关键字。 没有效果。

### 取消分配

使用 `DEALLOCATE` 取消分配以前准备的SQL语句。 如果未明确取消分配准备的语句，则会在会话结束时取消分配该语句。

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 参数

- `Prepare`:忽略此关键字。
- `name`:要取消分配的准备语句的名称。
- `ALL`:取消分配所有准备的语句。

### DECLARE

`DECLARE` 允许用户创建光标，该光标可用于在较大的查询中一次检索少量行。 创建光标后，使用从该光标中获取行 `FETCH`。

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 参数

- `name`:要创建的光标的名称。
- `WITH HOLD`:指定在创建游标的事务成功提交后，可以继续使用游标。
- `query`:提 `SELECT` 供游 `VALUES` 标要返回的行的或命令。

### 执行

`EXECUTE` 用于执行先前准备的语句。 由于准备语句仅在会话期间存在，因此准备语句必须是由在当前会话之前执行 `PREPARE` 的语句创建的。

如果创 `PREPARE` 建语句的语句指定了一些参数，则必须向该语句传递一组兼容的参数，否则 `EXECUTE` 将引发错误。 请注意，预准备的语句（与函数不同）不会根据其参数的类型或数量而过载。 准备语句的名称在数据库会话中必须是唯一的。

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 参数

- `name`:要执行的准备语句的名称。
- `parameter`:准备语句的参数的实际值。 这必须是一个表达式，其生成的值与此参数的数据类型兼容，这是创建准备语句时确定的。

### 说明

此命令显示PostgreSQL计划程序为提供的语句生成的执行计划。 执行计划显示如何扫描由语句引用的表— 通过简单的顺序扫描、索引扫描等方式— 如果引用了多个表，则使用哪些连接算法将每个输入表中所需的行相加。

显示最关键的部分是估计的语句执行成本，这是计划员对运行语句需要多长时间的猜测（以任意但通常平均磁盘页获取的成本单位来衡量）。 实际上，显示了两个数字：可以返回第一行之前的开始成本，以及返回所有行的总成本。 对于大多数查询，总成本是重要的，但在EXISTS中的子查询等上下文中，规划者选择最小的开始成本而不是最小的总成本（因为执行器在获得一行后停止）。 此外，如果限制带有条款的返回行数，则规划者会在端点成本之间做出适当的插值，以估计哪个计划真的最便宜。 `LIMIT`

该选 `ANALYZE` 项导致执行该语句，而不仅是计划语句。 然后，将实际运行时间统计数据添加到显示中，包括每个计划节点内花费的总已用时间（以毫秒为单位）以及它返回的总行数。 这有助于了解规划者的估计是否接近现实。

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 参数

- `ANALYZE`:执行命令并显示实际运行时间和其他统计信息。 此参数默认为 `FALSE`。
- `FORMAT`:指定输出格式，可以是TEXT、XML、JSON或YAML。 非文本输出包含与文本输出格式相同的信息，但对于项目来说，这些信息更易于解析。 此参数默认为 `TEXT`。
- `statement`:任 `SELECT`何、、 `INSERT`、 `UPDATE`或者说明 `DELETE`您想看的 `VALUES``EXECUTE``DECLARE``CREATE TABLE AS``CREATE MATERIALIZED VIEW AS` 、、、或者说明书。

> [!IMPORTANT] 请记住，使用该选项时实际执行 `ANALYZE` 该语句。 尽管 `EXPLAIN` 放弃返回的任何输出， `SELECT` 但该语句的其他副作用仍如常发生。

#### 示例

要在表上显示简单查询的计划(单列和10000 `integer` 行):

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 提取

`FETCH` 使用先前创建的游标检索行。

光标具有关联的位置，该位置由使用 `FETCH`。 光标位置可以位于查询结果的第一行之前、结果的任何特定行上或结果的最后一行之后。 创建时，光标将位于第一行之前。 获取某些行后，光标将位于最近检索到的行上。 如果 `FETCH` 在可用行的末尾之外运行，则光标将保留在最后一行之后。 如果没有这样的行，则返回空结果，并根据需要将光标放在第一行之前或最后一行之后。

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 参数

- `num_of_rows`:可能带符号的整数常数，用于确定要提取的行的位置或数量。
- `cursor_name`:打开光标的名称。

### 准备

`PREPARE` 创建预准备语句。 准备语句是可用于优化性能的服务器端对象。 执行该 `PREPARE` 语句时，将分析、分析和重写指定的语句。 当随后发 `EXECUTE` 出命令时，计划并执行准备的语句。 这种分工避免了重复的解析分析工作，同时允许执行计划依赖于提供的特定参数值。

预准备的语句可以采用执行语句时替换到语句中的参数和值。 创建准备语句时，请使用$1、$2等按位置引用参数。 可以选择地指定相应的列表参数数据类型。 当参数的数据类型未指定或声明为未知时，类型会根据首次引用参数的上下文推断（如果可能）。 执行语句时，在语句中指定这些参数的实际 `EXECUTE` 值。

准备的语句仅在当前数据库会话的持续时间内持续。 当会话结束时，将遗忘准备的语句，因此必须重新创建它才能再次使用。 这也意味着单个准备语句不能被多个同时的数据库客户端使用。 但是，每个客户端都可以创建自己的准备语句以供使用。 可以使用命令手动清除准备的 `DEALLOCATE` 语句。

当使用单个会话执行大量类似语句时，准备的语句可能具有最大的性能优势。 如果语句在规划或重写方面很复杂，例如，如果查询涉及多个表的连接或需要应用多个规则，则性能差异尤其显着。 如果语句的规划和重写相对简单，但执行相对昂贵，则预准备语句的性能优势就不那么明显。

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 参数

- `name`:给予此特定预准备语句的任意名称。 它在单个会话中必须是唯一的，并且随后用于执行或取消分配先前准备的语句。
- `data-type`:准备语句的参数的数据类型。 如果某个特定参数的数据类型未指定或指定为未知，则从首次引用该参数的上下文推断该数据类型。 要引用准备语句本身中的参数，请使用$1、$2等。


### 回滚

`ROLLBACK` 回滚当前事务，并导致丢弃由该事务所做的所有更新。

```
ROLLBACK [ WORK ]
```

#### 参数

- `WORK`

### 选择范围

`SELECT INTO` 创建一个新表，并用查询计算的数据填充该表。 数据不会像正常情况一样返回到客户端 `SELECT`。 新表的列具有与输出列关联的名称和数据类型 `SELECT`。

```
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

- `TEMPORARAY` 或 `TEMP`:如果指定，则表将创建为临时表。
- `UNLOGGED:` 如果指定，则表将创建为未记录的表。
- `new_table` 要创建的表的名称(可选模式限定)。

#### 示例

创建仅包含表 `films_recent` 中最近条目的新表 `films`:

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

`SHOW` 显示运行时参数的当前设置。 这些变量可以使用语句进行设置，方法是编辑postgresql.conf配置文件，通过环境变量（使用libpq或基于libpq的应用程序时）进行设置，或者在启动postgres服务器时通过命令行标志进行设置。 `SET``PGOPTIONS`

```
SHOW name
```

#### 参数

- `name`：
   - `SERVER_VERSION`:显示服务器的版本号。
   - `SERVER_ENCODING`:显示服务器端字符集编码。 目前，该参数可以显示但不能设置，因为编码是在创建数据库时确定的。
   - `LC_COLLATE`:显示数据库的归类区域设置（文本排序）。 目前，可以显示该参数，但不能设置该参数，因为该设置是在创建数据库时确定的。
   - `LC_CTYPE`:显示数据库的字符分类区域设置。 目前，可以显示该参数，但不能设置该参数，因为该设置是在创建数据库时确定的。
      `IS_SUPERUSER`:如果当前角色具有超级用户权限，则为true。
- `ALL`:显示所有配置参数的值及说明。

#### 示例

显示参数的当前设置 `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 开始事务

将解析该命令并将完成的命令发送回客户端。 这与命令相同 `BEGIN` 。

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```
