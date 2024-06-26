---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；SQL语法；SQL；CTAS；CTAS；创建表作为选择
solution: Experience Platform
title: 查询服务中的SQL语法
description: 本文档详细介绍并说明Adobe Experience Platform查询服务支持的SQL语法。
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: d2cb7c3d1968a33300d480e63c4cb007df3cce7b
workflow-type: tm+mt
source-wordcount: '4305'
ht-degree: 2%

---

# 查询服务中的SQL语法

可以将标准ANSI SQL用于 `SELECT` Adobe Experience Platform语句和其他有限的命令。 本文档介绍了支持的SQL语法。 [!DNL Query Service].

## 选择查询 {#select-queries}

以下语法定义 `SELECT` 查询支持方 [!DNL Query Service]：

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

此子句可用于基于快照ID增量读取表中的数据。 快照ID是由Long-type数字表示的检查点标记，每次将数据写入到快照ID时，该数字都会应用于数据湖表。 此 `SNAPSHOT` 子句将其自身附加到它旁边使用的表关系上。

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 示例

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN HEAD AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND TAIL;

SELECT * FROM (SELECT id FROM table_to_be_queried BETWEEN start_snapshot_id AND end_snapshot_id) C 

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

下表说明了SNAPSHOT子句中每个语法选项的含义。

| 语法 | 含义 |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | 从指定的快照ID （排除）开始读取数据。 |
| `AS OF end_snapshot_id` | 以指定的快照ID（包括）读取数据。 |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | 读取指定的开始快照ID和结束快照ID之间的数据。 它不包括 `start_snapshot_id` 并且包括 `end_snapshot_id`. |
| `BETWEEN HEAD AND start_snapshot_id` | 将数据从开头（第一个快照之前）读取到指定的启动快照ID（包括）。 注意，这仅返回以下位置的行： `start_snapshot_id`. |
| `BETWEEN end_snapshot_id AND TAIL` | 在指定的之后读取数据 `end-snapshot_id` 到数据集的结尾（不包括快照ID）。 这意味着，如果 `end_snapshot_id` 是数据集中的最后一个快照，查询将返回零行，因为除了最后一个快照之外，没有任何快照。 |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | 从指定的快照ID开始读取数据 `table_to_be_queried` 并将其与来自以下位置的数据连接： `table_to_be_joined` 原样 `your_chosen_snapshot_id`. 该连接基于来自要连接的两个表的ID列的匹配ID。 |

A `SNAPSHOT` 子句与表或表别名配合使用，但不在子查询或视图的顶部。 A `SNAPSHOT` 子句适用于任何位置 `SELECT` 可对表应用查询。

此外，您可以使用 `HEAD` 和 `TAIL` 作为快照子句的特殊偏移值。 使用 `HEAD` 是指第一个快照之前的偏移，而 `TAIL` 是指上一个快照之后的偏移。

