---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；SQL语法；SQL；CTAS；CTAS；创建表作为选择
solution: Experience Platform
title: 查询服务中的SQL语法
description: 本文档详细介绍并说明Adobe Experience Platform查询服务支持的SQL语法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: cd4734b2d837bc04e1de015771a74a48ff37173f
workflow-type: tm+mt
source-wordcount: '4686'
ht-degree: 1%

---

# 查询服务中的SQL语法

您可以在Adobe Experience Platform查询服务中为`SELECT`语句和其他有限命令使用标准ANSI SQL。 本文档介绍[!DNL Query Service]支持的SQL语法。

## 选择查询 {#select-queries}

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

下面的选项卡部分提供了FROM、GROUP和WITH关键字的可用选项。

>[!BEGINTABS]

>[!TAB `from_item`]

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

>[!TAB `grouping_element`]

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

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

以下小节提供了可在查询中使用的附加子句的详细信息，前提是它们遵循上述格式。

### SNAPSHOT子句

此子句可用于基于快照ID增量读取表中的数据。 快照ID是由Long-type数字表示的检查点标记，每次将数据写入到快照ID时，该数字都会应用于数据湖表。 `SNAPSHOT`子句将其自身附加到它旁边使用的表关系上。

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 示例

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN 'HEAD' AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND 'TAIL';

SELECT * FROM (SELECT id FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id) C;

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

>[!NOTE]
>
>在`SNAPSHOT`子句中使用`HEAD`或`TAIL`时，必须用单引号将它们括起来(例如，“HEAD”、“TAIL”)。 使用不带引号的这些变量会导致语法错误。

下表说明了SNAPSHOT子句中每个语法选项的含义。

| 语法 | 含义 |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | 从指定的快照ID （排除）开始读取数据。 |
| `AS OF end_snapshot_id` | 以指定的快照ID（包括）读取数据。 |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | 读取指定的开始快照ID和结束快照ID之间的数据。 它不包括`start_snapshot_id`且包括`end_snapshot_id`。 |
| `BETWEEN HEAD AND start_snapshot_id` | 将数据从开头（第一个快照之前）读取到指定的启动快照ID（包括）。 请注意，这仅返回`start_snapshot_id`中的行。 |
| `BETWEEN end_snapshot_id AND TAIL` | 从指定的`end_snapshot_id`之后将数据读取到数据集结尾（不包括快照ID）。 这意味着，如果`end_snapshot_id`是数据集中的最后一个快照，则查询将返回零行，因为除了最后一个快照之外，没有任何快照。 |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | 从`table_to_be_queried`中读取从指定的快照ID开始的数据，并将其与来自`table_to_be_joined`的数据联接，因为它位于`your_chosen_snapshot_id`。 该连接基于来自要连接的两个表的ID列的匹配ID。 |

`SNAPSHOT`子句与表或表别名一起使用，但不能在子查询或视图的顶部。 `SNAPSHOT`子句适用于对表应用`SELECT`查询的任何位置。

此外，还可以使用`HEAD`和`TAIL`作为快照子句的特殊偏移值。 使用`HEAD`是指第一个快照之前的偏移量，而`TAIL`是指最后一个快照之后的偏移量。

>[!NOTE]
>
>如果在两个快照ID之间进行查询，如果启动快照已过期且设置了可选的回退行为标志(`resolve_fallback_snapshot_on_failure`)，则可能会出现以下两种情况：
>
>- 如果设置了可选的回退行为标志，查询服务会选择最早可用的快照，将其设置为开始快照，并返回最早可用快照与指定结束快照之间的数据。 此数据是&#x200B;**包含最早可用快照的**。

### WHERE子句

默认情况下，`SELECT`查询上的`WHERE`子句生成的匹配项区分大小写。 如果您希望匹配项不区分大小写，则可以使用关键字`ILIKE`而不是`LIKE`。

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

使用联接的`SELECT`查询具有以下语法：

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### UNION、INTERSECT和EXCEPT

