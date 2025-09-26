---
title: Snowflake Source Connector概述
description: 了解如何使用API或用户界面将Snowflake连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 0476c42924bf0163380e650141fad8e50b98d4cf
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 3%

---

# [!DNL Snowflake]源

>[!IMPORTANT]
>
>* [!DNL Snowflake]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。
>* 默认情况下，[!DNL Snowflake]源将`null`解释为空字符串。 请联系您的Adobe代表，以确保在Adobe Experience Platform中将您的`null`值正确写入`null`。
>* 要让Experience Platform摄取数据，必须将所有基于表的批处理源的时区配置为UTC时区。 [!DNL Snowflake]源支持的唯一时间戳是带有UTC时间的TIMESTAMP_NTZ。

Adobe Experience Platform 允许从外部源摄取数据，同时让您能够使用 Experience Platform 服务来构建、标记和增强传入数据。您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从第三方数据库引入数据。 Experience Platform可以连接到各种类型的数据库，例如关系数据库、NoSQL数据库或数据仓库数据库。 对数据库提供程序的支持包括[!DNL Snowflake]。

## 先决条件 {#prerequisites}

本节概述在将[!DNL Snowflake]源连接到Experience Platform之前需要完成的设置任务。

### IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

### 收集所需的凭据

必须提供以下凭据属性的值才能对您的[!DNL Snowflake]源进行身份验证。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证(Azure)]

提供以下凭据的值，以使用帐户密钥身份验证将[!DNL Snowflake]连接到Azure上的Experience Platform。

