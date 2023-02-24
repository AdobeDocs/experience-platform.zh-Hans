---
title: 派生属性的无缝SQL流
description: 查询服务SQL已扩展，可无缝支持派生属性。 了解如何使用此SQL扩展创建为配置文件启用的派生属性，以及如何将该属性用于实时客户配置文件和分段服务。
source-git-commit: 1ff66d0ac8e0491a6db518545d122555d9d54c75
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 1%

---

# 派生属性的无缝SQL流

查询服务SQL已扩展，可无缝支持派生属性。 这为为实时客户资料业务用例创建派生属性提供了一种有效的替代方法。

本文档概述了各种方便的SQL扩展，这些扩展生成了用于实时客户配置文件的派生属性。 该工作流简化了您通过各种API调用或平台UI交互必须完成的流程。

通常，生成和发布实时客户配置文件的属性将涉及以下步骤：

* 创建标识命名空间（如果不存在）。
* 如有必要，创建用于存储派生属性的数据类型。
* 使用该数据类型创建字段组以存储派生的属性信息。
* 创建或分配一个主标识列，该列使用之前创建的命名空间。
* 使用之前创建的字段组和数据类型创建模式。
* 使用您的架构创建新数据集，并根据需要为用户档案启用该数据集。
* （可选）将数据集标记为已启用配置文件。

完成上述步骤后，即可填充数据集。 如果为配置文件启用了数据集，则还可以创建引用新属性的区段，并开始生成分析。

查询服务允许您使用SQL查询执行上面列出的所有操作。 这包括根据需要更改数据集和字段组。

## 创建一个表格，其中包含一个选项，为用户档案启用该表格 {#enable-dataset-for-profile}

>[!NOTE]
>
>下面提供的SQL查询假定使用预先存在的命名空间。

使用创建表作为选择(CTAS)查询创建数据集、分配数据类型、设置主标识、创建架构，并将其标记为启用了配置文件。 以下示例SQL语句创建属性，并使其可用于实时客户数据配置文件(Real-Time CDP)。 您的SQL查询将遵循以下示例中显示的格式：

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

或者，也可以通过Platform UI为用户档案启用数据集。 有关将数据集标记为已启用用户档案的更多信息，请参阅 [为实时客户配置文件文档启用数据集](../../../catalog/datasets/user-guide.md#enable-profile).

在以下示例查询中， `decile_table` 数据集创建时使用 `id` 作为主标识列，且具有命名空间 `IDFA`. 它还有一个名为 `decile1Month` 映射数据类型。 创建的表(`decile_table`)。

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

<!--        decile3Month map<text, integer>,
            decile6Month map<text, integer>,
            decile9month map<text, integer>,
            decile12month map<text, integer>,
            decilelifetime map<text, integer> -->

成功执行查询后，数据集ID将返回到控制台，如以下示例所示。

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

使用 `label='PROFILE'` 在 `CREATE TABLE` 命令创建启用了配置文件的数据集。 的 `upsert` 默认情况下，功能处于打开状态。 的 `upsert` 功能可以使用 `ALTER` 命令，如以下示例中所示。

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

有关使用的SQl语法的更多信息，请参阅SQl语法文档 [ALTER TABLE](../../sql/syntax.md#alter-table) 命令和 [作为CTAS查询一部分的标签](../../sql/syntax.md#create-table-as-select).

## 用于帮助通过SQL管理派生属性的结构

下面描述的功能在通过SQL管理派生属性时非常有用。

### 更改要为配置文件启用的现有数据集 {#enable-existing-dataset-for-profile}

ALTER TABLE SQL结构可用于为配置文件启用现有数据集。 这要求将启用配置文件的标记添加到架构和相应的数据集。

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>成功执行 `ALTER TABLE` 命令，控制台将返回 `ALTER SUCCESS`.

### 将主标识添加到现有数据集 {#add-primary-identity}

将数据集中的现有列标记为主标识集，否则，会导致错误。 要使用SQL设置主标识，请使用下面显示的查询格式。

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

例如：

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

在提供的示例中， `id2` 是 `test1_dataset`.

### 为配置文件禁用数据集 {#disable-dataset-for-profile}

如果要为使用的配置文件禁用表，则必须使用DROP命令。 USES的SQL语句示例 `DROP` 下方显示。

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

例如：

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

此SQL语句为使用API调用提供了一种有效的替代方法。 有关更多信息，请参阅有关如何 [禁用数据集以与Real-Time CDP一起使用，使用数据集API](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### 允许更新和插入数据集的功能 {#enable-upsert-functionality-for-dataset}

UPSERT命令允许您插入新记录或更新表中的现有数据。 具体而言，它允许您在表中已存在指定值时更新现有行，或在指定值不存在时插入新行。

下面显示了使用正确格式的示例语句。

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

此SQL语句为使用API调用提供了一种有效的替代方法。 有关更多信息，请参阅有关如何 [启用数据集以与Real-Time CDP和UPSERT一起使用，使用数据集API](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### 禁用数据集的更新和插入功能 {#disable-upsert-functionality-for-dataset}

此命令会禁用更新行并将其插入数据集的功能。

下面显示了使用正确格式的示例语句。

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

例如：

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### 显示与每个表关联的其他表信息 {#show-labels-for-tables}

启用了配置文件的数据集将保留其他元数据。 使用 `SHOW TABLES` 显示 `labels` 列，提供有关与表关联的任何标签的信息。

此命令的输出示例如下所示：

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

您可以从示例中看到 `table_with_a_decile` 已为用户档案启用并应用了诸如 [“UPSERT”](#enable-upsert-functionality-for-dataset), [“用户档案”](#enable-existing-dataset-for-profile) 如前面所述。

### 使用SQL创建字段组

现在，可以通过使用SQL来创建字段组。 这提供了一种替代方法，可以在Platform UI中使用架构编辑器，或对架构注册表进行API调用。

下面显示了用于创建字段组的示例语句。

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>如果 `label` 标记未在语句中提供，或者字段组已存在。
>确保查询包含 `IF NOT EXISTS` 子句来避免查询失败，因为字段组已存在。

真实世界的示例可能与下面所示的示例类似。

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

成功执行此语句将返回创建的字段组ID。 例如：`c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`。

请参阅有关如何 [在架构编辑器中创建新字段组](../../../xdm/ui/resources/field-groups.md#create) 或使用 [架构注册API](../../../xdm/api/field-groups.md#create) 以了解有关替代方法的更多信息。

### 删除字段组

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
>如果字段组不存在，则通过SQL删除字段组将失败。 确保语句包含 `IF EXISTS` 子句来避免查询失败。

### 显示表的所有字段组名称和ID

的 `SHOW FIELDGROUPS` 命令返回一个包含表名称、fieldgroupId和所有者的表。

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

阅读本文档后，您对如何使用SQL创建配置文件并基于派生属性重新插入数据集有了更好的了解。 现在，您可以将此数据集与批量摄取工作流结合使用，以更新配置文件数据。 要了解有关将数据摄取到Adobe Experience Platform的更多信息，请首先阅读 [数据摄取概述](../../../ingestion/home.md).
