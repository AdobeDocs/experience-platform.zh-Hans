---
keywords: Experience Platform；主页；热门主题；mysql;MySQL
solution: Experience Platform
title: 在UI中创建MySQL源连接
topic: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建MySQL源连接。
translation-type: tm+mt
source-git-commit: 8851e11e956b393e56714d4d48870b7f68947c18
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---


# 在UI中创建[!DNL MySQL]源连接

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用Adobe Experience Platform UI创建[!DNL MySQL]源连接的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已有[!DNL MySQL]连接，则可以跳过此文档的其余部分，继续学习有关[配置数据流](../../dataflow/databases.md)的教程。

### 收集所需凭据

要访问[!DNL Platform]上的[!DNL MySQL]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的帐户关联的[!DNL MySQL]连接字符串。 [!DNL MySQL]连接字符串模式为：`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 您可以阅读[[!DNL MySQL] 文档](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)，进一步了解连接字符串以及如何获取它们。 |

## 连接您的[!DNL MySQL]帐户

收集所需凭据后，您可以按照以下步骤将您的[!DNL MySQL]帐户链接到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;**[!UICONTROL Sources]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了可为其创建帐户的各种源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;类别下，选择&#x200B;**[!UICONTROL MySQL]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL Configure]**。 否则，选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新[!DNL MySQL]连接器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to MySQL]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供名称、可选说明和[!DNL MySQL]凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

![](../../../../images/tutorials/create/my-sql/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL MySQL]帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![](../../../../images/tutorials/create/my-sql/existing.png)

## 后续步骤

通过本教程，您已建立了与MySQL帐户的连接。 您现在可以继续下一个教程，并[配置一个数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。