| 凭据 | 描述 |
| ---------- | ----------- |
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 阅读有关[检索 [!DNL Snowflake] 帐户标识符](#retrieve-your-account-identifier)的部分以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |
| `database` | [!DNL Snowflake]数据库包含要带Experience Platform的数据。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `password` | [!DNL Snowflake]用户帐户的密码。 |
| `role` | 在[!DNL Snowflake]会话中使用的默认访问控制角色。 该角色应为已分配给指定用户的现有角色。 默认角色为`PUBLIC`。 |
| `connectionString` | 用于连接到[!DNL Snowflake]实例的连接字符串。 [!DNL Snowflake]的连接字符串模式为`jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`。 |

>[!TAB 密钥对身份验证(Azure)]

要使用密钥对身份验证，首先生成2048位RSA密钥对。 接下来，提供以下凭据的值，以使用密钥对身份验证连接到Azure上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 阅读有关[检索 [!DNL Snowflake] 帐户标识符](#retrieve-your-account-identifier)的部分以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `privateKey` | [!DNL Base64-]帐户的[!DNL Snowflake]编码私钥。 您可以生成加密或未加密的私钥。 如果您使用的是加密的私钥，那么在针对Experience Platform进行身份验证时，还必须提供私钥密码。 有关详细信息，请阅读[检索私钥](#retrieve-your-private-key)一节。 |
| `privateKeyPassphrase` | 私钥密码是附加的安全层，在使用加密的私钥进行身份验证时必须使用该安全层。 如果您使用未加密的私钥，则无需提供密码。 |
| `port` | [!DNL Snowflake]通过Internet连接到服务器时使用的端口号。 |
| `database` | 包含要摄取到Experience Platform的数据的[!DNL Snowflake]数据库。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |

有关这些值的详细信息，请参阅[[!DNL Snowflake] 密钥对身份验证指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!TAB 基本身份验证(AWS)]

提供以下凭据的值，以使用基本身份验证将[!DNL Snowflake]连接到AWS上的Experience Platform。

>[!WARNING]
>
>[!DNL Snowflake]源的基本身份验证（或帐户密钥身份验证）将于2025年11月被弃用。 您必须迁移到基于密钥对的身份验证，才能继续使用源并从数据库中摄取数据到Experience Platform。 有关弃用的详细信息，请阅读关于降低凭据泄露风险的[[!DNL Snowflake] 最佳实践指南](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/)。

| 凭据 | 描述 |
| --- | --- |
| `host` | 您的[!DNL Snowflake]帐户连接到的主机URL。 |
| `port` | [!DNL Snowflake]通过Internet连接到服务器时使用的端口号。 |
| `username` | 与您的[!DNL Snowflake]帐户关联的用户名。 |
| `password` | 与您的[!DNL Snowflake]帐户关联的密码。 |
| `database` | 将从其中提取数据的[!DNL Snowflake]数据库。 |
| `schema` | 与您的[!DNL Snowflake]数据库关联的架构的名称。 您必须确保要为其授予数据库访问权限的用户也具有此架构的访问权限。 |
| `warehouse` | 您正在使用的[!DNL Snowflake]仓库。 |

>[!TAB 密钥对身份验证(AWS)]

要使用密钥对身份验证，首先生成2048位RSA密钥对。 接下来，提供以下凭据的值，以使用密钥对身份验证连接到AWS上的Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](#etrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `privateKey` | [!DNL Snowflake]用户的私钥，以base64编码为单行，无标头或换行符。 要准备它，请复制PEM文件的内容，删除`BEGIN`/`END`行和所有换行符，然后对结果进行base64编码。 有关详细信息，请阅读[检索私钥](#retrieve-your-private-key)一节。 **注意：** AWS连接当前不支持加密的私钥。 |
| `port` | [!DNL Snowflake]通过Internet连接到服务器时使用的端口号。 |
| `database` | 包含要摄取到Experience Platform的数据的[!DNL Snowflake]数据库。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |

有关这些值的详细信息，请参阅[[!DNL Snowflake] 密钥对身份验证指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 检索帐户标识符 {#retrieve-your-account-identifier}

您必须从[!DNL Snowflake] UI仪表板中检索帐户标识符，因为您将使用该帐户标识符在Experience Platform上验证您的[!DNL Snowflake]实例。

要检索您的帐户标识符，请执行以下操作：

* 在[[!DNL Snowflake] 应用程序UI仪表板](https://app.snowflake.com/)上导航到您的帐户。
* 在左侧导航中，选择&#x200B;**[!DNL Accounts]**，然后从标题中选择&#x200B;**[!DNL Active Accounts]**。
* 接下来，选择信息图标，然后选择并复制当前URL的域名。

![选定域名的Snowflake UI仪表板。](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### 检索您的私钥 {#retrieve-your-private-key}

如果您正在对[!DNL Snowflake]连接使用密钥对身份验证，则您还必须在连接到Experience Platform之前生成私钥。

>[!BEGINTABS]

>[!TAB 创建加密的私钥]

要生成加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

如果成功，您应会收到PEM格式的私钥。

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 创建未加密的私钥]

要生成未加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

如果成功，您应会收到PEM格式的私钥。

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

接下来，获取您的私钥并在[!DNL Base64]中进行编码。 请确保您未对[!DNL Snowflake]私钥进行任何转换或格式转换。 此外，您必须确保私钥的末尾没有尾随新行字符，然后才能在[!DNL Base64]中对其进行编码。

### 验证配置

在为[!DNL Snowflake]数据创建源连接之前，还必须确保满足以下配置：

* 分配给给定用户的默认仓库必须与在向Experience Platform进行身份验证时输入的仓库相同。
* 分配给给定用户的默认角色必须有权访问在对Experience Platform进行身份验证时输入的同一数据库。

要验证您的角色和仓库，请执行以下操作：

* 在左侧导航中选择&#x200B;**[!DNL Admin]**，然后选择&#x200B;**[!DNL Users & Roles]**。
* 选择相应的用户，然后选择右上角的省略号(`...`)。
* 在出现的[!DNL Edit user]窗口中，导航到[!DNL Default Role]以查看与给定用户关联的角色。
* 在同一窗口中，导航到[!DNL Default Warehouse]以查看与给定用户关联的仓库。

![可在其中验证您的角色和仓库的Snowflake UI。](../../images/tutorials/create/snowflake/snowflake-configs.png)

成功编码后，您可以在Experience Platform上使用该已编码的[!DNL Base64]私钥来验证您的[!DNL Snowflake]帐户。

以下文档提供了有关如何使用API或用户界面将[!DNL Snowflake]连接到Experience Platform的信息：

## 使用API将[!DNL Snowflake]连接到Experience Platform

* [使用流服务API创建Snowflake基本连接](../../tutorials/api/create/databases/snowflake.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

## 使用UI将[!DNL Snowflake]连接到Experience Platform

* [在UI中创建Snowflake源连接](../../tutorials/ui/create/databases/snowflake.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
