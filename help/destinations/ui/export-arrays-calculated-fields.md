---
title: （Beta版）使用计算字段导出平面文件中的阵列
type: Tutorial
description: 了解如何将阵列和计算字段从Real-Time CDP导出到基于配置文件的批处理目标。
badge: "Beta 版"
source-git-commit: 79924b9a7d5114c94a004f99fb194102845b2127
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 2%

---


# （Beta版）使用计算字段导出平面架构文件中的阵列 {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta)导出阵列支持"
>abstract="将int、字符串或布尔值的简单数组从Experience Platform导出到所需的云存储目标。 存在一些限制。 查看文档以了解大量示例和支持的函数。"

<!--

additional links for contextualhelp:

>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Examples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Known limitations"

-->

>[!AVAILABILITY]
>
>* 通过计算字段导出数组的功能当前处于测试阶段。 文档和功能可能会发生变化。

了解如何通过计算字段将阵列从平面架构文件中的Real-Time CDP导出到云存储目标。 请阅读本文档以了解此功能启用的用例。

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

进度 [云存储目标的激活步骤](/help/destinations/ui/activate-batch-profile-destinations.md) 然后转到 [映射](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 步骤。

## 如何导出计算字段 {#how-to-export-calculated-fields}

在云存储目标的激活工作流的映射步骤中，选择 **[!UICONTROL (Beta)添加计算字段]**.

![添加计算字段以导出](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

这将打开一个模式窗口，您可以在其中选择可用于将属性导出到Experience Platform之外的属性。

>[!IMPORTANT]
>
>XDM架构中的某些字段在中仅可用 **[!UICONTROL 字段]** 视图。 您可以看到字符串值以及字符串、整数和布尔值的数组。 例如， `segmentMembership` 数组不会显示，因为它包含其他数组值。

![模式窗口1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，使用 `join` 上的函数 `loyaltyID` 如下所示的字段，用于在CSV文件中将忠诚度ID数组导出为与下划线连接的字符串。 视图 [有关此内容以及下面其他示例的更多信息](#join-function-export-arrays).

![模式窗口2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

选择 **[!UICONTROL 保存]** 以保留计算字段并返回映射步骤。

![模式窗口3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

返回工作流的映射步骤，填写 **[!UICONTROL 目标字段]** 在导出的文件中为此字段使用所需的列标题值。

![选择目标字段1](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![选择目标字段2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

准备就绪后，选择 **[!UICONTROL 下一个]** 以继续执行激活工作流的下一步。

![选择“下一步”以继续](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

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

![映射屏幕快照](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何使用将数组的三个元素连接到单个字符串中 `_` 字符。

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `coalesce` 用于导出数组的函数 {#coalesce-function-export-arrays}

使用 `coalesce` 函数，用于访问数组的第一个非空元素并将其导出到字符串中。

例如，您可以使用合并以下的XDM字段，如映射屏幕快照中所示 `coalesce(subscriptions.hasPromotion)` 语法返回数组中false值的第一个true ：

* `"subscriptions.hasPromotion": [null, true, null, false, true]` 数组
* `person.name.firstName` 字符串
* `person.name.lastName` 字符串
* `personalEmail.address` 字符串

![Coalesce函数的映射屏幕快照](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

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

![映射size_of函数的屏幕截图](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

在这种情况下，您的输出文件将如下所示。 请注意第二列如何指示数组中的元素数，对应于客户进行的单独购买次数。

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 基于索引的阵列访问 {#index-based-array-access}

您可以访问数组的索引以从数组导出单个项。 例如，与上面的示例类似， `size_of` 功能，如果您希望仅在客户首次购买特定产品时访问和导出，则可以使用 `purchaseTime[0]` 要导出时间戳的第一个元素， `purchaseTime[1]` 要导出时间戳的第二个元素， `purchaseTime[2]` 以导出时间戳的第三个元素，依此类推。

![用于访问索引的映射屏幕截图](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

在这种情况下，您的输出文件将如下所示：

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` 和 `last` 用于导出数组的函数 {#first-and-last-functions-export-arrays}

使用 `first` 和 `last` 用于导出数组中的第一个或最后一个元素的函数。 例如，继续使用 `purchaseTime` 具有前几个示例中的多个时间戳的数组对象，您可以使用这些对象到函数以导出人员的首次购买时间或上次购买时间。

![映射第一个和最后一个函数的屏幕截图](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

在这种情况下，您的输出文件将如下所示：

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### `iif` function to export arrays {#iif-function-export-arrays}

Here are some examples of how you could use the `iif` function to access and export arrays and other fields: (STILL TO DO)

-->

### `md5` 和 `sha256` 哈希函数 {#hashing-functions}

除了从数组导出数组或元素的特定函数之外，您还可以使用散列函数来散列属性。 例如，如果您在属性中有任何个人身份信息，则可以在导出这些字段时对其进行哈希处理。

您可以直接散列字符串值，例如 `md5(personalEmail.address)`. 如果需要，您还可以散列数组字段的单个元素，如下所示： `md5(purchaseTime[0])`



