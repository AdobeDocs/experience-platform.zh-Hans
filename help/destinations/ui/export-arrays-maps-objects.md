---
title: 将阵列、映射和对象从Real-Time CDP导出到云存储目标
type: Tutorial
description: 了解如何将阵列、映射和对象从Real-Time CDP导出到云存储目标。
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 15%

---

# 将阵列、映射和对象从Real-Time CDP导出到云存储目标 {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>将阵列导出到云存储目标的功能通常适用于以下目标： [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)、[[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)、[[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)、[[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md)、[[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md)、[[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md)，

了解如何将阵列从Real-Time CDP导出到[云存储目标](/help/destinations/catalog/cloud-storage/overview.md)。 阅读本文档以了解导出工作流、通过此功能启用的用例以及已知限制。

您可以将此页面作为您希望了解有关从Experience Platform导出数组、映射和其他对象类型的所有信息的首选位置。

## 底线在前面

在此部分中获取有关功能的最重要信息，并继续在下面转到文档的其他部分以了解详细信息。

* 导出数组、映射和对象的功能取决于您选择的&#x200B;**导出数组、映射、对象**&#x200B;切换。 请在页面](#export-arrays-maps-objects-toggle)上的下方[阅读更多相关信息。
* 只能在`JSON`和`Parquet`文件中将阵列、映射和对象导出到云存储目标。 人员和潜在客户受众受支持，而帐户受众不受支持。
* 您&#x200B;*可以*&#x200B;将数组、映射和对象导出到CSV文件，但只能通过使用`array_to_string`函数的计算字段功能并将它们串联为字符串来这样做。

## Platform中的数组和其他对象类型 {#arrays-strings-other-objects}

在Experience Platform中，您可以使用[XDM架构](/help/xdm/home.md)管理不同的字段类型。 在添加对数组导出的支持之前，您可以将简单的键值对类型字段(例如Experience Platform中的字符串)导出到所需的目标。 以前支持导出的此类字段示例为`personalEmail.address`：`johndoe@acme.org`。

Experience Platform中的其他字段类型包括数组字段。 阅读有关[在Experience Platform UI](/help/xdm/ui/fields/array.md)中管理数组字段的更多信息。 您现在可以导出数组对象，如下面的示例所示。

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

除了阵列之外，您还可以将映射和对象从Experience Platform导出到所需的云存储目标。 详细了解Experience Platform中的[映射](/help/xdm/ui/fields/map.md)和[对象](/help/xdm/ui/fields/object.md)。

## 先决条件 {#prerequisites}

[将](/help/destinations/ui/connect-destination.md)连接到所需的云存储目标，完成云存储目标的[激活步骤](/help/destinations/ui/activate-batch-profile-destinations.md)并转到[映射](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)步骤。 连接到所需的云目标时，必须选择&#x200B;**[!UICONTROL 导出数组、映射、对象]**&#x200B;切换开关。 有关更多信息，请参阅以下部分。

## 导出数组、映射和对象切换 {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="导出数组、映射和对象"
>abstract="<p> 将此设置切换为 <b>开</b>，以启用将数组、映射和对象导出到 JSON 或 Parquet 文件的功能。您可以在映射步骤中的源字段视图中选择这些对象类型。将其切换为开后，您就无法使用映射步骤中的计算字段选项。</p><p>将其切换为<b>关</b>后，您可以在激活受众时使用计算字段选项并应用各种数据转换功能。但是，您<i>不能</i>将数组、映射和对象导出到 JSON 或 Parquet 文件，要达到此目的必须配置单独的目标。</p>"

在连接到云存储目标时，可以设置打开或关闭&#x200B;**[!UICONTROL 导出阵列、映射、对象]**&#x200B;的切换开关。

![使用打开或关闭设置以及突出显示弹出框来导出数组、映射、对象切换。](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

将此设置切换为 **开**，以启用将数组、映射和对象导出到 JSON 或 Parquet 文件的功能。将受众激活到云存储目标时，您可以在[映射步骤](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)的源字段视图中选择这些对象类型。 但是，如果启用此设置，则不能在激活时使用计算字段选项来转换数据。

将其切换为&#x200B;**关**&#x200B;后，您可以在激活受众时使用计算字段选项并应用各种数据转换功能。但是，您不能将数组、映射和对象导出到JSON或Parquet文件，并且必须为此配置单独的目标。

## 导出数组、映射、对象将&#x200B;*切换为* {#export-arrays-maps-objects-toggle-on}

启用此设置后，您可以通过激活工作流映射步骤中的源字段选择器选择对象，导出整个对象（例如`person.name`）和数组。

![在激活工作流的映射步骤中，通过源字段选择器选择对象。](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

选中此选项后，用户界面会阻止用户使用计算字段，并且禁用&#x200B;**[!UICONTROL 添加计算字段]**&#x200B;控件，如下所示。 要将计算字段用于数据转换，请在关闭切换的情况下设置目标连接。

![已禁用计算字段控件。](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## 导出数组、映射、对象切换&#x200B;*关闭* {#export-arrays-maps-objects-toggle-off}

如果将此选项设置为&#x200B;*off*，则可以在激活受众时使用计算字段选项并应用各种数据转换函数。 但是，您不能将数组、映射和对象导出到JSON或Parquet文件，并且必须为此配置单独的目标。

您&#x200B;*可以*&#x200B;使用计算字段功能将数组、映射和对象导出到CSV文件，并使用`array_to_string`函数将它们串联为字符串。 [阅读有关使用该函数的更多信息](#array-to-string-function-export-arrays)。

阅读有关使用计算字段以[对导出到云存储目标](/help/destinations/ui/data-transformations-calculated-fields.md)的数据执行转换的更多信息。

## 示例导出文件 {#sample-exported-files}

通过使用此功能，您可以导出Parquet和JSON文件，其中的数据会保留Experience Platform中的结构。 在下方查看导出的JSON文件示例。

+++ 选择可查看导出的JSON文件。

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++