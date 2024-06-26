---
keywords: Experience Platform；主页；热门主题；Maria DB；maria db
solution: Experience Platform
title: 在UI中创建MariaDB源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Maria DB源连接。
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 创建 [!DNL MariaDB] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用创建Maria DB源连接器的步骤。 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [Real-time Customer Profile](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有 [!DNL MariaDB] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

要访问您的 [!DNL MariaDB] 帐户于 [!DNL Platform]，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与MariaDB身份验证关联的连接字符串。 此 [!DNL MariaDB] 连接字符串模式为： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

有关入门的更多信息，请参阅此 [[!DNL MariaDB] 文档](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## 连接您的 [!DNL Maria DB] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Maria DB] 目标帐户 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

在 **[!UICONTROL 数据库]** 类别，选择 **[!UICONTROL Maria DB]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL Maria DB] 连接器。

![](../../../../images/tutorials/create/maria-db/catalog.png)

此 **[!UICONTROL 连接到Maria DB]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL MariaDB] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/maria-db/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL MariaDB] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/maria-db/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL MariaDB] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
