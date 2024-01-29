---
title: 在UI中创建Snowflake源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Snowflake源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# 创建 [!DNL Snowflake] UI中的源连接

>[!IMPORTANT]
>
>此 [!DNL Snowflake] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了用于创建 [!DNL Snowflake] 源连接器，使用Adobe Experience Platform用户界面。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

必须提供以下凭据属性的值才能验证您的 [!DNL Snowflake] 源。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

| 凭据 | 描述 |
| ---------- | ----------- |
| 帐户 | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须唯一标识跨不同帐户的帐户 [!DNL Snowflake] 组织。 要实现此目的，您必须在帐户名称前添加组织名称。 例如：`orgname-account_name`。有关帐户名称的更多信息，请阅读 [!DNL Snowflake] 文档 [帐户标识符](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| 仓库 | 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 数据仓库相互独立，在将数据传送到Platform时必须单独进行访问。 |
| 数据库 | 此 [!DNL Snowflake] 数据库包含您要带入Platform的数据。 |
| 用户名 | 的用户名 [!DNL Snowflake] 帐户。 |
| 密码 | 的密码 [!DNL Snowflake] 用户帐户。 |
| 角色 | 在中使用的默认访问控制角色 [!DNL Snowflake] 会话。 该角色应为已分配给指定用户的现有角色。 默认角色为 `PUBLIC`. |
| 连接字符串 | 用于连接到 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 密钥对身份验证]

要使用密钥对身份验证，您必须生成一个2048位RSA密钥对，然后在创建帐户时提供以下值 [!DNL Snowflake] 源。

| 凭据 | 描述 |
| --- | --- |
| 帐户 | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须唯一标识跨不同帐户的帐户 [!DNL Snowflake] 组织。 要实现此目的，您必须在帐户名称前添加组织名称。 例如：`orgname-account_name`。有关帐户名称的更多信息，请阅读 [!DNL Snowflake] 文档 [帐户标识符](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| 用户名 | 您的用户名 [!DNL Snowflake] 帐户。 |
| 私钥 | 此 [!DNL Base64-]已编码私钥的 [!DNL Snowflake] 帐户。 您可以生成加密或未加密的私钥。 如果您使用的是加密的私钥，那么在针对Experience Platform进行身份验证时，您还必须提供私钥密码。 |
| 私钥密码 | 私钥密码是附加的安全层，在使用加密的私钥进行身份验证时必须使用该安全层。 如果您使用未加密的私钥，则无需提供密码。 |
| 数据库 | 此 [!DNL Snowflake] 包含要摄取到Experience Platform的数据的数据库。 |
| 仓库 | 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 数据仓库相互独立，在将数据传送到Platform时必须单独进行访问。 |

有关这些值的更多信息，请参阅 [此Snowflake文档](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

要在Experience Platform上访问您的Snowflake帐户，您必须提供以下身份验证值：

>[!NOTE]
>
>您必须设置 `PREVENT_UNLOAD_TO_INLINE_URL` 标记到 `FALSE` 允许从卸载数据 [!DNL Snowflake] Experience Platform数据库。

## 连接您的Snowflake帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 数据库] 类别，选择 **[!UICONTROL Snowflake]** 然后选择 **[!UICONTROL 添加数据]**.

![源目录 [!DNL Snowflake] 突出显示。](../../../../images/tutorials/create/snowflake/catalog.png)

此 **[!UICONTROL 连接到Snowflake]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL Snowflake] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中的现有帐户界面。](../../../../images/tutorials/create/snowflake/existing.png)

### 新帐户

要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新页面提供名称和可选描述 [!DNL Snowflake] 帐户。

![源工作流程中的新帐户界面。](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

要使用帐户密钥身份验证，请在输入表单中提供您的连接字符串，然后选择 **[!UICONTROL 连接到源]**.

![帐户密钥身份验证界面。](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB 密钥对身份验证]

要使用密钥对验证，请提供帐户、用户名、私钥、私钥密码、数据库和仓库的值，然后选择 **[!UICONTROL 连接到源]**.

![帐户密钥对身份验证界面。](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已与Snowflake帐户建立了连接。 您现在可以继续下一教程和 [配置数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md).