>[!NOTE]
>
>如果在两个快照ID之间进行查询，如果启动快照已过期且可选的回退行为标志(`resolve_fallback_snapshot_on_failure`)设置：
>
>- 如果设置了可选的回退行为标志，查询服务会选择最早可用的快照，将其设置为开始快照，并返回最早可用快照与指定结束快照之间的数据。 此数据为 **包含** 最早的可用快照的日志。

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
| `label` | 使用CTAS查询创建数据集时，请使用此标签和值 `profile` 将您的数据集标记为已为配置文件启用。 这意味着您的数据集会在创建时自动标记为用户档案。 有关使用的更多信息，请参阅派生的属性扩展文档 `label`. |
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询位于 [选择查询部分](#select-queries). |

**示例**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>此 `SELECT` 语句必须具有集合函数的别名，例如 `COUNT`， `SUM`， `MIN`，等等。 此外， `SELECT` 语句可以带有或不带有括号()提供。 您可以提供 `SNAPSHOT` 子句将增量增量增量读入目标表。

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
>以下是一个精心设计的示例，仅供参考。

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>Do **非** 随附 `SELECT` 括号()中的语句。 此外，结果的结构描述还可以 `SELECT` 语句必须符合 `INSERT INTO` 语句。 您可以提供 `SNAPSHOT` 子句将增量增量增量读入目标表。

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

## 删除表

此 `DROP TABLE` 命令删除现有的表，如果它不是外部表，则从文件系统删除与该表关联的目录。 如果该表不存在，则会发生异常。

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则不会引发异常（如果表确实如此） **非** 存在。 |

## 创建数据库

此 `CREATE DATABASE` 命令创建Azure Data Lake Storage (ADLS)数据库。

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
| `IF EXISTS` | 如果指定此参数且架构指定 **非** 存在，不会引发异常。 |
| `RESTRICT` | 模式的默认值。 如果指定，则只有在指定时，架构才会丢弃 **非** 包含任意表。 |
| `CASCADE` | 如果指定，将删除该架构以及该架构中存在的所有表。 |

## 创建视图 {#create-view}

SQL视图是基于SQL语句的结果集的虚拟表。 使用创建视图 `CREATE VIEW` 语句并为其命名。 然后，您可以使用该名称来引用回查询的结果。 这使得重复使用复杂的查询更加容易。

以下语法定义 `CREATE VIEW` 查询数据集。 此数据集可以是ADLS或加速存储数据集。

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

以下语法定义 `CREATE VIEW` 在数据库和模式的上下文中创建视图的查询。

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
| `select_query` | A `SELECT` 语句。 的语法 `SELECT` 查询位于 [选择查询部分](#select-queries). |

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

以下语法定义 `DROP VIEW` 查询：

```sql
DROP VIEW [IF EXISTS] view_name
```

| 参数 | 描述 |
| ------ | ------ |
| `IF EXISTS` | 如果指定此项，则当视图指定此项时，不会引发异常 **非** 存在。 |
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

以下示例执行 `SELECT 200;`.

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

此结构可以与 `raise_error();` 以返回自定义错误消息。 下面所示的代码块使用“自定义错误消息”终止匿名块。

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

查询服务支持可选会话级别设置，以便从JSON字符串形式的交互式SELECT查询返回顶级复杂字段。 此 `auto_to_json` 通过设置，可以将复杂字段中的数据作为JSON返回，然后使用标准库解析为JSON对象。

设置功能标志 `auto_to_json` 设置为true，然后再执行包含复杂字段的SELECT查询。

```sql
set auto_to_json=true; 
```

#### 在设置之前 `auto_to_json` 标志

下表提供了一个示例查询结果，它位于 `auto_to_json` 设置。 这两种方案都使用同一个SELECT查询（如下所示），该查询用于定向具有复杂字段的表。

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

#### 设置 `auto_to_json` 标志

下表显示了结果中的差异， `auto_to_json` 设置对生成的数据集有。 这两种方案都使用了相同的SELECT查询。

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### 解决故障时的回退快照 {#resolve-fallback-snapshot-on-failure}

此 `resolve_fallback_snapshot_on_failure` 选项用于解决快照ID过期的问题。 快照元数据在两天后过期，过期的快照可能会使脚本的逻辑失效。 当使用匿名块时，可能会出现问题。

设置 `resolve_fallback_snapshot_on_failure` 选项为true时，会使用以前的快照ID覆盖快照。

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

以下代码行将覆盖 `@from_snapshot_id` 包含最早可用的 `snapshot_id` 来自元数据。

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

请参阅 [数据资产的逻辑组织](../best-practices/organize-data-assets.md) 指南，以了解有关查询服务最佳实践的更详细说明。

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

## 排队 {#inline}

此 `inline` 函数将结构数组的元素分隔并生成表中的值。 它只能放置在 `SELECT` 列表或 `LATERAL VIEW`.

此 `inline` 函数 **无法** 位于有其他生成器函数的选择列表中。

默认情况下，生成的列将命名为“col1”、“col2”等。 如果表达式为 `NULL` 则不生成行。

>[!TIP]
>
>可使用重命名列名 `RENAME` 命令。

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

| SKU | 体验(_E) | 数量 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (“(”(“(A，pass，B，NULL)”)“)”) | 5 | 10.5 |
| product-id-5 | (“(”(“（A，通过， B，NULL）”)”)“) |          |              |
| product-id-2 | (“(”(“(AF， C， D，NULL)”)“)”) | 6 | 40 |
| product-id-4 | (“(”(“(BM，pass， NA，NULL)”)”)”) | 3 | 12 |

## [!DNL Spark] SQL命令

以下子部分介绍了查询服务支持的Spark SQL命令。

### 设置

此 `SET` command设置一个属性，并返回现有属性的值或列出所有现有属性。 如果为现有的属性键提供了值，则会覆盖旧值。

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

此 `ANALYZE TABLE` 命令对命名表执行分布分析和统计计算。 使用 `ANALYZE TABLE` 根据数据集是否存储在 [加速存储](#compute-statistics-accelerated-store) 或 [数据湖](#compute-statistics-data-lake). 有关其使用的更多信息，请参阅各自的部分。

#### 加速存储的计算统计信息 {#compute-statistics-accelerated-store}

此 `ANALYZE TABLE` 命令计算加速存储上表的统计信息。 统计信息是在加速存储上给定表的已执行CTAS或ITAS查询中计算的。

**示例**

```sql
ANALYZE TABLE <original_table_name>
```

以下是使用 `ANALYZE TABLE` 命令：-

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

您现在可以在以下位置计算列级统计信息 [!DNL Azure Data Lake Storage] (ADLS)数据集与 `COMPUTE STATISTICS` sql命令。 计算整个数据集、数据集子集、所有列或列子集的列统计信息。

`COMPUTE STATISTICS` 扩展 `ANALYZE TABLE` 命令。 但是， `COMPUTE STATISTICS`， `FILTERCONTEXT`、和 `FOR COLUMNS` 加速存储表不支持命令。 的这些扩展 `ANALYZE TABLE` 当前仅支持ADLS表使用命令。

**示例**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

此 `FILTER CONTEXT` 命令根据提供的过滤条件计算数据集子集的统计信息。 此 `FOR COLUMNS` 命令将目标定位到特定的列以供分析。

>[!NOTE]
>
>此 `Statistics ID` 生成的统计信息只对每个会话有效，不能跨不同的PSQL会话访问。<br><br>限制：<ul><li>数组或映射数据类型不支持生成统计信息</li><li>计算的统计信息为 **非** 跨会话保留。</li></ul><br><br>选项：<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>默认情况下，该标记设置为true。 因此，当请求有关不支持的数据类型的统计信息时，它不会出错但会静默跳过具有不支持的数据类型的字段。<br>要在请求有关不受支持数据类型的统计信息时启用错误通知，请使用： `SET skip_stats_for_complex_datatypes = false`.

控制台输出如下所示。

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

然后，您可以通过引用 `Statistics ID`. 使用 `Statistics ID` 或下面示例语句中显示的别名，以查看完整输出。 要了解有关此功能的更多信息，请参阅 [别名文档](../key-concepts/dataset-statistics.md#alias-name).

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

使用 `SHOW STATISTICS` 命令以显示会话中生成的所有临时统计信息的元数据。 此命令可帮助您优化统计分析的范围。

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

请参阅 [数据集统计文档](../key-concepts/dataset-statistics.md) 以了解更多信息。

#### 表示例 {#tablesample}

Adobe Experience Platform查询服务提供了示例数据集，作为其近似查询处理功能的一部分。

当不需要对数据集进行聚合操作的确切答案时，最好使用数据集示例。 要通过发出近似查询以返回近似答案对大型数据集进行更有效的探索性查询，请使用 `TABLESAMPLE` 功能。

使用来自现有样本的均匀随机样本创建样本数据集 [!DNL Azure Data Lake Storage] (ADLS)数据集，仅使用来自原始数据的记录百分比。 数据集示例功能对 `ANALYZE TABLE` 命令和 `TABLESAMPLE` 和 `SAMPLERATE` sql命令。

在下面的示例中，第一行演示如何计算表格的5%样本。 第二行演示如何从表中数据的过滤视图中计算5%的样本。

**示例**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

请参阅 [数据集示例文档](../key-concepts/dataset-samples.md) 以了解更多信息。

### 开始

此 `BEGIN` 命令，或者 `BEGIN WORK` 或 `BEGIN TRANSACTION` 命令，启动事务块。 在给出显式的COMMIT或ROLLBACK命令之前，在开始命令之后输入的任何语句都将在单个事务中执行。 此命令与 `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 关闭

此 `CLOSE` 命令释放与打开的光标相关联的资源。 游标关闭后，不允许对其执行任何后续操作。 当不再需要游标时，应将其关闭。

```sql
CLOSE name
CLOSE ALL
```

如果 `CLOSE name` 已使用， `name` 表示必须关闭的打开游标的名称。 如果 `CLOSE ALL` 使用，将关闭所有打开的游标。

### 取消分配

要取消分配以前准备的SQL语句，请使用 `DEALLOCATE` 命令。 如果未显式取消分配预准备语句，则该语句将在会话结束时取消分配。 有关预准备语句的更多信息，请参见 [PREPARE命令](#prepare) 部分。

```sql
DEALLOCATE name
DEALLOCATE ALL
```

如果 `DEALLOCATE name` 已使用， `name` 表示必须取消分配的准备语句的名称。 如果 `DEALLOCATE ALL` 会使用，所有已准备的报表会被取消分配。

### 声明

此 `DECLARE` 命令允许用户创建游标，该游标可用于从较大的查询中检索少量行。 创建游标后，会使用从其中获取行 `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要创建的游标的名称。 |
| `query` | A `SELECT` 或 `VALUES` 命令提供游标要返回的行。 |

### 执行

此 `EXECUTE` 命令用于执行以前准备的语句。 由于准备的语句仅存在于会话期间，因此准备的语句必须由 `PREPARE` 语句在当前会话中较早执行。 有关使用预准备语句的更多信息，请参见 [`PREPARE` 命令](#prepare) 部分。

如果 `PREPARE` 创建语句的语句指定了某些参数，必须将一组兼容的参数传递给 `EXECUTE` 语句。 如果未传入这些参数，则会引发错误。

```sql
EXECUTE name [ ( parameter ) ]
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 要执行的预准备语句的名称。 |
| `parameter` | 准备语句的参数实际值。 这必须是生成与此参数的数据类型兼容的值的表达式，该值在创建预准备语句时确定。 如果预准备语句有多个参数，则用逗号分隔。 |

### 说明

此 `EXPLAIN` 命令显示提供的语句的执行计划。 执行计划显示了如何扫描语句引用的表。 如果引用了多个表，它会显示使用哪些联接算法将每个输入表中的所需行组合在一起。

```sql
EXPLAIN statement
```

要定义响应的格式，请使用 `FORMAT` 带有的关键字 `EXPLAIN` 命令。

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| 参数 | 描述 |
| ------ | ------ |
| `FORMAT` | 使用 `FORMAT` 命令指定输出格式。 可用的选项包括 `TEXT` 或 `JSON`. 非文本输出包含的信息与文本输出格式相同，但程序更容易解析。 此参数默认为 `TEXT`. |
| `statement` | 任何 `SELECT`， `INSERT`， `UPDATE`， `DELETE`， `VALUES`， `EXECUTE`， `DECLARE`， `CREATE TABLE AS`，或 `CREATE MATERIALIZED VIEW AS` 语句，您希望查看其执行计划。 |

>[!IMPORTANT]
>
>任何输出 `SELECT` 使用运行时，语句可能会返回 `EXPLAIN` 关键字。 这一声明的其他副作用照常发生。

**示例**

以下示例显示了对具有单个表的简单查询的计划 `integer` 列和10000行：

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

此 `FETCH` 命令使用以前创建的游标检索行。

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 参数 | 描述 |
| ------ | ------ |
| `num_of_rows` | 要提取的行数。 |
| `cursor_name` | 从中检索信息的游标的名称。 |

### 准备 {#prepare}

此 `PREPARE` 命令用于创建预准备语句。 预准备语句是服务器端对象，可用于对类似的SQL语句进行模板化。

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

此 `ROLLBACK` 命令撤消当前事务并丢弃该事务进行的所有更新。

```sql
ROLLBACK
ROLLBACK WORK
```

### 选择范围

此 `SELECT INTO` 命令创建一个新表，并使用查询计算的数据填充该表。 数据不会返回到客户端，因为它与常规数据一样 `SELECT` 命令。 新表的列具有与的输出列关联的名称和数据类型 `SELECT` 命令。

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

有关标准SELECT查询参数的更多信息，请参见 [选择查询节](#select-queries). 此部分仅列出以下对象独有的参数： `SELECT INTO` 命令。

| 参数 | 描述 |
| ------ | ------ |
| `TEMPORARY` 或 `TEMP` | 可选参数。 如果指定了参数，则创建的表为临时表。 |
| `UNLOGGED` | 可选参数。 如果指定了参数，则创建的表是未记录的表。 有关未记录表的详细信息，请参见 [[!DNL PostgreSQL] 文档](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | 要创建的表的名称。 |

**示例**

下面的查询创建一个新表 `films_recent` 仅由表中的最近条目组成 `films`：

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 显示

此 `SHOW` 命令显示运行时参数的当前设置。 这些变量可以使用进行设置 `SET` 语句，通过编辑 `postgresql.conf` 配置文件，通过 `PGOPTIONS` 环境变量（在使用libpq或基于libpq的应用程序时），或在启动Postgres服务器时通过命令行标志。

```sql
SHOW name
SHOW ALL
```

| 参数 | 描述 |
| ------ | ------ |
| `name` | 您希望了解其信息的运行时参数的名称。 运行时参数的可能值包括以下值：<br>`SERVER_VERSION`：此参数显示服务器的版本号。<br>`SERVER_ENCODING`：此参数显示服务器端字符集编码。<br>`LC_COLLATE`：此参数显示数据库的归类（文本排序）区域设置。<br>`LC_CTYPE`：此参数显示数据库的字符分类区域设置。<br>`IS_SUPERUSER`：此参数显示当前角色是否具有超级用户权限。 |
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

此 `COPY` 命令复制任何 `SELECT` 查询到指定的位置。 用户必须具有此位置的访问权限，此命令才能成功。

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
>完整的输出路径为 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### 更改表 {#alter-table}

此 `ALTER TABLE` 命令用于添加或删除主键或外键约束，并向表中添加列。

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

**删除约束/关系/身份**

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

要添加或删除主标识表列和辅助标识表列的约束条件，请使用 `ALTER TABLE` 命令。

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

欲知更多详情，请参见 [在临时数据集中设置身份](../data-governance/ad-hoc-schema-identities.md).

#### 添加列

以下SQL查询显示了向表添加列的示例。

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### 支持的数据类型

下表列出了在使用向表中添加列时接受的数据类型 [!DNL Postgres SQL]、 XDM和 [!DNL Accelerated Database Recovery] (ADR)。

| — | PSQL客户端 | XDM | ADR | 描述 |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | 一种数值数据类型，用于存储从 — 9,223,372,036,854,775,807到9,223,372,036,854,775,807之间的大整数，以8字节为单位。 |
| 2 | `integer` | `int4` | `integer` | 用于存储 — 2,147,483,648到2,147,483,647 （以4字节为单位）的整数的数字数据类型。 |
| 3 | `smallint` | `int2` | `smallint` | 用于存储–32,768到215-1 32,767之间的整数（以2字节为单位）的数字数据类型。 |
| 4 | `tinyint` | `int1` | `tinyint` | 用于存储0到255之间的整数（以1字节为单位）的数字数据类型。 |
| 5 | `varchar(len)` | `string` | `varchar(len)` | 可变大小的字符数据类型。 `varchar` 当列数据条目的大小差别很大时，最好使用它。 |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` 和 `FLOAT` 是的有效同义词 `DOUBLE PRECISION`. `double precision` 是浮点数据类型。 浮点值以8字节为单位存储。 |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` 是的有效同义词 `double precision`.`double precision` 是浮点数据类型。 浮点值以8字节为单位存储。 |
| 8 | `date` | `date` | `date` | 此 `date` 数据类型是4字节存储的日历日期值，没有任何时间戳信息。 有效日期的范围为01-01-0001到12-31-9999。 |
| 9 | `datetime` | `datetime` | `datetime` | 一种数据类型，用于存储以日历日期和时间表示的时间瞬间。 `datetime` 包括限定符：年、月、日、小时、秒和分数。 A `datetime` 声明可以包括这些时间单位中在序列中连接任何子集，或者甚至包括单个时间单位。 |
| 10 | `char(len)` | `string` | `char(len)` | 此 `char(len)` 关键字用于指示项目是固定长度的字符。 |

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

此 `SHOW DATAGROUPS` 命令返回所有关联数据库的表。 对于每个数据库，该表都包括方案、组类型、子类型、子名称和子ID。

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

此 `SHOW DATAGROUPS FOR 'table_name'` 命令返回包含参数作为其子项的所有关联数据库的表。 对于每个数据库，该表都包括方案、组类型、子类型、子名称和子ID。

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
