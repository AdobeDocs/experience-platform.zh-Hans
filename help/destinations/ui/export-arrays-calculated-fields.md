---
title: 使用计算字段将数组导出为字符串
type: Tutorial
description: 了解如何使用计算字段将阵列作为字符串从Real-Time CDP导出到云存储目标。
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 6fec0432f71e58d0e17ac75121fb1028644016e1
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 0%

---

# 使用计算字段将数组导出为字符串{#use-calculated-fields-to-export-arrays-as-strings}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="导出阵列支持"
>abstract="<p>使用&#x200B;**添加计算字段**&#x200B;控件将int、字符串、布尔和对象值的数组从Experience Platform导出到所需的云存储目标。</p><p> 必须使用`array_to_string`函数将数组导出为字符串。 查看文档以了解大量示例和更多受支持的函数。</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="示例"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="已知限制"

>[!AVAILABILITY]
>
>* 通常提供通过计算字段导出数组的功能。

了解如何通过计算字段将阵列作为字符串从Real-Time CDP导出到[云存储目标](/help/destinations/catalog/cloud-storage/overview.md)。 请阅读本文档以了解此功能启用的用例。

获取有关计算字段的丰富信息 — 这些字段是什么以及它们为什么重要。 请阅读以下链接页面，了解有关数据准备中计算字段的介绍以及有关所有可用函数的更多信息：

