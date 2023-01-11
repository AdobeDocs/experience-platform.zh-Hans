---
keywords: Experience Platform；主页；热门主题；Snowflake
title: 在UI中创建Snowflake源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Snowflake源连接。
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# 创建 [!DNL Snowflake] UI中的源连接

本教程提供了创建 [!DNL Snowflake] 源连接器。

## 快速入门

本教程需要对Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要访问您的Snowflake帐户，请执行以下操作： [!DNL Platform]，则必须提供以下身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 帐户 | 与您的 [!DNL Snowflake] 帐户。 完全合格 [!DNL Snowflake] 帐户名称包括您的帐户名称、地区和云平台。 例如：`cj12345.east-us-2.azure`。有关帐户名称的更多信息，请参阅此 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| 仓库 | 的 [!DNL Snowflake] 仓库管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 仓库彼此独立，在将数据移至Platform时必须单独进行访问。 |
| 数据库 | 的 [!DNL Snowflake] 数据库包含要引入平台的数据。 |
| 用户名 | 的用户名 [!DNL Snowflake] 帐户。 |
| 密码 | 的密码 [!DNL Snowflake] 用户帐户。 |
| 连接字符串 | 用于连接到的连接字符串 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

有关这些值的更多信息，请参阅 [此Snowflake文档](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## 连接您的Snowflake帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以为其创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL Snowflake]** 然后选择 **[!UICONTROL 添加数据]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

的 **[!UICONTROL 连接到Snowflake]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Snowflake帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/snowflake/existing.png)

### 新帐户

如果您使用新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入窗体中，提供名称、可选描述和您的Snowflake凭据。 完成后，选择 **[!UICONTROL 连接]** 然后，再留出一些时间建立新连接。

![](../../../../images/tutorials/create/snowflake/new.png)

## 后续步骤

通过阅读本教程，您已建立与Snowflake帐户的连接。 您现在可以继续下一个教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
