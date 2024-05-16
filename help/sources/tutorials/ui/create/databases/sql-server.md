---
title: 在UI中创建Microsoft SQL Server源连接
description: 了解如何使用Adobe Experience Platform UI创建Microsoft SQL Server源连接。
exl-id: aba4e317-1c59-4999-a525-dba15f8d4df9
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 创建 [!DNL Microsoft SQL Server] UI中的源连接

阅读本教程，了解如何连接 [!DNL Microsoft SQL Server] 使用用户界面登录到Adobe Experience Platform的帐户。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL SQL Server] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/databases.md).

### 收集所需的凭据

为了连接到 [!DNL SQL Server] 日期 [!DNL Platform]中，您必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| 连接字符串 | 与您的关联的连接字符串 [!DNL Microsoft SQL Server] 帐户。 您的连接字符串模式取决于您是使用服务器名称还是实例名称作为数据源：<ul><li>使用服务器名的连接字符串： `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>使用实例名称的连接字符串：`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |

有关入门的更多信息，请参阅 [此 [!DNL SQL Server] 文档](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

## 连接您的 [!DNL SQL Server] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *数据库* 类别，选择 **[!DNL Microsoft SQL Server]**，然后选择 **[!UICONTROL 设置]**.

>[!TIP]
>
>源目录中的源显示 **[!UICONTROL 设置]** 选项。 经过身份验证的帐户存在后，此选项将更改为 **[!UICONTROL 添加数据]**.

![已选择Microsoft SQL Server源的源目录。](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

此 **[!UICONTROL 连接到Microsoft SQL Server]** 页面。 在此页上，您可以使用新凭据或现有凭据。

>[!BEGINTABS]

>[!TAB 创建新帐户]

要创建新帐户，请选择 **[!UICONTROL 新帐户]** 并提供名称、可选描述和您的凭据。

完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![输入并突出显示源连接详细信息的新帐户界面。](../../../../images/tutorials/create/microsoft-sql-server/new.png)

>[!TAB 使用现有帐户]

要使用现有帐户，请选择 **[!UICONTROL 现有帐户]** 然后从现有帐户目录中选择要使用的帐户。

选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![显示现有帐户列表的现有帐户界面。](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL SQL Server] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md).
