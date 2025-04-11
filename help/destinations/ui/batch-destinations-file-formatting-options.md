---
description: 了解在将数据激活到基于文件的目标时，如何配置文件格式选项
title: 为基于文件的目标配置文件格式选项
exl-id: f59b1952-e317-40ba-81d1-35535e132a72
source-git-commit: 4dd6e8685ff5cc61342b20e971216416918b95da
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 17%

---

# 为基于文件的目标配置文件格式选项

>[!IMPORTANT]
> 
>本文档中介绍的文件格式选项当前仅适用于CSV文件。

当您[连接](/help/destinations/ui/connect-destination.md)到基于文件的目标(如[Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect)、[Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)或[SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect))时，可以使用选项为导出的文件配置各种文件格式选项。

您可以使用Experience Platform UI为导出的文件配置各种文件格式选项。 您可以修改导出文件的几个属性，以匹配您这边文件接收系统的要求，从而以最佳方式读取和解读从Experience Platform收到的文件。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## CSV文件的文件格式配置 {#file-configuration}

要显示文件格式选项，请启动[连接到目标](/help/destinations/ui/connect-destination.md)工作流。 选择&#x200B;**数据类型：区段**&#x200B;和&#x200B;**文件类型：CSV**&#x200B;以显示可用于导出`CSV`文件的文件格式设置。

>[!IMPORTANT]
>
>您连接到的目标可能没有所有这些可用选项。 目标开发人员可以决定他们要在目标中支持哪些文件格式选项。 目标开发人员可以确定在连接到目标时可用的选项。 在Experience Platform UI中，必填选项标有星号。
> 
>Adobe构建的云存储目标 — [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)、[Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)、[Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)、[数据登陆区域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)、[Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)、[SFTP](/help/destinations/catalog/cloud-storage/sftp.md) — 当前仅支持下面突出显示的六个CSV选项。

