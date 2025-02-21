---
title: 使用计算字段对导出到云存储目标的数据执行转换
type: Tutorial
description: 了解如何使用计算字段功能对导出到云存储目标的数据执行转换
source-git-commit: 6122ddc078101c26061e8662de3fcdcb1cb65992
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 3%

---

# 使用计算字段对导出到云存储目标的数据执行转换 {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="添加计算字段"
>abstract="<p>使用&#x200B;**添加计算字段**&#x200B;控件对导出到云存储目标的数据执行各种数据转换。 例如，您可以将散列应用于数据，将数组串联为字符串等。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="示例"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="已知限制"

>[!AVAILABILITY]
>
>对导出到云存储目标的数据执行转换的功能通常适用于以下目标： [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)、[[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)、[[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)、[[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md)、[[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md)、[[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md)以及通过[Destination SDK](/help/destinations/destination-sdk/overview.md)创作的任何自定义合作伙伴编写的云存储目标。

要对导出到云存储目标的数据执行各种转换，您必须在导出工作流的映射步骤中使用计算字段功能。 有关计算字段的详细信息，请访问下面链接的页面。 这些页面包括对数据准备中计算字段的介绍，以及有关所有可用函数的更多信息：

* [UI指南和概述](/help/data-prep/ui/mapping.md#calculated-fields)
* [数据准备功能](/help/data-prep/functions.md)

## 先决条件 {#prerequisites}

要将计算字段用于数据转换：

1. [将](/help/destinations/ui/connect-destination.md)连接到所需的云存储目标。 连接到所需的云目标时，将&#x200B;**[!UICONTROL 导出数组、映射、对象]** [选项切换为关闭](/help/destinations/ui/export-arrays-calculated-fields.md##export-arrays-maps-objects-toggle)。
2. 执行云存储目标](/help/destinations/ui/activate-batch-profile-destinations.md)的[激活步骤并转到[映射](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)步骤。

## 如何使用计算字段 {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="启用分层输出架构"
>abstract="启用此设置可启用将数组、映射和对象导出到JSON或Parquet文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="添加计算字段已禁用"
>abstract="此控件已被禁用，因为您在设置此目标连接时选择了将&#x200B;**导出数组、映射、对象** 切换为&#x200B;*开*。要使用计算字段及其中可用的功能，通过将&#x200B;**导出数组、映射、对象** 切换为&#x200B;*关*&#x200B;设置一个新的目标连接。"

在云存储目标的激活工作流的映射步骤中，选择&#x200B;**[!UICONTROL 添加计算字段]**。

>[!TIP]
>
>对于已关闭&#x200B;**[!UICONTROL 导出数组、映射和对象]**&#x200B;控件的目标连接，**[!UICONTROL 添加计算字段]**&#x200B;控件已禁用。 [了解更多信息](/help/destinations/ui/export-arrays-calculated-fields.md#export-arrays-maps-objects-toggle)。

![添加在批处理激活工作流的映射步骤中突出显示的计算字段。](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

这将打开一个模式窗口，您可以在其中选择用于从Experience Platform中导出属性的函数和字段。

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

## 用于执行数据转换的支持函数示例 {#supported-functions}

将数据激活到基于文件的目标时，支持所有记录的[数据准备功能](/help/data-prep/functions.md)。

以下专门用于处理数组的导出或对字段应用哈希的函数与示例一起进行了说明。

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

## 用于执行数据转换的函数示例 {#examples}

有关上面列出的某些函数，请参阅以下部分中的示例和更多信息。 对于列出的其余函数，请参阅数据准备部分](/help/data-prep/functions.md)中的[常规函数文档。

### `array_to_string`函数以导出数组 {#array-to-string-function-export-arrays}

使用所需的分隔符（如`_`或`|`），使用`array_to_string`函数将数组的元素连接到字符串中。 当您想要将数组的元素从Experience Platform导出到CSV文件时，此函数非常有用。

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

### `filterArray`函数以导出筛选的数组 {#filter-array}

使用`filterArray`函数筛选导出数组的元素。 您可以将此函数与上面进一步描述的`array_to_string`函数组合。

使用上面的`organizations`数组对象继续，您可以编写一个函数，如`array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`，该函数返回在2021年或更近年份具有`founded`值的组织。

![filterArray函数的示例。](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

在这种情况下，您的输出文件将如下所示。 请注意数组中满足条件的两个元素如何使用`_`字符连接为单个字符串。

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray`函数以导出转换后的数组 {#transform-array}

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

### `flattenArray`函数以导出平面化数组 {#flatten-array}

使用`flattenArray`函数扁平化导出的多维数组。 您可以将此函数与上面进一步描述的`array_to_string`函数组合。

继续使用上面的`organizations`数组对象，您可以编写函数，如`array_to_string('_', flattenArray(organizations))`。 请注意，`array_to_string`函数默认将输入数组扁平化为字符串。

结果输出与上面进一步描述的`array_to_string`函数输出相同。

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

>[!IMPORTANT]
>
>与此页面上描述的其他函数不同，要导出数组的单个元素，您&#x200B;*不需要*&#x200B;在UI中使用&#x200B;**[!UICONTROL 计算字段]**&#x200B;控件。

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

### 哈希函数 {#hashing-functions}

其他可用函数专门用于从数组导出数组或元素。 您可以使用散列函数对导出文件中的属性进行散列。 例如，如果您在属性中有任何个人身份信息，则可以在导出这些字段时对其进行哈希处理。

您可以直接散列字符串值，例如`md5(personalEmail.address)`。 如果需要，您还可以散列数组字段的各个元素，假定数组中的元素是字符串，如下所示： `md5(purchaseTime[0])`

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
