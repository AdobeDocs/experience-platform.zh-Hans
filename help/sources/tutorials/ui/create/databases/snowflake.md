---
keywords: Experience Platform；主页；热门主题；Snowflake
title: 在UI中创建Snowflake源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Snowflake源连接。
source-git-commit: 2e717f33b487430220bd3bb7812558cde81d8852
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---

# 在UI中创建[!DNL Snowflake]源连接

>[!NOTE]
>
> [!DNL Snowflake]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Snowflake]源连接器的步骤。

## 快速入门

本教程需要对Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要在[!DNL Platform]上访问您的Snowflake帐户，必须提供以下身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 帐户 | 要连接到平台的[!DNL Snowflake]帐户。 |
| 仓库 | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Platform时必须单独进行访问。 |
| 数据库 | [!DNL Snowflake]包含要引入平台的数据。 |
| 用户名 | [!DNL Snowflake]帐户的用户名。 |
| 密码 | [!DNL Snowflake]用户帐户的密码。 |
| 连接字符串 | 用于连接到[!DNL Snowflake]实例的连接字符串。 [!DNL Snowflake]的连接字符串模式为`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |

有关这些值的更多信息，请参阅[此Snowflake文档](https://docs.snowflake.com/en/user-guide/oauth-custom.html)。

## 连接您的Snowflake帐户

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了您可以使用创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在[!UICONTROL Databases]类别下，选择&#x200B;**[!UICONTROL Snowflake]**，然后选择&#x200B;**[!UICONTROL Add data]**。

![](../../../../images/tutorials/create/snowflake/catalog.png)

出现&#x200B;**[!UICONTROL 连接到Snowflake]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Snowflake帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![](../../../../images/tutorials/create/snowflake/existing.png)

### 新帐户

如果您使用的是新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入窗体中，提供名称、可选描述和您的Snowflake凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后允许一些时间建立新连接。

![](../../../../images/tutorials/create/snowflake/new.png)

## 后续步骤

通过阅读本教程，您已建立与Snowflake帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。
