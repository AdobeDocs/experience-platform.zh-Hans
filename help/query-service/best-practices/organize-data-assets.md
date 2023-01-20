---
title: 查询服务中数据资产组织的最佳实践
description: 本文档概述了组织数据以便于查询服务使用的逻辑方法。
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 在查询服务中组织数据资产

本文档提供了有关组织数据资产（包括数据集、视图和临时表）以与Adobe Experience Platform查询服务一起使用的最佳实践指导。 它涵盖如何构建数据以及有关如何访问、更新和删除此信息的信息。

在平台内对数据资产进行逻辑组织非常重要 [!DNL Data Lake] 随着它们的生长。 查询服务扩展了SQL结构，使您能够在沙盒中对数据资产进行逻辑分组。 这种组织方法允许在架构之间共享数据资产，而无需实际移动它们。

## 快速入门

在继续阅读本文档之前，您应该对 [查询服务](../home.md) 功能和已阅读 [用户界面指南](../ui/user-guide.md).

## 在查询服务中组织数据

以下示例演示了通过Adobe Experience Platform查询服务可用于使用标准SQL语法对数据进行逻辑组织的结构。 您应该首先创建一个数据库，以用作数据点的容器。 数据库可以包含一个或多个架构，然后每个架构可以具有对数据资产（数据集、视图、临时表等）的一个或多个引用。 这些引用包括数据集之间的任何关系或关联。

请参阅 [查询编辑器用户指南](../ui/user-guide.md) 有关如何使用查询服务UI创建SQL查询的详细指南。

支持以下SQL结构，用于对沙盒中的数据集进行逻辑组织。

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

示例（因为简短而略有截断）演示了此方法，其中 `databaseA` 包含架构 `schema1`.

## 将数据资产关联到架构

创建架构以充当数据资产的容器后，每个数据集都可以使用标准SQL ALTER TABLE语法与数据库中的一个或多个架构相关联。

以下示例添加了 `dataset1`, `dataset2`, `dataset3` 和 `v1` 到 `databaseA.schema1` 容器。

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## 从数据容器访问数据资产

通过适当限定数据库名称， [!DNL PostgreSQL] 客户端可以连接到您使用SHOW关键字创建的任何数据结构。 有关SHOW关键词的详细信息，请参阅 [SQL语法文档中的SHOW部分](../sql/syntax.md#show).

“all”是默认的数据库名称，其中包含沙盒中的每个数据库和架构容器。 当你 [!DNL PostgreSQL] 连接使用 `dbname="all"`，您可以访问 **any** 数据库和已创建的架构，用于对数据进行逻辑组织。

列出 `dbname="all"` 显示三个可用数据库。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

列出 `dbname="all"` 显示与沙盒中的每个数据库相关的三个架构。

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

当你 [!DNL PostgreSQL] 连接使用 `dbname="databaseA"`，则可以访问与该特定数据库关联的任何架构，如以下示例所示。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

点表示法允许您访问与连接到所选数据库的特定架构关联的每个表。 通过连接到 `DBNAME = databaseA.schema1;`，与特定架构(`schema1`)。 这提供了有关哪个数据集包含哪个表的信息。

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## 从数据容器更新或删除数据资产

随着IMS组织（或沙盒）中的数据资产数量增加，有必要从数据容器更新或删除数据资产。 可通过使用点表示法引用相应的数据库和架构名称，从组织容器中删除单个资产。 表和视图(`t1` 和 `v1` ) `databaseA.schema1` 在第一个示例中，使用以下示例中的语法删除。

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 删除数据资产

的 [拖放表](../sql/syntax.md#drop-table) 函数仅从实际中删除数据资产 [!DNL Data Lake] 当IMS组织中的所有数据库之间存在对表的单个引用时。

```sql
DROP TABLE databaseA.schema2.t1;
```

### 删除数据资产容器

数据库和模式也可以使用标准SQL函数删除。

#### 删除数据库

如果对与数据库关联的数据资产有其他引用，则函数在尝试删除数据库时将引发错误。

```sql
DROP DATABASE databaseA;
```

#### 删除架构

删除架构时，需注意以下三个重要注意事项：

- 删除架构不会实际删除任何数据资产，如表、视图或临时表。
- 如果目标架构中引用了任何数据资产，且模式为RESTRICT，则会引发异常。
- 如果目标架构中引用了任何数据资产，并且模式为CASCADE，则系统将删除架构容器引用的所有数据资产，然后删除架构容器。

```sql
DROP SCHEMA databaseA.schema2;
```

## 后续步骤

通过阅读本文档，您现在可以更好地了解有关数据资产的组织和结构的最佳实践，以便与Adobe Experience Platform查询服务结合使用。 建议通过阅读 [数据删除文档](../essential-concepts/deduplication.md).
