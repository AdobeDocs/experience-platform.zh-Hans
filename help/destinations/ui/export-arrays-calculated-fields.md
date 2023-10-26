---
title: （Beta版）使用计算字段导出平面架构文件中的阵列
type: Tutorial
description: 了解如何使用计算字段将平面架构文件中的阵列从Real-Time CDP导出到云存储目标。
badge: Beta 版
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: b6bdfef8b9ac5ef03ea726d668477b8629b70b6c
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 5%

---

# （Beta版）使用计算字段导出平面架构文件中的阵列 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) 导出数组支持"
>abstract="使用&#x200B;**添加计算字段**&#x200B;控件，将整型、字符串或布尔值的简单数组从 Experience Platform 导出到所需的云存储目标。其中适用一些限制。查看文档以了解大量示例和支持的函数。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="示例"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="已知限制"

>[!AVAILABILITY]
>
>* 通过计算字段导出数组的功能当前处于测试阶段。 文档和功能可能会发生变化。

了解如何通过平面架构文件中Real-Time CDP的计算字段将阵列导出到 [云存储目标](/help/destinations/catalog/cloud-storage/overview.md). 请阅读本文档以了解此功能启用的用例。

获取有关计算字段的丰富信息 — 这些字段是什么以及它们为什么重要。 请阅读以下链接页面，了解有关数据准备中计算字段的介绍以及有关所有可用函数的更多信息：

