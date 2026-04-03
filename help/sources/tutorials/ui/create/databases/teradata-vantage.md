---
keywords: Experience Platform；主页；热门主题；Teradata Vantage
title: 在UI中创建Teradata Vantage Source连接
description: 了解如何使用Teradata UI创建Adobe Experience Platform Vantage源连接。
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 2%

---

# 在用户界面中创建[!DNL Teradata Vantage]源连接

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Teradata Vantage]源连接器的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要在Experience Platform上访问您的[!DNL Teradata Vantage]帐户，必须提供以下身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 连接字符串 | 连接字符串是一个字符串，它提供有关数据源以及如何连接到该数据源的信息。 [!DNL Teradata Vantage]的连接字符串模式为`DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`。 |

有关入门的详细信息，请参阅此[[!DNL Teradata Vantage] 文档](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options)。

## 连接您的[!DNL Teradata Vantage]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在[!UICONTROL Databases]类别下，选择&#x200B;**[!UICONTROL Teradata Vantage]**，然后选择&#x200B;**[!UICONTROL Set up]**。

>[!TIP]
>
>当给定的源尚未拥有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL Set up]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL Add data]**。

![已选择Teradata Vantage源的源目录。](../../../../images/tutorials/create/teradata/catalog.png)

此时会显示&#x200B;**[!UICONTROL Connect to Teradata Vantage]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要连接现有帐户，请选择要连接的[!DNL Teradata Vantage]帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![源工作区中的现有帐户页面。](../../../../images/tutorials/create/teradata/existing.png)

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL Teradata Vantage]凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后留出一些时间来建立新连接。

![源工作区中的新帐户创建界面。](../../../../images/tutorials/create/teradata/new.png)

## 后续步骤

通过学习本教程，您已建立与Teradata Vantage帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/databases.md)。