![显示某些可用文件格式选项的图像。](../assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔符 {#delimiter}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_delimiter"
>title="分隔符"
>abstract="使用此控件为每个字段和值设置分隔符。查看每个选择的示例文档。"

使用此控件可以为导出的CSV文件中的每个字段和值设置分隔符。 可用选项包括：

* 冒号`(:)`
* 逗号`(,)`
* 管道`(|)`
* 分号`(;)`
* 选项卡`(\t)`

#### 示例

通过UI中的每个选择，查看导出CSV文件中内容的以下示例。

* 示例输出中选定了&#x200B;**[!UICONTROL 冒号`(:)`]**： `male:John:Doe`
* 示例输出中选定了&#x200B;**[!UICONTROL 逗号`(,)`]**： `male,John,Doe`
* 已选择&#x200B;**[!UICONTROL 管道`(|)`]**&#x200B;的示例输出： `male|John|Doe`
* 示例输出中选定了&#x200B;**[!UICONTROL 分号`(;)`]**： `male;John;Doe`
* 已选择&#x200B;**[!UICONTROL 选项卡`(\t)`]**&#x200B;的示例输出： `male \t John \t Doe`

### 引号字符 {#quote-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_quoteCharacter"
>title="引号字符"
>abstract="如果要从导出的字符串中删除双引号，请使用此选项。查看每个选择的示例文档。"

使用此选项可控制是应删除双引号还是应将其保留在导出的字符串中。

可用的选项包括：

* **[!UICONTROL Null字符(\0000)]**。 使用此选项可从导出的CSV文件中删除双引号。
* **[!UICONTROL 双引号(“)]**。 当字符串值包含分隔符或双引号时，请使用此选项。 此选项可帮助您在导出的CSV文件中保留分隔符或双引号，以便您能够正确识别哪个值对应于哪个字段。

#### 示例

考虑输入值`Anna,"Doe,John"`。

在UI中选择每个内容，查看导出CSV文件中的以下内容示例。

* 已选择&#x200B;**[!UICONTROL Null字符(\0000)]**&#x200B;的输出示例： `Anna,Doe,John`
* 示例输出中选定了&#x200B;**[!UICONTROL 双引号(&quot;)]**： `Anna,"Doe,John"`

### 转义字符 {#escape-character}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_escapeCharacter"
>title="转义字符"
>abstract="设置一个用于在已被引号引起的值中将引号转义的字符。查看每个选择的示例文档。"

使用此选项可设置一个字符，用于在已加引号的值内转义引号。 例如，当字符串用双引号括起来时，此选项非常有用，因为字符串的一部分已用双引号括起来。 此选项确定要替换内双引号的字符。 可用选项包括：

* 反斜杠`(\)`
* 单引号`(')`

#### 示例

在UI中选择每个内容，查看导出CSV文件中的以下内容示例。

* 示例输出&#x200B;**[!UICONTROL 反斜杠`(\)`]**&#x200B;已选定： `"Test,\"John\",LastName"`
* 已选择&#x200B;**[!UICONTROL 单引号`(')`]**&#x200B;的输出示例： `"Test,'"John'",LastName"`

### 空值输出 {#empty-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_emptyValueOutput"
>title="空值输出"
>abstract="使用此选项设置应如何在导出的 CSV 文件中表示空值。查看每个选择的示例文档。"

使用此控件可设置空值的字符串表示形式。 此选项确定在导出的CSV文件中如何表示空值。 可用选项包括：

* **[!UICONTROL Null (null)]**
* **双引号(“)**&#x200B;中的空字符串
* **[!UICONTROL 空字符串]**

#### 示例

在UI中选择每个内容，查看导出CSV文件中的以下内容示例。

* 已选择&#x200B;**[!UICONTROL null]**&#x200B;的示例输出： `male,NULL,TestLastName`。 在这种情况下，Experience Platform会将空值转换为null值。
* 已选择&#x200B;**“**”的示例输出： `male,"",TestLastName`。 在这种情况下，Experience Platform将空值转换为一对双引号。
* 已选择&#x200B;**[!UICONTROL 空字符串]**&#x200B;的示例输出： `male,,TestLastName`。 在这种情况下，Experience Platform将维护空值并按原样导出（不带双引号）。

>[!TIP]
>
>以下部分中的空值输出和空值输出之间的区别在于，空值具有空的实际值。 NULL值没有任何值。 将空值视为表上的空玻璃，将null值视为表上没有玻璃。

### null 值输出 {#null-value-output}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_nullValueOutput"
>title="null 值输出"
>abstract="使用此选项设置应如何在导出的文件中表示 null 值。查看每个选择的示例文档。"

使用此选项设置应如何在导出的文件中表示 null 值。此选项确定在导出的CSV文件中如何表示null值。 可用选项包括：

* **[!UICONTROL Null (null)]**
* **双引号(“)**&#x200B;中的空字符串
* **[!UICONTROL 空字符串]**

#### 示例

在UI中选择每个内容，查看导出CSV文件中的以下内容示例。

* 已选择&#x200B;**[!UICONTROL null]**&#x200B;的示例输出： `male,NULL,TestLastName`。 在这种情况下，不会进行任何转换，并且CSV文件包含null值。
* 已选择&#x200B;**“**”的示例输出： `male,"",TestLastName`。 在这种情况下，Experience Platform会在空字符串周围使用双引号替换空值。
* 已选择&#x200B;**[!UICONTROL 空字符串]**&#x200B;的示例输出： `male,,TestLastName`。 在这种情况下，Experience Platform会将null值替换为空字符串（不带双引号）。

### 压缩格式 {#compression-format}

>[!CONTEXTUALHELP]
>id="platform_destinations_csvOptions_compressionFormat"
>title="压缩格式"
>abstract="设置在将数据保存到文件时要使用何种压缩类型。支持的选项为 GZIP 和 NONE。查看每个选择的示例文档。"

设置在将数据保存到文件时要使用何种压缩类型。支持的选项为 GZIP 和 NONE。此选项确定您是否将导出压缩文件。

### 编码

*未显示在用户界面屏幕快照中*。 指定保存的CSV文件的编码（字符集）。 选项为UTF-8或UTF-16。

### 用于转义引号的字符

*未显示在用户界面屏幕快照中*。 指示是否始终将包含引号的值包含在引号中的标志。

默认转义包含引号字符的所有值。

### 行分隔符

*未显示在用户界面屏幕快照中*。 定义用于编写的行分隔符。 最大长度为1个字符。

### 忽略前导空格

*未显示在用户界面屏幕快照中*。 指示是否应跳过导出值前导空格的标记。

已选择&#x200B;**[!UICONTROL True]**&#x200B;的示例输出： `"male","John","TestLastName"`
已选择**[!UICONTROL False]**&#x200B;的示例输出： `" male","John","TestLastName"`

### 忽略尾随空格

未显示在UI屏幕快照中。 指示是否应跳过导出值的尾随空格标志。

已选择&#x200B;**[!UICONTROL True]**&#x200B;的示例输出： `"male","John","TestLastName"`
已选择**[!UICONTROL False]**&#x200B;的示例输出： `"male ","John","TestLastName"`

### 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何为CSV数据文件配置文件导出选项，以根据下游文件接收系统的要求定制文件内容。 接下来，您可以阅读[基于文件的目标激活教程](/help/destinations/ui/activate-batch-profile-destinations.md)，以开始将文件导出到您首选的云存储位置。
