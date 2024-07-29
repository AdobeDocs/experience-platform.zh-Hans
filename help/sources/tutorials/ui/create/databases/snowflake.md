---
title: 在UI中创建SnowflakeSource连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Snowflake源连接。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: d89e0c81bd250e41a863b8b28d358cc6ddea1c37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 4%

---

# 在用户界面中创建[!DNL Snowflake]源连接

>[!IMPORTANT]
>
>[!DNL Snowflake]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Snowflake]源连接器的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

必须提供以下凭据属性的值才能对您的[!DNL Snowflake]源进行身份验证。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

| 凭据 | 描述 |
| ---------- | ----------- |
| 帐户 | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| 仓库 | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Platform时必须单独访问。 |
| 数据库 | [!DNL Snowflake]数据库包含要带入Platform的数据。 |
| 用户名 | [!DNL Snowflake]帐户的用户名。 |
| 密码 | [!DNL Snowflake]用户帐户的密码。 |
| 角色 | 在[!DNL Snowflake]会话中使用的默认访问控制角色。 该角色应为已分配给指定用户的现有角色。 默认角色为`PUBLIC`。 |
| 连接字符串 | 用于连接到[!DNL Snowflake]实例的连接字符串。 [!DNL Snowflake]的连接字符串模式为`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 密钥对身份验证]

要使用密钥对身份验证，您必须生成一个2048位RSA密钥对，然后在为[!DNL Snowflake]源创建帐户时提供以下值。

| 凭据 | 描述 |
| --- | --- |
| 帐户 | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| 用户名 | [!DNL Snowflake]帐户的用户名。 |
| 私钥 | [!DNL Snowflake]帐户的[!DNL Base64-]编码私钥。 您可以生成加密或未加密的私钥。 如果您使用的是加密的私钥，那么在针对Experience Platform进行身份验证时，您还必须提供私钥密码。 有关详细信息，请阅读[检索 [!DNL Snowflake] 私钥](../../../../connectors/databases/snowflake.md)的指南。 |
| 私钥密码 | 私钥密码是附加的安全层，在使用加密的私钥进行身份验证时必须使用该安全层。 如果您使用未加密的私钥，则无需提供密码。 |
| 数据库 | 包含要摄取到Experience Platform的数据的[!DNL Snowflake]数据库。 |
| 仓库 | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Platform时必须单独访问。 |

有关这些值的详细信息，请参阅[此Snowflake文档](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

>[!NOTE]
>
>必须将`PREVENT_UNLOAD_TO_INLINE_URL`标志设置为`FALSE`以允许从[!DNL Snowflake]数据库卸载数据以Experience Platform。

## 连接您的Snowflake帐户

在Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL 数据库]类别下，选择&#x200B;**[!UICONTROL Snowflake]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![突出显示[!DNL Snowflake]的源目录。](../../../../images/tutorials/create/snowflake/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Snowflake]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

若要使用现有帐户，请选择要连接的[!DNL Snowflake]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![源工作流中的现有帐户接口。](../../../../images/tutorials/create/snowflake/existing.png)

### 新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为您的新[!DNL Snowflake]帐户提供名称和可选描述。

![源工作流中的新帐户接口。](../../../../images/tutorials/create/snowflake/new.png)

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

若要使用帐户密钥身份验证，请在输入表单中提供连接字符串，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![帐户密钥身份验证接口。](../../../../images/tutorials/create/snowflake/connection-string.png)

>[!TAB 密钥对身份验证]

要使用密钥对身份验证，请提供帐户、用户名、私钥、私钥密码、数据库和仓库的值，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![帐户密钥对身份验证接口。](../../../../images/tutorials/create/snowflake/key-pair.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已与Snowflake帐户建立了连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Platform]](../../dataflow/databases.md)。
