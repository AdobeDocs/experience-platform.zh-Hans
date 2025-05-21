---
title: 使用UI将MariaDB连接到Experience Platform
description: 了解如何使用Experience Platform用户界面中的源工作区将您的MariaDB帐户连接到Experience Platform。
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 使用UI将[!DNL MariaDB]连接到Experience Platform

阅读本指南，了解如何使用Experience Platform用户界面中的源工作区将您的[!DNL MariaDB]帐户连接到Adobe Experience Platform。

## 开始使用

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [实时客户个人资料](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时客户个人资料。

如果您已经有[!DNL MariaDB]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL MariaDB] 概述](../../../../connectors/databases/mariadb.md#prerequisites)。

## 导航源目录

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;*[!UICONTROL 源]*&#x200B;工作区。 在&#x200B;*[!UICONTROL 类别]*&#x200B;面板中选择相应的类别或者，使用搜索栏导航到要使用的特定源。

若要使用[!DNL MariaDB]，请选择&#x200B;*[!UICONTROL 数据库]*&#x200B;下的&#x200B;**[!UICONTROL MariaDB]**&#x200B;源卡，然后选择&#x200B;**[!UICONTROL 设置]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 创建经过身份验证的帐户后，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![选择了MariaDB卡的UI中的源目录。](../../../../images/tutorials/create/maria-db/catalog.png)

## 使用现有帐户 {#existing}

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后选择要使用的[!DNL MariaDB]帐户。

![源工作流中已选择“现有帐户”的现有帐户接口。](../../../../images/tutorials/create/maria-db/existing.png)

## 创建新帐户 {#create}

如果您没有现有帐户，则必须通过提供与您的源对应的必需身份验证凭据来创建新帐户。

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后提供名称并选择性地为您的帐户添加描述。

![源工作流中的新帐户接口，提供了帐户名称和可选描述。](../../../../images/tutorials/create/maria-db/new.png)

### 连接到Experience Platform

您可以使用帐户密钥或基本身份验证将您的[!DNL MariaDB]帐户连接到Experience Platform。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

若要使用帐户密钥身份验证，请选择&#x200B;**[!UICONTROL 帐户密钥身份验证]**，提供您的[连接字符串](../../../../connectors/databases/mariadb.md#azure)，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流中的新帐户接口已选择“帐户密钥身份验证”。](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB 基本身份验证]

若要使用基本身份验证，请选择&#x200B;**[!UICONTROL 基本身份验证]**，提供[身份验证凭据](../../../../connectors/databases/mariadb.md#azure)的值，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![源工作流程中的新帐户接口选择了“基本身份验证”。](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

通过学习本教程，您已建立与[!DNL MariaDB]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/databases.md)。