* [UI指南和概述](/help/data-prep/ui/mapping.md#calculated-fields)
* [数据准备功能](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>并非上面列出的所有函数都受支持 *将字段导出到云存储目标时* 使用计算字段功能。 请参阅 [“支持的函数”部分](#supported-functions) 有关更多信息，请参阅下文。

## Platform中的数组和其他对象类型 {#arrays-strings-other-objects}

在Experience Platform中，您可以使用 [XDM架构](/help/xdm/home.md) 以管理不同的字段类型。 以前，您可以将简单的键值对类型字段(如字符串不Experience Platform)导出到所需的目标。 以前支持导出的此类字段的示例为 `personalEmail.address`：`johndoe@acme.org`.

Experience Platform中的其他字段类型包括数组字段。 详细了解 [管理Experience PlatformUI中的数组字段](/help/xdm/ui/fields/array.md). 除了以前支持的字段类型之外，您现在还可以导出数组对象，例如： `organizations:[marketing, sales, engineering]`. 请参阅下面的更多信息 [大量示例](#examples) 介绍如何使用各种函数来访问数组的元素，将数组元素加入字符串等。

## 已知限制 {#known-limitations}

请注意此功能测试版的以下已知限制：

* 目前不支持导出到具有分层架构的JSON或Parquet文件。 您只能将数组导出为平面架构CSV、JSON和Parquet文件。
* 此时， *您只能将简单阵列（或基元值阵列）导出到云存储目标*. 这意味着您可以导出包含字符串、int或布尔值的数组对象。 无法导出映射或对象数组。计算字段模式窗口仅显示可导出的数组。

## 先决条件 {#prerequisites}

[连接](/help/destinations/ui/connect-destination.md) 到所需的云存储目标，请浏览 [云存储目标的激活步骤](/help/destinations/ui/activate-batch-profile-destinations.md) 然后转到 [映射](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 步骤。

## 如何导出计算字段 {#how-to-export-calculated-fields}

在云存储目标的激活工作流的映射步骤中，选择 **[!UICONTROL (Beta)添加计算字段]**.

![添加在批量激活工作流的映射步骤中高亮显示的计算字段。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

这将打开一个模式窗口，您可以在其中选择可用于将属性导出到Experience Platform之外的属性。

>[!IMPORTANT]
>
>XDM架构中的某些字段在中仅可用 **[!UICONTROL 字段]** 视图。 您可以看到字符串值以及字符串、整数和布尔值的数组。 例如， `segmentMembership` 数组不会显示，因为它包含其他数组值。

![尚未选择函数的计算字段功能的模式窗口。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，使用 `join` 上的函数 `loyaltyID` 如下所示的字段，用于在CSV文件中将忠诚度ID数组导出为与下划线连接的字符串。 视图 [有关此内容以及下面其他示例的更多信息](#join-function-export-arrays).

![已选择连接函数的计算字段功能的模式窗口。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

选择 **[!UICONTROL 保存]** 以保留计算字段并返回映射步骤。

![选定联接函数并突出显示“保存”控件时计算字段功能的模态窗口。](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

返回工作流的映射步骤，填写 **[!UICONTROL 目标字段]** 在导出的文件中为此字段使用所需的列标题值。

![突出显示目标字段的映射步骤。](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![选择目标字段2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

准备就绪后，选择 **[!UICONTROL 下一个]** 以继续执行激活工作流的下一步。

![映射步骤，其中突出显示目标字段并填充目标值。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 支持的函数 {#supported-functions}

请注意，计算字段的测试版仅支持以下函数，并且目标支持数组：

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## 用于导出数组的函数示例 {#examples}

有关上面列出的某些函数，请参阅以下部分中的示例和更多信息。 对于列出的其余函数，请参阅 [“数据准备”部分中的常规函数文档](/help/data-prep/functions.md).

### `join` 用于导出数组的函数 {#join-function-export-arrays}

使用 `join` 用于将数组的元素连接到字符串的函数，使用所需的分隔符，例如 `_` 或 `|`.

例如，您可以使用合并以下的XDM字段，如映射屏幕快照中所示 `join('_',loyalty.loyaltyID)` 语法：

* `"organizations": ["Marketing","Sales,"Finance"]` 数组
* `person.name.firstName` 字符串
* `person.name.lastName` 字符串
* `personalEmail.address` 字符串

![包含连接函数的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何使用将数组的三个元素连接到单个字符串中 `_` 字符。

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` 用于导出数组的函数 {#iif-function-export-arrays}

使用 `iif` 函数以导出特定条件下的数组元素。 例如，继续使用 `organizations` 从上面数组对象，可以编写一个简单的条件函数，如 `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![包括iif函数的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

在这种情况下，您的输出文件将如下所示。 在这种情况下，数组的第一个元素是营销，因此人员是营销部门的成员。

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` 用于导出数组的函数 {#add-to-array-function-export-arrays}

使用 `add_to_array` 函数以将元素添加到导出的数组。 您可以将此函数与 `join` 函数中。

继续使用 `organizations` 从上面数组对象，您可以编写函数，如 `source: join('_', add_to_array(organizations,"2023"))`，退回2023年人员所属的组织。

![包括add_to_array函数的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何使用将数组的三个元素连接到单个字符串中 `_` 字符和2023也附加在字符串的末尾。

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` 用于导出数组的函数 {#coalesce-function-export-arrays}

使用 `coalesce` 函数，用于访问数组的第一个非空元素并将其导出到字符串中。

例如，您可以使用合并以下的XDM字段，如映射屏幕快照中所示 `coalesce(subscriptions.hasPromotion)` 用于返回第一个 `true` 之 `false` 数组中的值：

* `"subscriptions.hasPromotion": [null, true, null, false, true]` 数组
* `person.name.firstName` 字符串
* `person.name.lastName` 字符串
* `personalEmail.address` 字符串

![包括coalesce函数的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

在这种情况下，您的输出文件将如下所示。 请注意第一个非空值的方式 `true` 数组中的值会导出到文件中。

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` 用于导出数组的函数 {#sizeof-function-export-arrays}

使用 `size_of` 函数来指示数组中存在的元素数。 例如，如果您拥有 `purchaseTime` 具有多个时间戳的数组对象，您可以使用 `size_of` 指示某个人单独购买多少次的功能。

例如，您可以合并下面的以下XDM字段，如映射屏幕快照中所示。

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` 数组，指示客户的五个单独购买时间
* `personalEmail.address` 字符串

![包括size_of函数的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

在这种情况下，您的输出文件将如下所示。 请注意第二列如何指示数组中的元素数，对应于客户进行的单独购买次数。

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 基于索引的阵列访问 {#index-based-array-access}

您可以访问数组的索引以从数组导出单个项。 例如，与上面的示例类似， `size_of` 功能，如果您希望仅在客户首次购买特定产品时访问和导出，则可以使用 `purchaseTime[0]` 要导出时间戳的第一个元素， `purchaseTime[1]` 要导出时间戳的第二个元素， `purchaseTime[2]` 以导出时间戳的第三个元素，依此类推。

![显示如何访问数组的元素的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

在这种情况下，您的输出文件如下所示，在客户首次购买时导出：

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` 和 `last` 用于导出数组的函数 {#first-and-last-functions-export-arrays}

使用 `first` 和 `last` 用于导出数组中的第一个或最后一个元素的函数。 例如，继续使用 `purchaseTime` 具有前几个示例中的多个时间戳的数组对象，您可以使用这些对象到函数以导出人员的首次购买时间或上次购买时间。

![映射示例，包括第一个和最后一个函数。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

在这种情况下，您的输出文件将如下所示，导出客户第一次和最后一次购买的时间：

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### 哈希函数 {#hashing-functions}

除了从数组导出数组或元素的特定函数之外，您还可以使用散列函数对导出文件中的属性进行散列。 例如，如果您在属性中有任何个人身份信息，则可以在导出这些字段时对其进行哈希处理。

您可以直接散列字符串值，例如 `md5(personalEmail.address)`. 如果需要，您还可以散列数组字段的单个元素，假定数组中的元素是字符串，如下所示： `md5(purchaseTime[0])`

支持的哈希函数包括：

| 函数 | 示例表达式 |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}