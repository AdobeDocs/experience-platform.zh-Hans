---
title: 派生属性的无缝SQL流
description: 查询服务SQL已扩展，可提供对派生属性的无缝支持。 了解如何使用此SQL扩展创建为配置文件启用的派生属性，以及如何将属性用于Real-time Customer Profile和Segmentation Service。
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: e9c4068419b36da6ffaec67f0d1c39fe87c2bc4c
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# 派生属性的无缝SQL流

查询服务SQL已扩展，可提供对派生属性的无缝支持。 这提供了一种有效的替代方法，可为您的Real-time Customer Profile业务用例创建派生属性。

本文档概述了各种方便的SQL扩展，这些扩展可生成用于实时客户个人资料的派生属性。 该工作流简化了原本必须通过各种API调用或Platform UI交互完成的流程。

通常，生成和发布实时客户个人资料的属性需要以下步骤：

* 创建身份命名空间（如果尚不存在）。
* 如有必要，创建数据类型以存储派生属性。
* 创建具有该数据类型的字段组以存储派生的属性信息。
* 使用之前创建的命名空间创建或分配主标识列。
* 使用之前创建的字段组和数据类型创建架构。
* 使用架构创建新数据集，并根据需要为用户档案启用该数据集。
* 可以选择将数据集标记为已启用配置文件。

完成上述步骤后，即可填充数据集。 如果为用户档案启用了数据集，则还可以创建引用新属性的区段并开始生成见解。

查询服务允许您使用SQL查询执行上面列出的所有操作。 这包括在需要时更改数据集和字段组。

## 创建一个表，并带有一个为配置文件启用该表的选项 {#enable-dataset-for-profile}

>[!NOTE]
>
>下面提供的SQL查询假定使用预先存在的命名空间。

使用创建表作为选择(CTAS)查询创建数据集、分配数据类型、设置主标识、创建架构并将其标记为启用配置文件。 以下示例SQL语句创建属性并将其用于Real-time Customer Data Platform (Real-Time CDP)。 您的SQL查询将遵循以下示例中显示的格式：

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

支持的数据类型包括：布尔值、日期、日期时间、文本、浮点、bigint、整数、映射、数组和结构/行。

下面的SQl代码块提供了用于定义结构/行、映射和数组数据类型的示例。 第一行演示了行语法。 第二行演示映射语法，第三行演示数组语法。

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

或者，也可以通过Platform UI为配置文件启用数据集。 有关将数据集标记为已为用户档案启用的更多信息，请参阅 [为实时客户档案文档启用数据集](../../../catalog/datasets/user-guide.md#enable-profile).

在下面的示例查询中， `decile_table` 数据集创建工具 `id` 作为主标识列，具有命名空间 `IDFA`. 它还具有一个名为的字段 `decile1Month` 映射数据类型的ID。 创建的表(`decile_table`)为配置文件启用。

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

成功执行查询时，数据集ID将返回到控制台，如下面的示例所示。

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

使用 `label='PROFILE'` 在 `CREATE TABLE` 创建启用配置文件的数据集的命令。 此 `upsert` 默认情况下，功能处于打开状态。 此 `upsert` 功能可使用以下内容覆盖 `ALTER` 命令，如下面的示例所示。

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

有关使用的更多信息，请参阅SQl语法文档。 [更改表](../../sql/syntax.md#alter-table) 命令和 [标签作为CTAS查询的一部分](../../sql/syntax.md#create-table-as-select).

## 帮助通过SQL管理派生属性的构造

下面介绍的功能在通过SQL管理派生属性时非常有用。

### 更改要为配置文件启用的现有数据集 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL构造可用于为配置文件启用现有数据集。 这要求向架构和相应的数据集中添加启用配置文件的标记。

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>成功执行 `ALTER TABLE` 命令，控制台将返回 `ALTER SUCCESS`.

### 向现有数据集添加主要身份 {#add-primary-identity}

将数据集中的现有列标记为主标识集，否则会导致错误。 要使用SQL设置主标识，请使用下面显示的查询格式。

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

例如：

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

在提供的示例中， `id2` 是中的现有列 `test1_dataset`.

### 为配置文件禁用数据集 {#disable-dataset-for-profile}

如果要为配置文件禁用表，则必须使用DROP命令。 USES的示例SQL语句 `DROP` 如下所示。

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

例如：

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

此SQL语句提供了使用API调用的高效替代方法。 有关更多信息，请参阅有关如何执行操作的文档。 [使用数据集API禁用用于Real-Time CDP的数据集](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### 允许为数据集更新和插入功能 {#enable-upsert-functionality-for-dataset}

UPSERT命令允许您在表中插入新记录或更新现有数据。 具体来说，如果表中已存在指定的值，它允许您更新现有行；如果指定的值不存在，它允许您插入新行。

下面显示了使用正确格式的示例语句。

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

此SQL语句提供了使用API调用的高效替代方法。 有关更多信息，请参阅有关如何执行操作的文档。 [启用数据集，以便与Real-Time CDP一起使用，并使用数据集API进行UPSERT](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### 禁用数据集的更新和插入功能 {#disable-upsert-functionality-for-dataset}

此命令禁用更新行并将其插入到数据集的功能。

下面显示了使用正确格式的示例语句。

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 显示与每个表关联的其他表信息 {#show-labels-for-tables}

为启用配置文件的数据集保留其他元数据。 使用 `SHOW TABLES` 用于显示额外内容的命令 `labels` 列提供有关与表关联的任何标签的信息。

此命令的输出示例如下所示：

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

从示例中可以看到 `table_with_a_decile` 已为配置文件启用并已应用标签，例如 [&#39;更新插入&#39;](#enable-upsert-functionality-for-dataset)， [&#39;配置文件&#39;](#enable-existing-dataset-for-profile) 如前所述。

### 使用SQL创建字段组

现在可以通过使用SQL创建字段组。 为在平台UI中使用架构编辑器或对架构注册表进行API调用提供了替代方法。

下面显示了创建字段组的示例语句。

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>如果通过SQL创建字段组失败， `label` 标记未在语句中提供，或者字段组已存在。
>确保查询包含 `IF NOT EXISTS` 子句以避免查询失败，因为字段组已存在。

现实世界的例子可能与下面所示的例子类似。

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

成功执行此语句将返回创建的字段组ID。 例如：`c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`。

请参阅有关如何执行操作的文档 [在架构编辑器中创建新字段组](../../../xdm/ui/resources/field-groups.md#create) 或使用 [架构注册表API](../../../xdm/api/field-groups.md#create) 以了解有关替代方法的更多信息。

### 放置字段组

有时可能需要从架构注册表中删除字段组。 这是通过执行 `DROP FIELDGROUP` 命令。

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

例如：

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>如果字段组不存在，则通过SQL删除字段组将失败。 确保语句包含 `IF EXISTS` 子句以避免查询失败。

### 显示表的所有字段组名和ID

此 `SHOW FIELDGROUPS` 命令返回一个表，其中包含表的名称、fieldgroupId和所有者。

此命令的输出示例如下所示：

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## 后续步骤

阅读本文档后，您对如何使用SQL基于派生属性创建用户档案和启用更新插入的数据集有了更好的了解。 现在，您可以将此数据集与批量摄取工作流一起使用，以更新用户档案数据。 要了解有关将数据摄取到Adobe Experience Platform的更多信息，请先阅读 [数据摄取概述](../../../ingestion/home.md).
