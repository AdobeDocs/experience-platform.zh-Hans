---
keywords: Experience Platform;home;popular topics;Microsoft SQL Server;SQL Server;sql server
solution: Experience Platform
title: 在UI中创建Microsoft SQL Server源连接器
topic: overview
description: 本教程提供了使用平台用户界面创建Microsoft SQL Server（以下称“SQL Server”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# 在UI [!DNL Microsoft SQL Server] 中创建源连接器

>[!NOTE]
>
> 连接 [!DNL Microsoft SQL Server] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Microsoft SQL Server] 户界面创建(下[!DNL SQL Server]称“”)源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL SQL Server] 接，您可以跳过此文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要在上连接 [!DNL SQL Server] ，必 [!DNL Platform]须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的帐户关联的连接 [!DNL SQL Server] 字符串。 连接 [!DNL SQL Server] 字符串模式为： `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

有关快速入门的详细信息，请参 [ [!DNL SQL Server] 阅本文档](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)。

## 连接帐 [!DNL SQL Server] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL SQL Server] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别 **[!UICONTROL 下，选择Microsoft SQL Server]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL SQL Server] 接器。

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

将 **[!UICONTROL 显示“连接到Microsoft SQL Server]** ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL SQL Server] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL SQL Server] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL SQL Server] 连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。