* [UI指南和概述](/help/data-prep/ui/mapping.md#calculated-fields)
* [数据准备功能](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Platform中的数组和其他对象类型 {#arrays-strings-other-objects}

在Experience Platform中，您可以使用[XDM架构](/help/xdm/home.md)管理不同的字段类型。 以前，您可以将简单的键值对类型字段(如字符串不Experience Platform)导出到所需的目标。 以前支持导出的此类字段示例为`personalEmail.address`：`johndoe@acme.org`。

Experience Platform中的其他字段类型包括数组字段。 阅读有关Experience PlatformUI](/help/xdm/ui/fields/array.md)中[管理数组字段的更多信息。 除了以前支持的字段类型之外，您现在还可以使用`array_to_string`函数将数组对象（如下面的示例）导出为字符串。

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

请参阅下面的[大量示例](#examples)，了解如何使用各种函数访问数组的元素、转换和筛选数组、将数组元素加入字符串等。

## 已知限制 {#known-limitations}

请注意当前适用于此功能的以下已知限制：

* 目前不支持导出到具有分层架构&#x200B;*的JSON或Parquet文件*。 通过使用`array_to_string`函数，您可以将数组仅作为字符串&#x200B;*导出到CSV、JSON和Parquet文件*。

## 先决条件 {#prerequisites}

[将](/help/destinations/ui/connect-destination.md)连接到所需的云存储目标，完成云存储目标的[激活步骤](/help/destinations/ui/activate-batch-profile-destinations.md)并转到[映射](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)步骤。

## 如何导出计算字段 {#how-to-export-calculated-fields}

在云存储目标的激活工作流的映射步骤中，选择&#x200B;**[!UICONTROL 添加计算字段]**。

![添加在批处理激活工作流的映射步骤中突出显示的计算字段。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

这将打开一个模式窗口，您可以在其中选择用于导出属性以免Experience Platform的函数和字段。

![尚未选择函数的计算字段功能的模式窗口。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

例如，使用如下所示的`organizations`字段上的`array_to_string`函数将组织数组导出为CSV文件中的字符串。 查看](#array-to-string-function-export-arrays)下方的[有关此示例和其他示例的详细信息。

![选定了数组到字符串函数的计算字段功能的模式窗口。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保留计算字段并返回映射步骤。

![选定了array-to-string函数且突出显示Save控件的计算字段功能的模式窗口。](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

返回工作流的映射步骤，使用导出文件中该字段所需的列标题值填写&#x200B;**[!UICONTROL 目标字段]**。

![映射步骤，目标字段突出显示。](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![选择目标字段2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

准备就绪后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续执行激活工作流的下一步。

![映射步骤，其中目标字段高亮显示且目标值已填充。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## 导出数组的支持的函数示例 {#supported-functions}

将数据激活到基于文件的目标时，支持所有记录的[数据准备功能](/help/data-prep/functions.md)。

以下专门用于处理数组导出的函数与示例一起进行了说明。

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## 用于导出数组的函数示例 {#examples}

有关上面列出的某些函数，请参阅以下部分中的示例和更多信息。 对于列出的其余函数，请参阅数据准备部分](/help/data-prep/functions.md)中的[常规函数文档。

### `array_to_string`函数以导出数组 {#array-to-string-function-export-arrays}

使用所需的分隔符（如`_`或`|`），使用`array_to_string`函数将数组的元素连接到字符串中。

例如，您可以使用`array_to_string('_',organizations)`语法将以下XDM字段组合在一起，如映射屏幕快照中所示：

* `organizations`数组
* `person.name.firstName`字符串
* `person.name.lastName`字符串
* `personalEmail.address`字符串

![映射示例包括array_to_string函数。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何使用`_`字符将数组的元素连接到单个字符串中。

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `flattenArray`函数以导出平面化数组

使用`flattenArray`函数扁平化导出的多维数组。 您可以将此函数与上面进一步描述的`array_to_string`函数组合。

继续使用上面的`organizations`数组对象，您可以编写函数，如`array_to_string('_', flattenArray(organizations))`。 请注意，`array_to_string`函数默认将输入数组扁平化为字符串。

得到的输出与上面描述的`array_to_string`函数相同。


### `filterArray`函数以导出筛选的数组

使用`filterArray`函数筛选导出数组的元素。 您可以将此函数与上面进一步描述的`array_to_string`函数组合。

继续使用上面的`organizations`数组对象，您可以编写一个函数，如`array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`，并返回在2021年或更近年份具有`founded`值的组织。

![filterArray函数的示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

在这种情况下，您的输出文件将如下所示。 请注意数组中满足条件的两个元素如何使用`_`字符连接为单个字符串。

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray`函数以导出转换后的数组

使用`transformArray`函数转换导出数组的元素。 您可以将此函数与上面进一步描述的`array_to_string`函数组合。

使用上面的`organizations`数组对象继续，您可以编写一个函数，如`array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`，返回已转换为全部大写的组织名称。

![TransformArray函数的示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何使用`_`字符将数组的三个元素转换并连接为单个字符串。

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif`函数以导出数组 {#iif-function-export-arrays}

使用`iif`函数在特定条件下导出数组的元素。 例如，继续使用上面的`organizations`数组对象，可以编写简单的条件函数，如`iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`。

![映射示例包括iif函数。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

在这种情况下，您的输出文件将如下所示。 在这种情况下，数组的第一个元素是营销，因此人员是营销部门的成员。

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array`函数以导出数组 {#add-to-array-function-export-arrays}

使用`add_to_array`函数将元素添加到导出的数组。 您可以将此函数与上面进一步描述的`array_to_string`函数组合。

使用上面的`organizations`数组对象继续，您可以编写函数，如`source: array_to_string('_', add_to_array(organizations,"2023"))`，返回人员在2023年所属的组织。

![映射示例包括add_to_array函数。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何使用字符`_`将数组的三个元素连接到单个字符串中，并将2023也附加到字符串的末尾。

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce`函数以导出数组 {#coalesce-function-export-arrays}

使用`coalesce`函数访问数组的第一个非null元素并将其导出到字符串中。

例如，通过使用`coalesce(subscriptions.hasPromotion)`语法返回数组中`false`值的前`true`个，您可以组合下面的XDM字段，如映射屏幕快照中所示：

* `"subscriptions.hasPromotion": [null, true, null, false, true]`数组
* `person.name.firstName`字符串
* `person.name.lastName`字符串
* `personalEmail.address`字符串

![包括coalesce函数的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

在这种情况下，您的输出文件将如下所示。 请注意如何在文件中导出数组中的第一个非空`true`值。

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of`函数以导出数组 {#sizeof-function-export-arrays}

使用`size_of`函数指示数组中存在多少个元素。 例如，如果您有一个具有多个时间戳的`purchaseTime`数组对象，则可以使用`size_of`函数来指示某个人分别进行了多少次购买。

例如，您可以合并下面的以下XDM字段，如映射屏幕快照中所示。

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]`阵列，指示客户分别购买五次
* `personalEmail.address`字符串

![映射示例包括size_of函数。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

在这种情况下，您的输出文件将如下所示。 请注意第二列如何指示数组中的元素数，对应于客户进行的单独购买次数。

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### 基于索引的阵列访问 {#index-based-array-access}

您可以访问数组的索引以从数组导出单个项。 例如，与上述针对`size_of`函数的示例类似，如果您只想在客户购买特定产品时访问和导出，则可以使用`purchaseTime[0]`导出时间戳的第一个元素，使用`purchaseTime[1]`导出时间戳的第二个元素，使用`purchaseTime[2]`导出时间戳的第三个元素，依此类推。

![显示如何访问数组元素的映射示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

在这种情况下，您的输出文件如下所示，在客户首次购买时导出：

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first`和`last`函数以导出数组 {#first-and-last-functions-export-arrays}

使用`first`和`last`函数导出数组中的第一个或最后一个元素。 例如，使用前面示例中具有多个时间戳的`purchaseTime`数组对象继续，您可以使用这些对函数进行导出，以导出人员进行的首次购买或上次购买时间。

![映射示例，包括第一个和最后一个函数。](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

在这种情况下，您的输出文件将如下所示，导出客户第一次和最后一次购买的时间：

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->