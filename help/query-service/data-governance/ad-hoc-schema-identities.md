---
title: 在临时数据集中设置主要身份
description: Adobe Experience Platform查询服务允许您直接通过SQL ALTER TABLE命令为临时模式数据集字段设置标识或主标识。 本文档说明如何使用ALTER TABLE命令设置主标识或辅助标识。
exl-id: b8e6b87e-c6e5-4688-a936-a3a1510a3c5b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 在临时数据集中设置主身份

Adobe Experience Platform查询服务允许您使用SQL `ALTER TABLE`命令的约束将数据集列标记为主要或辅助标识。 您可以使用此功能确保标记的字段符合数据隐私要求。 此命令允许您直接通过SQL添加或删除主标识表列和辅助标识表列的约束。

## 快速入门

将数据集列标记为主标识或辅助标识需要了解`ALTER TABLE` SQL命令并充分了解数据隐私要求。 在继续阅读本文档之前，请查看以下文档：

* [ `ALTER TABLE`命令的SQL语法指南](../sql/syntax.md)。
* [数据管理概述](../../data-governance/home.md)，以了解更多信息。

## 添加约束 {#add-constraints}

`ALTER TABLE`命令允许您为数据集列添加标签作为人员标识，然后使用SQL更新关联的元数据以将该标签用作主标识。 当通过SQL而不是通过Experience Platform UI直接从架构创建数据集时，这尤其有用。 命令可用于确保Experience Platform中的数据操作符合数据使用策略。

**示例**

以下示例向现有`t1`表添加约束。 `id`列的值现在标记为`IDFA`命名空间下的主标识。 身份命名空间是一个关键字，用于声明字段表示的身份数据类型。

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
```

第二个示例确保`id`列被标记为辅助标识。

```sql
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

## 删除约束 {#drop-constraints}

还可以使用`ALTER TABLE`命令从表列中删除约束。

**示例**

以下示例删除了在现有`t1`表中将`c1`列标记为主标识的要求。

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
```

如下所示，在删除标识约束时，会使用相同的语法。

```sql
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

## 显示身份

使用命令行界面中的元数据命令`show identities`显示具有指定为标识的每个属性的表。

```shell
> show identities;
```

下面显示了返回表的示例。

```console
 tableName | columnName | datatype | namespace | ifPrimary
-----------+------------+----------+-----------+----------
(0 rows)
```

## XDM限制 {#limitations}

以下列表说明了使用XDM时更新现有数据集中的身份的重要注意事项。

* 要将列指定为标识，您&#x200B;**必须**&#x200B;同时定义要保留为该列的元数据的命名空间。
* XDM不支持在namespace属性中指定列名称。
* 如果您的架构使用`identityMap` XDM字段，根或顶级`identityMap`对象&#x200B;**必须**&#x200B;标记为身份或主身份。
