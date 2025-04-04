---
keywords: Experience Platform；主页；热门主题；mysql；MySQL
solution: Experience Platform
title: 在UI中创建MySQL Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform用户界面创建MySQL源连接。
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# 在用户界面中创建[!DNL MySQL]源连接

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用Adobe Experience Platform UI创建[!DNL MySQL]源连接的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经有[!DNL MySQL]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需的凭据

要在[!DNL Experience Platform]上访问您的[!DNL MySQL]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的帐户关联的[!DNL MySQL]连接字符串。 [!DNL MySQL]连接字符串模式为： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 通过阅读[[!DNL MySQL] 文档](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)，您可以了解有关连接字符串以及如何获取它们的更多信息。 |

## 连接您的[!DNL MySQL]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL MySQL]帐户关联到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

在&#x200B;**[!UICONTROL 数据库]**&#x200B;类别下，选择&#x200B;**[!UICONTROL MySQL]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的[!DNL MySQL]连接器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到MySQL]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL MySQL]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/my-sql/new.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL MySQL]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/my-sql/existing.png)

## 后续步骤

通过学习本教程，您已建立与MySQL帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/databases.md)。
