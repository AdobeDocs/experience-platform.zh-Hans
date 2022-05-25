---
title: 在临时数据集中设置主标识
description: Adobe Experience Platform查询服务允许您直接通过SQL ALTER TABLE命令为临时架构数据集字段设置标识或主标识。 本文档介绍如何使用ALTER TABLE命令设置主标识或次标识。
source-git-commit: bf51fc3e0c9635c0555f87f3389fb4a9542c092d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# 在临时数据集中设置主标识

Adobe Experience Platform查询服务允许您使用SQL的约束将数据集列标记为主标识或次标识 `ALTER TABLE` 命令。 您可以使用此功能确保标记的字段符合数据隐私要求。 此命令允许您直接通过SQL添加或删除主标识表列和次标识表列的约束。

## 快速入门

为数据集列设置主标识或次标识标签需要了解 `ALTER TABLE` SQL命令，并且对数据隐私要求有很好的了解。 在继续阅读本文档之前，请查阅以下文档：

* [的SQL语法指南 `ALTER TABLE` 命令](../sql/syntax.md).
* [数据管理概述](../../data-governance/home.md) 以了解更多信息。

## 添加约束 {#add-constraints}

的 `ALTER TABLE` 命令允许您将数据集列标记为人员身份，然后使用该标签作为主标识，方法是使用SQL更新关联的元数据。 当数据集是通过SQL创建的，而不是直接通过Platform UI从架构创建时，这一点特别有用。 该命令可用于确保您的平台中的数据操作符合数据使用策略。

**示例**

以下示例向现有 `t1` 表。 的值 `id` 列现在标记为主标识 `IDFA` 命名空间。 标识命名空间是用于声明字段表示的身份数据类型的关键字。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

第二个示例确保 `id` 列被标记为辅助标识。

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 放置约束 {#drop-constraints}

还可以使用 `ALTER TABLE` 命令。

**示例**

以下示例消除了 `c1` 列被标记为现有 `t1` 表。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

如下所示，删除身份约束时使用的语法相同。

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## 显示身份

使用元数据命令 `show identities` 从命令行界面显示一个表，其中每个属性都被指定为标识。

```shell
> show identities;
```

返回表的示例如下所示。

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM限制 {#limitations}

以下列表介绍了在使用XDM时更新现有数据集中标识的重要注意事项。

* 要将列指定为标识，您需要 **必须** 还定义要保留为列元数据的命名空间。
* XDM不支持在命名空间属性中指定列名称。
* 如果您的架构使用 `identityMap` XDM字段、根或顶级 `identityMap` 对象 **必须** 标记为身份或主身份。
