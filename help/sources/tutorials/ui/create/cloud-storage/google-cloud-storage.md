---
title: 在UI中创建Google云存储源连接
description: 了解如何使用Google UI创建Adobe Experience Platform Cloud Storage源连接。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# 创建 [!DNL Google Cloud Storage] UI中的源连接

本教程提供了用于创建 [!DNL Google Cloud Storage] 源连接(使用Adobe Experience Platform UI)。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Google Cloud Storage] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/batch/cloud-storage.md).

### 支持的文件格式

[!DNL Experience Platform] 支持从外部存储摄取的以下文件格式：

* 分隔符分隔值(DSV)：任何单字符值都可以用作DSV格式数据文件的分隔符。
* JavaScript对象表示法(JSON)： JSON格式的数据文件必须与XDM兼容。
* Apache Parquet： Parquet格式的数据文件必须与XDM兼容。

### 收集所需的凭据

要访问您的 [!DNL Google Cloud Storage] 数据，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 访问密钥ID | 61个字符的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。 |
| 访问密钥 | 40个字符的base-64编码字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。 |
| 存储桶名称 | 您的名称 [!DNL Google Cloud Storage] 桶。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| 文件夹路径 | 要提供访问权限的文件夹的路径。 |

有关这些值的更多信息，请参见 [Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有关如何生成您自己的访问密钥ID和秘密访问密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Google Cloud Storage] Platform帐户。

## 连接您的 [!DNL Google Cloud Storage] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 以访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Google云存储]** 然后选择 **[!UICONTROL 添加数据]**.

![显示源目录页面的Platform UI屏幕。](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此 **[!UICONTROL 连接到Google云存储]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择 [!DNL Google Cloud Storage] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![Platform UI屏幕显示Google云存储源的现有帐户页面](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Google Cloud Storage] 凭据。 在此步骤中，您还可以通过定义子文件夹的路径名称来指定您的帐户将有权访问的子文件夹。

完成后，选择 **[!UICONTROL 连接到源]** 然后留出一些时间来建立新连接。

![Platform UI屏幕显示Google Cloud Storage源的新帐户页面。](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 后续步骤

按照本教程，您已建立与的连接 [!DNL Google Cloud Storage] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md).
