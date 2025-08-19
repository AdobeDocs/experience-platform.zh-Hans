---
title: 在UI中将Azure Blob Storage连接到Experience Platform
description: 了解如何使用UI中的源工作区将您的Azure Blob Storage帐户连接到Experience Platform。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# 使用UI将[!DNL Azure Blob Storage]连接到Experience Platform

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL Azure Blob Storage]实例连接到Adobe Experience Platform。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于在Experience Platform中组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Azure Blob Storage]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 支持的文件格式

Experience Platform支持从外部存储摄取以下文件格式：

* 分隔符分隔值(DSV)：可使用任何单列分隔符（如制表符、逗号、竖线、分号或哈希）收集任何格式的平面文件。
* JavaScript对象表示法(JSON)： JSON格式的数据文件必须符合XDM。
* Apache Parquet： Parquet格式的数据文件必须符合XDM。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Azure Blob Storage] 概述](../../../../connectors/cloud-storage/blob.md#authentication)。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 选择类别或使用搜索栏查找您的源。

若要连接到[!DNL Azure Blob Storage]，请转到&#x200B;*[!UICONTROL 云存储]*&#x200B;类别，选择&#x200B;**[!UICONTROL Azure Blob存储]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>源显示&#x200B;**[!UICONTROL 为新连接设置]**，如果帐户已存在，则显示&#x200B;**[!UICONTROL 添加数据]**。

![已选择Azure Blob存储源的源目录。](../../../../images/tutorials/create/blob/catalog.png)

## 使用现有帐户

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL Azure Blob Storage]帐户。

![Azure Blob存储的现有源接口。](../../../../images/tutorials/create/blob/existing.png)

## 创建新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。 您可以使用以下身份验证类型将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform：

* **帐户密钥身份验证**：使用存储帐户的访问密钥进行身份验证并连接到您的[!DNL Azure Blob Storage]帐户。
* **共享访问签名(SAS)**：使用SAS URI为您的[!DNL Azure Blob Storage]帐户中的资源提供委派的、有时间限制的访问。
* **基于服务主体的身份验证**：使用Azure Active Directory (AAD)服务主体（客户端ID和密码）对您的Azure Blob存储帐户进行安全身份验证。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

选择&#x200B;**[!UICONTROL 帐户密钥身份验证]**&#x200B;并提供您的`connectionString`、`container`和`folderPath`。 接下来，选择&#x200B;**[!UICONTROL 连接到源]**，并等待一段时间以建立连接。

![新帐户创建步骤中的帐户密钥身份验证选项。](../../../../images/tutorials/create/blob/account-key.png)

>[!TAB 共享访问签名]

选择&#x200B;**[!UICONTROL 共享访问签名]**&#x200B;并提供您的`sasUri`、`container`和`folderPath`。 接下来，选择&#x200B;**[!UICONTROL 连接到源]**，并等待一段时间以建立连接。

![新帐户创建步骤中的共享访问签名身份验证选项。](../../../../images/tutorials/create/blob/sas.png)

>[!TAB 基于服务主体的身份验证]

选择&#x200B;**[!UICONTROL 基于服务主体的身份验证]**&#x200B;并提供您的`serviceEndpoint`、`servicePrincipalId`、`servicePrincipalKey`、`accountKind`、`tenant`、`container`和`folderPath`。 接下来，选择&#x200B;**[!UICONTROL 连接到源]**，并等待一段时间以建立连接。

![新帐户创建步骤中基于服务主体的身份验证选项。](../../../../images/tutorials/create/blob/service-principal.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与[!DNL Azure Blob Storage]帐户的连接。 您现在可以继续阅读下一教程，并[配置数据流以将数据从云存储引入Experience Platform](../../dataflow/batch/cloud-storage.md)。
