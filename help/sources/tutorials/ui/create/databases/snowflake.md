---
title: 在UI中创建Snowflake源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Snowflake源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 669b47753a9c9400f22aa81d08a4d25bb5e414c5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# 创建 [!DNL Snowflake] UI中的源连接

>[!IMPORTANT]
>
>此 [!DNL Snowflake] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了用于创建 [!DNL Snowflake] 源连接器，使用Adobe Experience Platform用户界面。

## 快速入门

本教程需要深入了解Platform的以下组件：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

若要访问您的Snowflake帐户，请 [!DNL Platform]中，您必须提供以下身份验证值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 帐户 | 与您的关联的完整帐户名称 [!DNL Snowflake] 帐户。 完全合格的 [!DNL Snowflake] 帐户名称包括您的帐户名称、区域和云平台。 例如：`cj12345.east-us-2.azure`。有关帐户名称的更多信息，请参阅此 [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| 仓库 | 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 仓库相互独立，在将数据传送到Platform时必须单独访问。 |
| 数据库 | 此 [!DNL Snowflake] 数据库包含要带入Platform的数据。 |
| 用户名 | 的用户名 [!DNL Snowflake] 帐户。 |
| 密码 | 的密码 [!DNL Snowflake] 用户帐户。 |
| 角色 | 在中使用的默认访问控制角色 [!DNL Snowflake] 会话。 该角色应为已分配给指定用户的现有角色。 默认角色为 `PUBLIC`. |
| 连接字符串 | 用于连接到 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

有关这些值的更多信息，请参阅 [此Snowflake文档](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!NOTE]
>
>您必须设置 `PREVENT_UNLOAD_TO_INLINE_URL` 标记到 `FALSE` 允许从卸载数据 [!DNL Snowflake] 要Experience Platform的数据库。

## 连接您的Snowflake帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL Snowflake]** 然后选择 **[!UICONTROL 添加数据]**.

![](../../../../images/tutorials/create/snowflake/catalog.png)

此 **[!UICONTROL 连接到Snowflake]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Snowflake帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/snowflake/existing.png)

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在显示的输入表单上，提供名称、可选描述和您的Snowflake凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/snowflake/new.png)

## 后续步骤

通过学习本教程，您已建立与Snowflake帐户的连接。 您现在可以继续下一教程和 [配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md).
