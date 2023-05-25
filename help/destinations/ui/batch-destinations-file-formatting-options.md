---
description: 了解在将数据激活到基于文件的目标时如何配置文件格式选项
title: （测试版）为基于文件的目标配置文件格式选项
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: b1e9b781f3b78a22b8b977fe08712d2926254e8c
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 19%

---

# （测试版）为基于文件的目标配置文件格式选项

>[!IMPORTANT]
>
>此 **[!UICONTROL 文件格式选项]** Adobe Experience Platform中的功能目前处于Beta阶段。 文档和功能可能会发生更改。
>请联系您的Adobe代表以获取此功能的访问权限。
> 
>本文档中描述的文件格式选项当前仅适用于CSV文件。

当您使用时，可以使用为导出的文件配置各种文件格式选项的选项 [connect](/help/destinations/ui/connect-destination.md) 到基于文件的目标，例如 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect)， [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)，或 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

您可以使用Experience PlatformUI为导出的文件配置各种文件格式选项。 您可以修改导出文件的多个属性，以符合您所在端文件接收系统的要求，从而以最佳方式读取和解释从Experience Platform接收的文件。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## CSV文件的文件格式配置 {#file-configuration}

要显示文件格式选项，请启动 [连接到目标](/help/destinations/ui/connect-destination.md) 工作流。 选择 **数据类型：区段** 和 **文件类型：CSV** 用于显示可用于导出的文件格式设置 `CSV` 文件。

