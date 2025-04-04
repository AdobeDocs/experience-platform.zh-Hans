---
title: 在UI中创建Google Cloud Storage Source连接
description: 了解如何使用Google UI创建Adobe Experience Platform Cloud Storage源连接。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---

# 在用户界面中创建[!DNL Google Cloud Storage]源连接

本教程提供了使用Adobe Experience Platform UI创建[!DNL Google Cloud Storage]源连接的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Google Cloud Storage]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 支持的文件格式

[!DNL Experience Platform]支持从外部存储摄取的以下文件格式：

* 分隔符分隔值(DSV)：任何单字符值都可以用作DSV格式的数据文件的分隔符。
* JavaScript对象表示法(JSON)： JSON格式的数据文件必须符合XDM。
* Apache Parquet： Parquet格式的数据文件必须符合XDM。

### 收集所需的凭据

要在Experience Platform上访问[!DNL Google Cloud Storage]数据，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 访问密钥 ID | 一个由61个字符组成的字母数字字符串，用于向Experience Platform验证您的[!DNL Google Cloud Storage]帐户。 |
| 访问密钥 | 用于向Experience Platform验证您的[!DNL Google Cloud Storage]帐户的40个字符Base-64编码字符串。 |
| 存储桶名称 | [!DNL Google Cloud Storage]存储段的名称。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| 文件夹路径 | 要提供访问权限的文件夹的路径。 |

有关这些值的更多信息，请参阅[Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有关如何生成自己的访问密钥ID和访问密钥的步骤，请参阅[[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md)。

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Google Cloud Storage]帐户关联到Experience Platform。

## 连接您的[!DNL Google Cloud Storage]帐户

在Experience Platform UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL 云存储]类别下，选择&#x200B;**[!UICONTROL Google云存储]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![Experience Platform UI屏幕显示源目录页面。](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Google Cloud Storage]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL Google Cloud Storage]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![Experience Platform UI屏幕显示Google Cloud Storage源的现有帐户页面](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Google Cloud Storage]凭据。 在此步骤中，您还可以通过定义子文件夹的路径名称来指定帐户将有权访问的子文件夹。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![Experience Platform UI屏幕显示Google Cloud Storage源的新帐户页面。](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 后续步骤

通过学习本教程，您已建立与[!DNL Google Cloud Storage]帐户的连接。 您现在可以继续阅读下一教程，并[配置数据流以将数据从云存储引入Experience Platform](../../dataflow/batch/cloud-storage.md)。