`UNION`、`INTERSECT`和`EXCEPT`子句用于组合或排除两个或多个表中的类似行：

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 创建表作为选择 {#create-table-as-select}

使用`CREATE TABLE AS SELECT` (CTAS)命令将`SELECT`查询的结果实体化为新表。 这有助于在模型中使用特征工程数据之前创建转换的数据集、执行聚合或预览特征工程数据。

如果您已准备好使用转换的功能训练模型，请参阅[模型文档](../advanced-statistics/models.md)以了解有关将`CREATE MODEL`与`TRANSFORM`子句结合使用的指导。

您可以选择包含`TRANSFORM`子句以直接在CTAS语句中应用一个或多个功能工程函数。 使用`TRANSFORM`在模型训练之前检查转换逻辑的结果。

此语法适用于永久表和临时表。

```sql
CREATE TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

```sql
CREATE TEMP TABLE table_name 
  [WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE')] 
  [TRANSFORM (transformFunctionExpression1, transformFunctionExpression2, ...)]
AS (select_query)
```

| 参数 | 描述 |
| ----- | ----- |
| `schema` | XDM架构的标题。 仅当您希望将新表与现有XDM架构关联时，才使用此子句。 |
| `rowvalidation` | （可选）为摄取到数据集的每个批次启用行级验证。 默认值为true。 |
| `label` | （可选）使用值`PROFILE`将数据集标记为已启用配置文件摄取。 |
| `transform` | （可选）在具体化数据集之前应用特征工程转换（如字符串索引、单热编码或TF-IDF）。 此子句用于预览转换后的特征。 有关详细信息，请参阅[`TRANSFORM`子句文档](#transform)。 |
| `select_query` | 定义数据集的标准`SELECT`语句。 有关详细信息，请参阅[`SELECT`查询部分](#select-queries)。 |

>[!NOTE]
>
>`SELECT`语句必须包含聚合函数（如`COUNT`、`SUM`或`MIN`）的别名。 您可以提供`SELECT`查询，无论是否带有圆括号。 无论是否使用`TRANSFORM`子句，均适用。

**示例**

使用`TRANSFORM`子句预览一些工程功能的基本示例：

```sql
CREATE TABLE ctas_transform_table_vp14 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments
)
AS SELECT * FROM movie_review_e2e_DND;
```

更高级的示例，其中包含多个转换步骤：

```sql
CREATE TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

临时表示例：

```sql
CREATE TEMP TABLE ctas_transform_table 
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) as ohe_add_comments,
  tokenizer(comments) as token_comments,
  stop_words_remover(token_comments, array('and','very','much')) stp_token,
  ngram(stp_token, 3) ngram_token,
  tf_idf(ngram_token, 20) ngram_idf,
  count_vectorizer(stp_token, 13) cnt_vec_comments,
  tf_idf(token_comments, 10, 1) as cmts_idf
)
AS SELECT * FROM movie_review;
```

#### 限制和行为 {#limitations-and-behavior}

在将`TRANSFORM`子句与`CREATE TABLE`或`CREATE TEMP TABLE`一起使用时，请记住以下限制：

- 如果有任何变换函数生成矢量输出，则它会自动转换为数组。
- 因此，使用`TRANSFORM`创建的表不能直接在`CREATE MODEL`语句中使用。 必须在模型创建期间重新定义转换逻辑，以生成相应的特征向量。
- 转换仅在表创建期间应用。 插入到具有`INSERT INTO`的表中的新数据是&#x200B;**未自动转换**。 要将转换应用到新数据，必须使用带有`TRANSFORM`子句的`CREATE TABLE AS SELECT`重新创建表。
- 此方法旨在预览和验证某个时间点的转换，而不是构建可重用的转换管道。

>[!NOTE]
>
>有关可用转换函数及其输出类型的更多详细信息，请参阅[功能转换输出数据类型](../advanced-statistics/feature-transformation.md#available-transformations)。


### TRANSFORM子句 {#transform}

使用`TRANSFORM`子句在模型训练或表创建之前将一个或多个功能工程函数应用到数据集。 此子句允许您预览、验证或定义输入特征的确切形状。

`TRANSFORM`子句可用于以下语句：

- `CREATE MODEL`
- `CREATE TABLE`
- `CREATE TEMP TABLE`

有关使用CREATE MODEL的详细说明，包括如何定义转换、设置模型选项和配置训练数据，请参阅[模型文档](../advanced-statistics/models.md)。

有关`CREATE TABLE`的使用情况，请参阅[CREATE TABLE AS SELECT部分](#create-table-as-select)。

#### 创建模型示例

```sql
CREATE MODEL review_model
TRANSFORM(
  String_Indexer(additional_comments) si_add_comments,
  one_hot_encoder(si_add_comments) AS ohe_add_comments,
  tokenizer(comments) AS token_comments,
  stop_words_remover(token_comments, array('and','very','much')) AS stp_token,
  ngram(stp_token, 3) AS ngram_token,
  tf_idf(ngram_token, 20) AS ngram_idf,
  count_vectorizer(stp_token, 13) AS cnt_vec_comments,
  tf_idf(token_comments, 10, 1) AS cmts_idf,
  vector_assembler(array(cmts_idf, viewsgot, ohe_add_comments, ngram_idf, cnt_vec_comments)) AS features
)
OPTIONS(MODEL_TYPE='logistic_reg', LABEL='reviews')
AS SELECT * FROM movie_review_e2e_DND;
```

#### 限制 {#limitations}

以下限制适用于将`TRANSFORM`与`CREATE TABLE`一起使用的情况。 请参阅`CREATE TABLE AS SELECT`限制和行为部分，详细解释如何存储转换后的数据、如何处理矢量输出以及为什么无法在模型训练工作流中直接重用结果。

- 矢量输出自动转换为数组，不能直接在`CREATE MODEL`中使用。
- 转换逻辑不会作为元数据保留，并且无法跨批次重用。

## 插入到

`INSERT INTO`命令的定义如下：

>[!IMPORTANT]
>
>查询服务支持使用ITAS引擎的&#x200B;**仅附加操作**。 `INSERT INTO`是唯一受支持的数据操作命令，**更新**&#x200B;和&#x200B;**删除**&#x200B;操作不可用。 要反映数据中的更改，请插入表示所需状态的新记录。

```sql
INSERT INTO table_name select_query
```

| 参数 | 描述 |
| ----- | ----- |
| `table_name` | 要插入查询的表的名称。 |
| `select_query` | `SELECT`语句。 `SELECT`查询的语法可在[SELECT查询节](#select-queries)中找到。 |

**示例**

>[!NOTE]
>
>以下是一个精心设计的示例，仅供参考。

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>请&#x200B;**不**&#x200B;将`SELECT`语句括在圆括号()中。 此外，`SELECT`语句结果的架构必须符合`INSERT INTO`语句中定义的表的架构。 您可以提供`SNAPSHOT`子句以将增量增量增量增量读入目标表。

在根级别未找到实际XDM架构中的大多数字段，并且SQL不允许使用点表示法。 要使用嵌套字段获得逼真的结果，您必须映射`INSERT INTO`路径中的每个字段。

要`INSERT INTO`嵌套路径，请使用以下语法：

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

## 删除表

`DROP TABLE`命令删除现有的表，如果它不是外部表，则从文件系统中删除与该表关联的目录。 如果该表不存在，则会发生异常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则在表&#x200B;**不**&#x200B;存在时不会引发异常。 |

## 创建数据库

`CREATE DATABASE`命令创建Azure Data Lake Storage (ADLS)数据库。

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 删除数据库

`DROP DATABASE`命令从实例中删除数据库。

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则在数据库&#x200B;**不**&#x200B;存在时不会引发异常。 |

## 删除架构

`DROP SCHEMA`命令删除现有架构。

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此参数且架构&#x200B;**不**&#x200B;存在，则不会引发异常。 |
| `RESTRICT` | 模式的默认值。 如果指定，则仅当架构&#x200B;**不**&#x200B;包含任何表时才会丢弃。 |
| `CASCADE` | 如果指定，将删除该架构以及该架构中存在的所有表。 |

## 创建视图 {#create-view}

SQL视图是基于SQL语句的结果集的虚拟表。 使用`CREATE VIEW`语句创建视图并为其命名。 然后，您可以使用该名称来引用回查询的结果。 这使得重复使用复杂的查询更加容易。

以下语法为数据集定义了`CREATE VIEW`查询。 此数据集可以是ADLS或加速存储数据集。

```sql
CREATE VIEW view_name AS select_query
```

| 参数 | 描述 |
| ------ | ------ |
| `view_name` | 要创建的视图的名称。 |
| `select_query` | `SELECT`语句。 `SELECT`查询的语法可在[SELECT查询节](#select-queries)中找到。 |

**示例**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

以下语法定义了在数据库和架构的上下文中创建视图的`CREATE VIEW`查询。

**示例**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| 参数 | 描述 |
| ------ | ------ |
| `db_name` | 数据库的名称。 |
| `schema_name` | 架构的名称。 |
| `view_name` | 要创建的视图的名称。 |
| `select_query` | `SELECT`语句。 `SELECT`查询的语法可在[SELECT查询节](#select-queries)中找到。 |

**示例**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## 显示视图

以下查询显示视图列表。

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## 放置视图

以下语法定义了`DROP VIEW`查询：

```sql
DROP VIEW [IF EXISTS] view_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则当视图&#x200B;**不**&#x200B;存在时，不会引发异常。 |
| `view_name` | 要删除的视图的名称。 |

**示例**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 匿名块 {#anonymous-block}

匿名块由两部分组成：可执行部分和异常处理部分。 在匿名块中，可执行部分是必需的。 但是，“例外处理”部分是可选的。

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

### 匿名块中的条件语句 {#conditional-anonymous-block-statements}

当条件被评估为TRUE时，IF-THEN-ELSE控制结构允许有条件地执行语句列表。 此控制结构仅适用于匿名块。 如果此结构用作独立命令，则会导致语法错误（“匿名块外部的命令无效”）。

下面的代码段演示了匿名块中IF-THEN-ELSE条件语句的正确格式。

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**示例**

以下示例执行`SELECT 200;`。

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

此结构可与`raise_error();`一起使用以返回自定义错误消息。 下面所示的代码块使用“自定义错误消息”终止匿名块。

**示例**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### 嵌套IF语句

匿名块中支持嵌套的IF语句。

**示例**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### 异常块

匿名块中支持异常块。

**示例**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHER THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### 自动转换为JSON {#auto-to-json}

查询服务支持可选会话级别设置，以便从JSON字符串形式的交互式SELECT查询返回顶级复杂字段。 `auto_to_json`设置允许将复杂字段中的数据作为JSON返回，然后使用标准库解析为JSON对象。

在执行包含复杂字段的SELECT查询之前，将功能标志`auto_to_json`设置为true。

```sql
set auto_to_json=true; 
```

#### 在设置`auto_to_json`标记之前

下表提供了应用`auto_to_json`设置之前的示例查询结果。 这两种方案都使用同一个SELECT查询（如下所示），该查询用于定向具有复杂字段的表。

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

#### 设置`auto_to_json`标志后

下表显示了`auto_to_json`设置与结果数据集在结果中的差异。 这两种方案都使用了相同的SELECT查询。

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### 解决故障时的回退快照 {#resolve-fallback-snapshot-on-failure}

`resolve_fallback_snapshot_on_failure`选项用于解决快照ID过期的问题。

将`resolve_fallback_snapshot_on_failure`选项设置为true以使用以前的快照ID覆盖快照。

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

以下代码行使用元数据中最早可用的`snapshot_id`覆盖`@from_snapshot_id`。

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

随着数据资产的增长，在Adobe Experience Platform数据湖中对它们进行逻辑组织非常重要。 查询服务扩展了SQL构造，使您能够按逻辑对沙盒中的数据资产进行分组。 这种组织方法允许在架构之间共享数据资产，而无需在物理上移动它们。

您可以使用标准SQL语法支持以下SQL结构，以便从逻辑上组织数据。

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

有关查询服务最佳实践的更详细说明，请参阅[数据资产的逻辑组织](../best-practices/organize-data-assets.md)指南。

## 表存在

`table_exists` SQL命令用于确认系统中当前是否存在表。 如果表&#x200B;**确实存在**，则命令返回布尔值： `true`；如果表确实存在&#x200B;**确实不存在**，则返回`false`。

通过在运行语句之前验证表是否存在，`table_exists`功能简化了编写匿名块以涵盖`CREATE`和`INSERT INTO`用例的过程。

以下语法定义`table_exists`命令：

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

## 排队 {#inline}

`inline`函数将结构数组的元素分隔并生成表中的值。 它只能放在`SELECT`列表或`LATERAL VIEW`中。

`inline`函数&#x200B;**不能放在存在其他生成器函数的选择列表中**。

默认情况下，生成的列将命名为“col1”、“col2”等。 如果表达式为`NULL`，则不会生成任何行。

>[!TIP]
>
>可以使用`RENAME`命令重命名列名。

**示例**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

此示例返回以下内容：

```text
1  a Spark SQL
2  b Spark SQL
```

第二个示例进一步演示了`inline`函数的概念和应用。 下图说明了示例的数据模型。

![productListItems的架构图。](../images/sql/productListItems.png)

**示例**

```sql
select inline(productListItems) from source_dataset limit 10;
```

从`source_dataset`中获取的值用于填充目标表。

| SKU | 体验(_E) | 数量 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (“(”(“(A，pass，B，NULL)”)“)”) | 5 | 10.5 |
| product-id-5 | (“(”(“（A，通过， B，NULL）”)”)“) |          |              |
| product-id-2 | (“(”(“(AF， C， D，NULL)”)“)”) | 6 | 40 |
| product-id-4 | (“(”(“(BM，pass， NA，NULL)”)”)”) | 3 | 12 |

## 设置

`SET`命令设置属性，并返回现有属性的值或列出所有现有属性。 如果为现有的属性键提供了值，则会覆盖旧值。

```sql
SET property_key = property_value
```

| 参数 | 描述 |
| ------ | ------ |
| `property_key` | 要列出或更改的属性的名称。 |
| `property_value` | 您希望属性设置为的值。 |

要返回任何设置的值，请使用不带`property_value`的`SET [property key]`。

## [!DNL PostgreSQL]命令

以下子部分介绍了查询服务支持的[!DNL PostgreSQL]命令。

### 分析表 {#analyze-table}

`ANALYZE TABLE`命令对命名表执行分布分析和统计计算。 根据数据集是存储在[加速存储](#compute-statistics-accelerated-store)还是[数据湖](#compute-statistics-data-lake)中，`ANALYZE TABLE`的使用会有所不同。 有关其使用的更多信息，请参阅各自的部分。

#### 加速存储的计算统计信息 {#compute-statistics-accelerated-store}

`ANALYZE TABLE`命令计算加速存储上表的统计信息。 统计信息是在加速存储上给定表的已执行CTAS或ITAS查询中计算的。

**示例**

```sql
ANALYZE TABLE <original_table_name>
```

以下是使用`ANALYZE TABLE`命令后可用的统计计算列表：-

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

#### 计算数据湖上的统计信息 {#compute-statistics-data-lake}

您现在可以使用`COMPUTE STATISTICS` SQL命令计算[!DNL Azure Data Lake Storage] (ADLS)数据集的列级统计信息。 计算整个数据集、数据集子集、所有列或列子集的列统计信息。

`COMPUTE STATISTICS`扩展`ANALYZE TABLE`命令。 但是，加速存储表上不支持`COMPUTE STATISTICS`、`FILTERCONTEXT`和`FOR COLUMNS`命令。 当前，只有ADLS表支持`ANALYZE TABLE`命令的这些扩展。

**示例**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

`FILTER CONTEXT`命令根据提供的筛选条件计算数据集子集的统计信息。 `FOR COLUMNS`命令将目标定位到特定列以供分析。

>[!NOTE]
>
>生成的`Statistics ID`和统计信息只对每个会话有效，不能跨不同的PSQL会话访问。<br><br>限制：<ul><li>数组或映射数据类型不支持生成统计信息</li><li>计算统计信息是&#x200B;**而不是**&#x200B;跨会话持久保留。</li></ul><br><br>选项：<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>默认情况下，标志设置为true。 因此，当请求有关不支持的数据类型的统计信息时，它不会出错但会静默跳过具有不支持的数据类型的字段。<br>要在请求不支持的数据类型上的统计信息时启用错误通知，请使用： `SET skip_stats_for_complex_datatypes = false`。

控制台输出如下所示。

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

然后，可以通过引用`Statistics ID`直接查询计算统计信息。 使用`Statistics ID`或下面示例语句中所示的别名来完整查看输出。 要了解有关此功能的更多信息，请参阅[别名文档](../key-concepts/dataset-statistics.md#alias-name)。

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

使用`SHOW STATISTICS`命令显示会话中生成的所有临时统计数据的元数据。 此命令可帮助您优化统计分析的范围。

```sql
SHOW STATISTICS;
```

下面显示了SHOW STATISTICS的输出示例。

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

有关详细信息，请参阅[数据集统计信息文档](../key-concepts/dataset-statistics.md)。

#### 表示例 {#tablesample}

Adobe Experience Platform查询服务提供了示例数据集，作为其近似查询处理功能的一部分。

当不需要对数据集进行聚合操作的确切答案时，最好使用数据集示例。 若要通过发出近似查询以返回近似答案来对大型数据集执行更有效的探索性查询，请使用`TABLESAMPLE`功能。

使用来自现有[!DNL Azure Data Lake Storage] (ADLS)数据集的统一随机样本创建样本数据集，仅使用来自原始数据集的记录百分比。 数据集示例功能使用`TABLESAMPLE`和`SAMPLERATE` SQL命令扩展`ANALYZE TABLE`命令。

在下面的示例中，第一行演示如何计算表格的5%样本。 第二行演示如何从表中数据的过滤视图中计算5%的样本。

**示例**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

有关详细信息，请参阅[数据集示例文档](../key-concepts/dataset-samples.md)。

### 开始

`BEGIN`命令，或者`BEGIN WORK`或`BEGIN TRANSACTION`命令启动事务块。 在给出显式的COMMIT或ROLLBACK命令之前，在开始命令之后输入的任何语句都将在单个事务中执行。 此命令与`START TRANSACTION`相同。

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 关闭

`CLOSE`命令释放与打开游标关联的资源。 游标关闭后，不允许对其执行任何后续操作。 当不再需要游标时，应将其关闭。

```sql
CLOSE name
CLOSE ALL
```

如果使用`CLOSE name`，则`name`表示必须关闭的打开游标的名称。 如果使用`CLOSE ALL`，则将关闭所有打开的游标。

### 取消分配

要取消分配以前准备的SQL语句，请使用`DEALLOCATE`命令。 如果未显式取消分配预准备语句，则该语句将在会话结束时取消分配。 有关预准备语句的详细信息，请参阅[PREPARE命令](#prepare)部分。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果使用`DEALLOCATE name`，则`name`表示必须取消分配的准备语句的名称。 如果使用`DEALLOCATE ALL`，则会取消分配所有准备语句。

### 声明

`DECLARE`命令允许用户创建游标，该游标可用于从较大的查询中检索少量行。 创建游标后，将使用`FETCH`从中获取行。

```sql
DECLARE name CURSOR FOR query
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要创建的游标的名称。 |
| `query` | 提供游标要返回的行的`SELECT`或`VALUES`命令。 |

### 执行

`EXECUTE`命令用于执行以前准备的语句。 由于预准备语句仅存在于会话期间，因此预准备语句必须由在当前会话中较早执行的`PREPARE`语句创建。 有关使用预准备语句的详细信息，请参阅[`PREPARE`命令](#prepare)部分。

如果创建该语句的`PREPARE`语句指定了某些参数，则必须将一组兼容的参数传递到`EXECUTE`语句。 如果未传入这些参数，则会引发错误。

```sql
EXECUTE name [ ( parameter ) ]
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要执行的预准备语句的名称。 |
| `parameter` | 准备语句的参数实际值。 这必须是生成与此参数的数据类型兼容的值的表达式，该值在创建预准备语句时确定。 如果预准备语句有多个参数，则用逗号分隔。 |

### 说明

`EXPLAIN`命令显示所提供语句的执行计划。 执行计划显示了如何扫描语句引用的表。 如果引用了多个表，它会显示使用哪些联接算法将每个输入表中的所需行组合在一起。

```sql
EXPLAIN statement
```

要定义响应的格式，请使用`FORMAT`关键字和`EXPLAIN`命令。

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| 参数 | 描述 |
| ------ | ------ |
| `FORMAT` | 使用`FORMAT`命令指定输出格式。 可用选项为`TEXT`或`JSON`。 非文本输出包含的信息与文本输出格式相同，但程序更容易解析。 此参数默认为`TEXT`。 |
| `statement` | 要查看其执行计划的任何`SELECT`、`INSERT`、`UPDATE`、`DELETE`、`VALUES`、`EXECUTE`、`DECLARE`、`CREATE TABLE AS`或`CREATE MATERIALIZED VIEW AS`语句。 |

>[!IMPORTANT]
>
>使用`EXPLAIN`关键字运行时，`SELECT`语句可能返回的任何输出都将被丢弃。 这一声明的其他副作用照常发生。

**示例**

以下示例显示了对具有单个`integer`列和10000行的表进行简单查询的计划：

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

`FETCH`命令使用以前创建的游标检索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 参数 | 描述 |
| ------ | ------ |
| `num_of_rows` | 要提取的行数。 |
| `cursor_name` | 从中检索信息的游标的名称。 |

### 准备 {#prepare}

使用`PREPARE`命令可以创建预准备语句。 预准备语句是服务器端对象，可用于对类似的SQL语句进行模板化。

预准备语句可以接受参数，这些参数是在执行语句时替换到该语句中的值。 在使用预准备语句时，参数由位置引用，使用$1、$2等。

或者，您可以指定参数数据类型的列表。 如果未列出参数的数据类型，则可以从上下文推断该类型。

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 预准备语句的名称。 |
| `data_type` | 预准备语句参数的数据类型。 如果未列出参数的数据类型，则可以从上下文推断该类型。 如果必须添加多个数据类型，则可以将其添加到以逗号分隔的列表中。 |

### 回滚

`ROLLBACK`命令撤消当前事务并放弃该事务进行的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 选择范围

`SELECT INTO`命令创建一个新表，并用查询计算的数据填充该表。 数据不会返回到客户端，因为它使用的是普通`SELECT`命令。 新表的列具有与`SELECT`命令的输出列关联的名称和数据类型。

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

有关标准SELECT查询参数的详细信息，请参阅[SELECT查询节](#select-queries)。 此部分仅列出`SELECT INTO`命令独有的参数。

| 参数 | 描述 |
| ------ | ------ |
| `TEMPORARY`或`TEMP` | 可选参数。 如果指定了参数，则创建的表为临时表。 |
| `UNLOGGED` | 可选参数。 如果指定了参数，则创建的表是未记录的表。 有关未记录表的详细信息可在[[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/current/sql-createtable.html)中找到。 |
| `new_table` | 要创建的表的名称。 |

**示例**

以下查询创建新的表`films_recent`，其中仅包含表`films`中的最近条目：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

`SHOW`命令显示运行时参数的当前设置。 可以使用`SET`语句、通过编辑`postgresql.conf`配置文件来设置这些变量、通过`PGOPTIONS`环境变量（在使用libpq或基于libpq的应用程序时）或通过命令行标志（在启动Postgres服务器时）来设置这些变量。

```sql
SHOW name
SHOW ALL
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 您希望了解其信息的运行时参数的名称。 运行时参数的可能值包括以下值： <br>`SERVER_VERSION`：此参数显示服务器的版本号。<br>`SERVER_ENCODING`：此参数显示服务器端字符集编码。<br>`LC_COLLATE`：此参数显示用于归类（文本排序）的数据库区域设置。<br>`LC_CTYPE`：此参数显示数据库的字符分类区域设置。<br>`IS_SUPERUSER`：此参数显示当前角色是否具有超级用户权限。 |
| `ALL` | 显示所有配置参数的值及其说明。 |

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

`COPY`命令将任何`SELECT`查询的输出复制到指定位置。 用户必须具有此位置的访问权限，此命令才能成功。

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 参数 | 描述 |
| ------ | ------ |
| `query` | 要复制的查询。 |
| `format_name` | 您希望在其中复制查询的格式。 `format_name`可以是`parquet`、`csv`或`json`之一。 默认情况下，值为`parquet`。 |

>[!NOTE]
>
>完整的输出路径为`adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### 更改表 {#alter-table}

使用`ALTER TABLE`命令可以添加或删除主键或外键约束，并向表中添加列。

#### 添加或删除约束

以下SQL查询显示了向表添加或删除约束的示例。 可使用逗号分隔值将主键和外键约束添加到多个列中。 您可以通过传递两个或多个列名称值来创建组合键，如下面的示例所示。

**定义主键或复合键**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**根据一个或多个键定义表之间的关系**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**定义标识列**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**删除约束/关系/标识**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

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
>表架构应该是唯一的，并且不在多个表之间共享。 此外，对于主键、主标识和标识约束，命名空间是必需的。

#### 添加或删除主标识和辅助标识

要添加或删除主标识表和辅助标识表列的约束，请使用`ALTER TABLE`命令。

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

有关更多详细信息，请参阅有关[在临时数据集](../data-governance/ad-hoc-schema-identities.md)中设置标识的文档。

#### 添加列

以下SQL查询显示了向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### 支持的数据类型

下表列出了用于向Azure SQL中具有[!DNL Postgres SQL]、XDM和[!DNL Accelerated Database Recovery] (ADR)的表添加列的接受数据类型。

| — | PSQL客户端 | XDM | ADR | 描述 |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | 一种数值数据类型，用于存储从 — 9,223,372,036,854,775,807到9,223,372,036,854,775,807之间的大整数，以8字节为单位。 |
| 2 | `integer` | `int4` | `integer` | 用于存储 — 2,147,483,648到2,147,483,647 （以4字节为单位）的整数的数字数据类型。 |
| 3 | `smallint` | `int2` | `smallint` | 用于存储–32,768到215-1 32,767之间的整数（以2字节为单位）的数字数据类型。 |
| 4 | `tinyint` | `int1` | `tinyint` | 用于存储0到255之间的整数（以1字节为单位）的数字数据类型。 |
| 5 | `varchar(len)` | `string` | `varchar(len)` | 可变大小的字符数据类型。 当列数据项的大小差别很大时，最好使用`varchar`。 |
| 6 | `double` | `float8` | `double precision` | `FLOAT8`和`FLOAT`是`DOUBLE PRECISION`的有效同义词。 `double precision`是浮点数据类型。 浮点值以8字节为单位存储。 |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8`是`double precision`的有效同义词。`double precision`是浮点数据类型。 浮点值以8字节为单位存储。 |
| 8 | `date` | `date` | `date` | `date`数据类型是4字节存储的日历日期值，没有任何时间戳信息。 有效日期的范围为01-01-0001到12-31-9999。 |
| 9 | `datetime` | `datetime` | `datetime` | 一种数据类型，用于存储以日历日期和时间表示的时间瞬间。 `datetime`包含限定符：年、月、日、小时、秒和分数。 `datetime`声明可以包括在该序列中连接这些时间单位的任何子集，或者甚至只包括单个时间单位。 |
| 10 | `char(len)` | `string` | `char(len)` | `char(len)`关键字用于指示该项为固定长度字符。 |

#### 添加架构

以下SQL查询显示了向数据库/模式添加表的示例。

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 无法将ADLS表和视图添加到DWH数据库/架构中。


#### 删除架构

以下SQL查询显示了从数据库/模式中删除表的示例。

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

`SHOW PRIMARY KEYS`命令列出给定数据库的所有主键约束。

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

`SHOW FOREIGN KEYS`命令列出了给定数据库的所有外键约束。

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

`SHOW DATAGROUPS`命令返回所有关联数据库的表。 对于每个数据库，该表都包括方案、组类型、子类型、子名称和子ID。

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### 显示表的数据组

`SHOW DATAGROUPS FOR 'table_name'`命令返回包含参数作为其子项的所有关联数据库的表。 对于每个数据库，该表都包括方案、组类型、子类型、子名称和子ID。

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**参数**

- `table_name`：要为其查找关联数据库的表的名称。

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