>[!IMPORTANT]
>
>您连接到的目标可能没有所有这些可用选项。 由目标开发人员决定他们要在目标中支持哪些文件格式选项。 目标开发人员可以确定在连接到目标时可用的选项。 在Experience PlatformUI中，必填选项标有星号。
> 
>新的云存储目标 —  [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)， [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [(Beta)数据登陆区](/help/destinations/catalog/cloud-storage/data-landing-zone.md)， [（测试版） Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)， [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md)  — 当前仅支持下面高亮显示的六个CSV选项。

![显示一些可用文件格式选项的图像。](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔符 {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="分隔符"
>abstract="使用此控件为每个字段和值设置分隔符。查看每个选择的示例文档。"

使用此控件可为导出的CSV文件中的每个字段和值设置分隔符。 可用选项包括：

* 冒号 `(:)`
* 逗号 `(,)`
* 竖线 `(|)`
* 分号 `(;)`
* Tab `(\t)`

#### 示例

通过UI中的每个选择，查看导出的CSV文件中内容的以下示例。

* 示例输出 **[!UICONTROL 冒号`(:)`]** 已选定： `male:John:Doe`
* 示例输出 **[!UICONTROL 逗号`(,)`]** 已选定： `male,John,Doe`
* 示例输出 **[!UICONTROL 管道`(|)`]** 已选定： `male|John|Doe`
* 示例输出 **[!UICONTROL 分号`(;)`]** 已选定： `male;John;Doe`
* 示例输出 **[!UICONTROL 选项卡`(\t)`]** 已选定： `male \t John \t Doe`

### 引号字符 {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="引号字符"
>abstract="如果要从导出的字符串中删除双引号，请使用此选项。查看每个选择的示例文档。"

如果要从导出的字符串中删除双引号，请使用此选项。可用选项包括：

* **[!UICONTROL 空字符(\0000)]**. 使用此选项可从导出的CSV文件中删除双引号。
* **[!UICONTROL 双引号(“)]**. 使用此选项可在导出的CSV文件中保留双引号。

#### 示例

通过UI中的每个选择，查看导出CSV文件中内容的以下示例。

* 示例输出 **[!UICONTROL 空字符(\0000)]** 已选定： `Test,John,LastName`
* 示例输出 **[!UICONTROL 双引号(“)]** 已选定： `"Test","John","LastName"`

### 转义字符 {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="转义字符"
>abstract="设置一个用于在已被引号引起的值中将引号转义的字符。查看每个选择的示例文档。"

使用此选项可设置一个字符，用于在已加引号的值内转义引号。 例如，当字符串用双引号括起来时，此选项非常有用，因为字符串的一部分已用双引号括起来。 此选项确定要用哪个字符替换内双引号。 可用选项包括：

* 反斜杠 `(\)`
* 单引号 `(')`

#### 示例

通过UI中的每个选择，查看导出CSV文件中内容的以下示例。

* 示例输出 **[!UICONTROL 反斜杠`(\)`]** 已选定： `"Test,\"John\",LastName"`
* 示例输出 **[!UICONTROL 单引号`(')`]** 已选定： `"Test,'"John'",LastName"`

### 空值输出 {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="空值输出"
>abstract="使用此选项设置应如何在导出的 CSV 文件中表示空值。查看每个选择的示例文档。"

使用此控件可设置空值的字符串表示形式。 此选项确定空值在导出的CSV文件中的表示方式。 可用选项包括：

* **[!UICONTROL null]**
* **“”**
* **[!UICONTROL 空字符串]**

#### 示例

通过UI中的每个选择，查看导出CSV文件中内容的以下示例。

* 示例输出 **[!UICONTROL null]** 已选定： `male,NULL,TestLastName`. 在这种情况下，Experience Platform会将空值转换为null值。
* 示例输出 **“”** 已选定： `male,"",TestLastName`. 在这种情况下，Experience Platform将空值转换为一对双引号。
* 示例输出 **[!UICONTROL 空字符串]** 已选定： `male,,TestLastName`. 在这种情况下，Experience Platform将维护空值并按原样导出（不带双引号）。

>[!TIP]
>
>以下部分中的空值输出与null值输出的区别在于，空值具有空的实际值。 NULL值没有任何值。 将空值视为表上的空玻璃，将null值视为表上没有玻璃。

### null 值输出 {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="null 值输出"
>abstract="使用此选项设置应如何在导出的文件中表示 null 值。查看每个选择的示例文档。"

使用此选项设置应如何在导出的文件中表示 null 值。此选项确定在导出的CSV文件中如何表示null值。 可用选项包括：

* **[!UICONTROL null]**
* **&quot;&quot;**
* **[!UICONTROL 空字符串]**

#### 示例

通过UI中的每个选择，查看导出CSV文件中内容的以下示例。

* 示例输出 **[!UICONTROL null]** 已选定： `male,NULL,TestLastName`. 在这种情况下，不会进行任何转换并且CSV文件包含空值。
* 示例输出 **“”** 已选定： `male,"",TestLastName`. 在这种情况下，Experience Platform会在空字符串周围用双引号替换null值。
* 示例输出 **[!UICONTROL 空字符串]** 已选定： `male,,TestLastName`. 在这种情况下，Experience Platform会将null值替换为空字符串（不带双引号）。

### 压缩格式 {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="压缩格式"
>abstract="设置在将数据保存到文件时要使用何种压缩类型。支持的选项为 GZIP 和 NONE。查看每个选择的示例文档。"

设置在将数据保存到文件时要使用何种压缩类型。支持的选项为 GZIP 和 NONE。此选项确定是否要导出压缩文件。

### 编码

*未显示在UI屏幕快照中*. 指定保存的CSV文件的编码（字符集）。 选项为UTF-8或UTF-16。

### 用于转义引号的字符

*未显示在UI屏幕快照中*. 指示是否始终将包含引号的值包含在引号中的标志。

默认转义包含引号字符的所有值。

### 行分隔符

*未显示在UI屏幕快照中*. 定义用于编写的行分隔符。 最大长度为1个字符。

### 忽略前导空格

*未显示在UI屏幕快照中*. 指示是否应跳过导出值前导空格的标记。

示例输出 **[!UICONTROL True]** 已选定： `"male","John","TestLastName"`
示例输出 **[!UICONTROL False]** 已选定： `" male","John","TestLastName"`

### 忽略尾随空格

未显示在UI屏幕快照中。 指示是否应跳过导出值的尾随空格的标记。

示例输出 **[!UICONTROL True]** 已选定： `"male","John","TestLastName"`
示例输出 **[!UICONTROL False]** 已选定： `"male ","John","TestLastName"`

### 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何为CSV数据文件配置文件导出选项，以根据下游文件接收系统的要求定制文件内容。 接下来，您可以阅读 [基于文件的目标激活教程](/help/destinations/ui/activate-batch-profile-destinations.md) 以开始将文件导出到您首选的云存储位置。
