---
description: 了解如何在将数据激活到基于文件的目标时配置文件格式选项
title: （测试版）为基于文件的目标配置文件格式选项
source-git-commit: 23a7a1997e05d2bde26de5b73a23ea051bf2b3bb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# （测试版）为基于文件的目标配置文件格式选项

>[!IMPORTANT]
>
>的 **[!UICONTROL 文件格式选项]** Adobe Experience Platform中的功能目前处于测试阶段。 文档和功能可能会发生更改。
>请联系您的Adobe代表以获取此功能的访问权限。
> 
>本文档中描述的文件格式选项当前仅适用于CSV文件。

当您 [connect](/help/destinations/ui/connect-destination.md) 到基于文件的目标，例如 [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md#connect), [Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md#connect)或 [SFTP](/help/destinations/catalog/cloud-storage/sftp.md#connect).

您可以使用Experience PlatformUI为导出的文件配置各种文件格式选项。 您可以修改导出文件的多个属性，以符合您所在方的文件接收系统的要求，以便以最佳方式读取和解释从Experience Platform接收的文件。

<!--
* To configure file formatting options for exported files by using the Experience Platform UI, read this document.
* To configure file formatting options for exported files by using the Experience Platform Flow Service API, read [Flow Service API - Destinations](https://developer.adobe.com/experience-platform-apis/references/destinations/).
-->

## 文件格式配置 {#file-configuration}

>[!IMPORTANT]
>
>您连接到的目标可能并没有所有这些选项可用。 由目标开发人员决定他们要在其目标中支持的文件格式选项。 目标开发人员可以确定在连接到目标时哪些选项可用。 在Experience PlatformUI中，必需选项带有星号标记。

要显示文件格式选项，请启动 [连接到目标](/help/destinations/ui/connect-destination.md) 工作流和选择区段作为 **文件类型**. 本节介绍可用于导出的文件格式设置 `CSV` 文件。

![显示一些可用文件格式选项的图像。](/help/destinations/assets/ui/batch-destinations-file-formatting-options/file-formatting-options.png)

### 分隔符

为每个字段和值设置分隔符。 例如， `,` (以逗号分隔值或 `/t` 的值。

### 引号字符

设置一个用于转义引号值的字符，其中分隔符可以是值的一部分。

### 转义字符

设置一个用于在已引号值内转义引号的字符。

### 空值输出

设置空值的字符串表示形式。

### Null值输出

在导出的文件中设置空值的字符串表示形式。

示例输出 **[!UICONTROL null]** 选定项： `male,NULL,TestLastName`
示例输出 **&quot;** 选定项： `male,"",TestLastName`
示例输出 **[!UICONTROL 空字符串]** 选定项： `male,,TestLastName`

### 压缩格式

设置在将数据保存到文件时要使用的压缩编解码器。 支持的选项包括GZIP和NONE。

### 编码

*UI屏幕截图中未显示*. 指定保存的CSV文件的编码（字符集）。 选项为UTF-8或UTF-16。

### Char转义引号

*UI屏幕截图中未显示*. 指示包含引号的值是否应始终用引号括起来的标记。

默认值是对包含引号字符的所有值进行转义。

### 行分隔符

*UI屏幕截图中未显示*. 定义应用于写入的行分隔符。 最大长度为1个字符。

### 忽略前导空格

*UI屏幕截图中未显示*. 指示是否应跳过导出值中的前导空格的标记。

示例输出 **[!UICONTROL True]** 选定项： `"male","John","TestLastName"`
示例输出 **[!UICONTROL False]** 选定项： `" male","John","TestLastName"`

### 忽略尾随空格

未在UI屏幕截图中显示。 指示是否应跳过导出值的尾随空格的标记。

示例输出 **[!UICONTROL True]** 选定项： `"male","John","TestLastName"`
示例输出 **[!UICONTROL False]** 选定项： `"male ","John","TestLastName"`

### 后续步骤 {#next-steps}

阅读本文档后，您现在知道如何为CSV数据文件配置文件导出选项，以根据下游文件接收系统的要求定制文件内容。 接下来，您可以阅读 [基于文件的目标激活教程](/help/destinations/ui/activate-batch-profile-destinations.md) 开始将文件导出到首选的云存储位置。
