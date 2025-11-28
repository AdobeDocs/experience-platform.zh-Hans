---
title: Snowflake Source Connector概述
description: 了解如何使用API或用户界面将Snowflake连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 2%

---

# [!DNL Snowflake]源

>[!IMPORTANT]
>
>* [!DNL Snowflake]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。
>* 默认情况下，[!DNL Snowflake]源将`null`解释为空字符串。 请联系您的Adobe代表，以确保在Adobe Experience Platform中将您的`null`值正确写入`null`。
>* 要让Experience Platform摄取数据，必须将所有基于表的批处理源的时区配置为UTC时区。 [!DNL Snowflake]源支持的唯一时间戳是带有UTC时间的TIMESTAMP_NTZ。

[!DNL Snowflake]是一个基于云的数据仓库平台，旨在使组织能够有效地存储、处理和分析大量数据。 [!DNL Snowflake]旨在利用云的可扩展性和灵活性，它支持数据集成、高级分析和跨团队的无缝共享。 作为完全托管的服务，[!DNL Snowflake]消除了传统数据库常见的维护复杂性，使您能够专注于从数据中获取见解和价值。

您可以使用[!DNL Snowflake]源连接并将数据从[!DNL Snowflake]带到Adobe Experience Platform。 阅读以下文档以了解如何设置[!DNL Snowflake]源并连接到Experience Platform。

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
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `myorg-myaccount.snowflakecomputing.com`。 阅读有关[检索 [!DNL Snowflake] 帐户标识符](#retrieve-your-account-identifier)的部分以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
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
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `myorg-myaccount.snowflakecomputing.com`。 阅读有关[检索 [!DNL Snowflake] 帐户标识符](#retrieve-your-account-identifier)的部分以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
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
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `http://myorg-myaccount.snowflakecomputing.com/`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](#etrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `privateKey` | [!DNL Snowflake]用户的私钥，以base64编码为单行，无标头或换行符。 要准备它，请复制PEM文件的内容，删除`BEGIN`/`END`行和所有换行符，然后对结果进行base64编码。 有关详细信息，请阅读[检索私钥](#retrieve-your-private-key)一节。 **注意：** AWS连接当前不支持加密的私钥。 |
| `port` | [!DNL Snowflake]通过Internet连接到服务器时使用的端口号。 |
| `database` | 包含要摄取到Experience Platform的数据的[!DNL Snowflake]数据库。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |

有关这些值的详细信息，请参阅[[!DNL Snowflake] 密钥对身份验证指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 检索帐户标识符 {#retrieve-your-account-identifier}

您必须从[!DNL Snowflake] UI仪表板中检索帐户标识符，因为您将使用此仪表板在Experience Platform上验证[!DNL Snowflake]实例。

要检索您的帐户标识符，请执行以下操作：

* 使用[[!DNL Snowflake] 应用程序UI仪表板](https://app.snowflake.com/)访问您的帐户。
* 在左侧导航中，选择&#x200B;**[!DNL Accounts]**，然后从标题中选择&#x200B;**[!DNL Active Accounts]**。
* 接下来，选择信息图标，然后选择并复制当前URL的域名。

![选定域名的Snowflake UI仪表板。](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### 生成RSA密钥对

在命令行界面中使用OpenSSL生成PKCS#8格式的2048位RSA密钥对。 最佳实践是为安全目的创建加密的私钥，这需要密码。

>[!BEGINTABS]

>[!TAB 生成加密的私钥]

要生成加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB 生成未加密的私钥]

要生成未加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### 从私钥生成公钥

接下来，在命令行界面中运行以下命令，以基于私钥创建公钥。

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### 将公钥分配给[!DNL Snowflake]用户

您需要使用[!DNL Snowflake]管理员角色（如&#x200B;**SECURITYADMIN**）将生成的公钥与Experience Platform将使用的[!DNL Snowflake]服务用户相关联。 要检索公钥内容，请打开`rsa_key.pub`文件并复制整个内容，不包括`-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----`行。 接下来，在[!DNL Snowflake]中执行以下SQL：

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### 在[!DNL Base64]中编码私钥

Experience Platform要求在连接设置期间将私钥进行[!DNL Base64]编码并作为字符串提供。 使用合适的工具或脚本将`rsa_key.p8`文件的内容编码为单个[!DNL Base64]字符串。

>[!TIP]
>
>确保在编码过程之前或之后没有额外的空格或换行符，包括页眉/页脚行`(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`，因为这会导致身份验证错误。

### 验证配置

在Experience Platform中创建[!DNL Snowflake]源连接之前，必须确保用户的&#x200B;**[!DNL Default Role]**&#x200B;和&#x200B;**[!DNL Default Warehouse]**&#x200B;与您在Experience Platform中提供的值匹配。 您可以使用[!DNL Snowflake] SQL命令在`DESCRIBE USER {USERNAME}` UI中验证这些设置。

或者，您可以按照以下步骤验证您的设置：

* 在左侧导航中选择&#x200B;**[!DNL Admin]**，然后选择&#x200B;**[!DNL Users & Roles]**。
* 选择相应的用户，然后选择右上角的省略号(`...`)。
* 在出现的[!DNL Edit user]窗口中，导航到[!DNL Default Role]以查看与给定用户关联的角色。
* 在同一窗口中，导航到[!DNL Default Warehouse]以查看与给定用户关联的仓库。

![可在其中验证您的角色和仓库的Snowflake UI。](../../images/tutorials/create/snowflake/snowflake-configs.png)

## 后续步骤

完成设置后，您现在可以继续将您的[!DNL Snowflake]帐户连接到Experience Platform。 有关详细信息，请阅读以下文档：

### 使用API将[!DNL Snowflake]连接到Experience Platform

* [使用API连接 [!DNL Snowflake] 到Experience Platform](../../tutorials/api/create/databases/snowflake.md)
* [使用流服务API浏览数据表](../../tutorials/api/explore/tabular.md)
* [使用流服务API为数据库源创建数据流](../../tutorials/api/collect/database-nosql.md)

### 使用UI将[!DNL Snowflake]连接到Experience Platform

* [使用UI连接 [!DNL Snowflake] 到Experience Platform](../../tutorials/ui/create/databases/snowflake.md)
* [在用户界面中为数据库源连接创建数据流](../../tutorials/ui/dataflow/databases.md)
