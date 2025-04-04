---
title: 查询服务中数据资产组织的最佳实践
description: 本文档概述整理数据以通过查询服务轻松使用的逻辑方法。
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# 在查询服务中组织数据资产

本文档提供了整理数据资产（包括数据集、视图和临时表）以用于Adobe Experience Platform查询服务的最佳实践指南。 它涵盖了如何构建数据以及如何访问、更新和删除此信息的信息。

随着数据资源的增长，在Experience Platform [!DNL Data Lake]中对数据进行逻辑组织非常重要。 查询服务扩展了SQL构造，使您能够按逻辑对沙盒中的数据资产进行分组。 这种组织方法允许在架构之间共享数据资产，而无需在物理上移动它们。

## 快速入门

在继续阅读本文档之前，您应该对[查询服务](../home.md)的功能有了很好的了解，并且已经阅读了[用户界面指南](../ui/user-guide.md)。

## 在查询服务中组织数据

以下示例演示了通过Adobe Experience Platform查询服务可以使用的结构，这些结构使用标准SQL语法从逻辑上组织数据。 您应该从创建数据库开始，以充当数据点的容器。 数据库可以包含一个或多个架构，每个架构随后可以具有一个或多个对数据资产（数据集、视图、临时表等）的引用。 这些引用包括数据集之间的任何关系或关联。

有关如何使用查询服务UI创建SQL查询的详细指导，请参阅[查询编辑器用户指南](../ui/user-guide.md)。

支持以下用于在沙盒中逻辑组织数据集的SQL构造。

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

该示例（为简短起见，略微截断）演示了`databaseA`包含架构`schema1`的此方法。

## 将数据资产关联到架构

创建模式以充当数据资产的容器后，可以使用标准SQL ALTER TABLE语法将每个数据集与数据库中的一个或多个模式相关联。

以下示例将`dataset1`、`dataset2`、`dataset3`和`v1`添加到在上一个示例中创建的`databaseA.schema1`容器中。

```SQL
ALTER TABLE dataset1 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 ADD SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 ADD SCHEMA databaseA.schema1;
 
ALTER VIEW v1  ADD SCHEMA databaseA.schema1;
```

## 从数据容器访问数据资产

通过适当限定数据库名称，任何[!DNL PostgreSQL]客户端都可以连接到您使用SHOW关键字创建的任何数据结构。 有关SHOW关键字的详细信息，请参阅SQL语法文档](../sql/syntax.md#show)中的[SHOW部分。

“all”是默认数据库名称，其中包含沙盒中的每个数据库和架构容器。 当您使用`dbname="all"`建立[!DNL PostgreSQL]连接时，您可以访问已创建的&#x200B;**任何**&#x200B;数据库和架构以从逻辑上组织数据。

列出`dbname="all"`下的所有数据库将显示三个可用数据库。

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

在`dbname="all"`下列出所有架构，将显示与沙盒中每个数据库相关的三个架构。

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

当您使用`dbname="databaseA"`建立[!DNL PostgreSQL]连接时，您可以访问与该特定数据库关联的任何架构，如下面的示例所示。

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

点表示法允许您访问与连接到所选数据库的特定架构关联的每个表。 通过连接到`DBNAME = databaseA.schema1;`，将显示与该特定架构(`schema1`)关联的所有表。 这提供了有关哪个数据集包含哪个表的信息。

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

随着组织（或沙盒）中数据资产量的增长，有必要更新数据容器或从数据容器中删除数据资产。 通过使用点表示法引用相应的数据库和架构名称，可以从组织容器中删除单个资产。 第一个示例中添加到`databaseA.schema1`的表和视图（`t1`和`v1`）将使用以下示例中的语法删除。

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 删除数据资产

仅当[DROP TABLE](../sql/syntax.md#drop-table)函数在组织中的所有数据库中存在对该表的单个引用时，才会从[!DNL Data Lake]中实际删除数据资产。

```sql
DROP TABLE databaseA.schema2.t1;
```

### 删除数据资产容器

也可以使用标准SQL函数删除数据库和模式。

#### 删除数据库

如果存在其他对与该数据库关联的数据资产的引用，则该函数在尝试删除数据库时将引发错误。

```sql
DROP DATABASE databaseA;
```

#### 删除架构

删除架构时，需要注意三个重要注意事项：

- 删除架构并不会实际删除任何数据资产，例如表、视图或临时表。
- 如果目标架构中引用了任何数据资产，并且模式为RESTRICT，则会引发异常。
- 如果存在目标架构中引用的任何数据资产，并且模式为CASCADE，则系统会删除架构容器引用的所有数据资产，然后删除架构容器。

```sql
DROP SCHEMA databaseA.schema2;
```

## 后续步骤

通过阅读本文档，您现在可以更好地了解有关用于Adobe Experience Platform查询服务的数据资产的组织和结构的最佳实践。 建议通过阅读关于[重复数据删除文档](../key-concepts/deduplication.md)来继续了解查询服务的最佳实践。
