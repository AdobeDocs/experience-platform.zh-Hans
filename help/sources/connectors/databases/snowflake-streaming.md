---
title: Snowflake流Source连接器概述
description: 了解如何创建源连接和数据流，以将流数据从Snowflake实例摄取到Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 3%

---

# [!DNL Snowflake]流源

>[!IMPORTANT]
>
>* [!DNL Snowflake]流源在API中可供已购买Real-Time CDP Ultimate的用户使用。
>
>* 在Amazon Web Services (AWS)上运行Adobe Experience Platform时，您现在可以使用[!DNL Snowflake]流源。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../landing/multi-cloud.md)。

Adobe Experience Platform 允许从外部源摄取数据，同时让您能够使用 Experience Platform 服务来构建、标记和增强传入数据。您可以从各种源(如Adobe应用程序、基于云的存储、数据库和许多其他源)中摄取数据。

Experience Platform支持从[!DNL Snowflake]数据库流式传输数据。

## 了解[!DNL Snowflake]流源

[!DNL Snowflake]流源通过定期执行SQL查询并为结果集中的每一行创建输出记录来加载数据。

通过使用[!DNL Kafka Connect]，[!DNL Snowflake]流源将跟踪它从每个表中收到的最新记录，以便它可以在下一个迭代的正确位置开始。 源使用此功能来筛选数据，并且只从每个迭代上的表中获取更新的行。

## 先决条件

以下部分概述了在将数据从[!DNL Snowflake]数据库流式传输到Experience Platform之前需要完成的先决步骤：

### IP地址允许列表

在将源连接到Experience Platform之前，必须将特定于区域的IP地址添加到允许列表。 有关详细信息，请阅读有关[将IP地址列入允许列表到Experience Platform](../../ip-address-allow-list.md)的指南。

以下文档提供了有关如何使用API或用户界面将[!DNL Amazon Redshift]连接到Experience Platform的信息：

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Snowflake]连接，您必须提供以下连接属性：

>[!BEGINTABS]

>[!TAB 基本身份验证]

| 凭据 | 描述 |
| --- | --- |
| `account` | [!DNL Snowflake]帐户的完整帐户标识符（帐户名称或帐户定位器）附加了后缀`snowflakecomputing.com`。 帐户标识符可以具有不同的格式： <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com （如`acme-abc12345.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}.snowflakecomputing.com （如`acme12345.ap-southeast-1.snowflakecomputing.com`）</li><li>{ACCOUNT_LOCATOR}。{CLOUD_REGION_ID}。{CLOUD}.snowflakecomputing.com （如`acme12345.east-us-2.azure.snowflakecomputing.com`）</li></ul> 有关详细信息，请阅读[[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>)。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |
| `database` | [!DNL Snowflake]数据库包含要带Experience Platform的数据。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `password` | [!DNL Snowflake]用户帐户的密码。 |
| `role` | （可选）可以为给定连接的用户提供自定义角色。 如果未提供，此值默认为`public`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Snowflake]的连接规范ID为`51ae16c2-bdad-42fd-9fce-8d5dfddaf140`。 |

>[!TAB 密钥对身份验证]

要使用密钥对身份验证，您必须生成一个2048位RSA密钥对，然后在为[!DNL Snowflake]源创建帐户时提供以下值。

| 凭据 | 描述 |
| --- | --- |
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须跨不同的[!DNL Snowflake]组织唯一标识帐户。 要实现此目的，您必须在帐户名称前添加组织名称。 例如： `orgname-account_name`。 请阅读有关[检索 [!DNL Snowflake] 帐户标识符](./snowflake.md#retrieve-your-account-identifier)的指南，以获取其他指导。 有关更多信息，请参阅[[!DNL Snowflake] 文档](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization)。 |
| `username` | [!DNL Snowflake]帐户的用户名。 |
| `privateKey` | [!DNL Base64-]帐户的[!DNL Snowflake]编码私钥。 您可以生成加密或未加密的私钥。 如果您使用的是加密的私钥，那么在针对Experience Platform进行身份验证时，还必须提供私钥密码。 有关详细信息，请阅读[检索 [!DNL Snowflake] 私钥](./snowflake.md)的指南。 |
| `passphrase` | 密码短语是附加的安全层，在使用加密的私钥进行身份验证时必须使用该安全层。 如果您使用未加密的私钥，则无需提供密码。 |
| `database` | 包含要摄取到Experience Platform的数据的[!DNL Snowflake]数据库。 |
| `warehouse` | [!DNL Snowflake]仓库管理应用程序的查询执行过程。 每个[!DNL Snowflake]仓库彼此独立，在将数据传送到Experience Platform时必须单独访问。 |

有关这些值的详细信息，请参阅[[!DNL Snowflake] 密钥对身份验证指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html)。

>[!ENDTABS]

### 检索帐户标识符 {#retrieve-your-account-identifier}

要通过Experience Platform验证您的[!DNL Snowflake]实例，您需要从[!DNL Snowflake] UI仪表板获取帐户标识符。

按照以下步骤查找您的帐户标识符：

* 在[[!DNL Snowflake] 应用程序UI仪表板](https://app.snowflake.com/)上导航到您的帐户。
* 在左侧导航中，选择&#x200B;**[!DNL Accounts]**，然后从标题中选择&#x200B;**[!DNL Active Accounts]**。
* 接下来，选择信息图标，然后选择并复制当前URL的域名。

### 检索您的私钥 {#retrieve-your-private-key}

如果您计划对[!DNL Snowflake]连接使用密钥对身份验证，则需要在连接到Experience Platform之前生成私钥。

>[!BEGINTABS]

>[!TAB 创建加密的私钥]

要生成加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

如果成功，您应会收到PEM格式的私钥。

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB 创建未加密的私钥]

要生成未加密的[!DNL Snowflake]私钥，请在终端上运行以下命令：

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

如果成功，您应会收到PEM格式的私钥。

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

生成私钥后，直接在[!DNL Base64]中对其进行编码，而不对其格式或内容进行任何更改。 在编码之前，请确保私钥的末尾没有额外的空格或空行（包括尾随新行）。

### 验证配置

在为[!DNL Snowflake]数据创建源连接之前，还必须确保满足以下配置：

* 分配给给定用户的默认仓库必须与在向Experience Platform进行身份验证时输入的仓库相同。
* 分配给给定用户的默认角色必须有权访问在对Experience Platform进行身份验证时输入的同一数据库。

要验证您的角色和仓库，请执行以下操作：

* 在左侧导航中选择&#x200B;**[!DNL Admin]**，然后选择&#x200B;**[!DNL Users & Roles]**。
* 选择相应的用户，然后选择右上角的省略号(`...`)。
* 在出现的[!DNL Edit user]窗口中，导航到[!DNL Default Role]以查看与给定用户关联的角色。
* 在同一窗口中，导航到[!DNL Default Warehouse]以查看与给定用户关联的仓库。

成功编码后，您可以在Experience Platform上使用该已编码的[!DNL Base64]私钥来验证您的[!DNL Snowflake]帐户。

### 配置角色设置 {#configure-role-settings}

即使分配了默认公共角色，也必须配置角色的权限，以允许源连接访问相关[!DNL Snowflake]数据库、架构和表。 不同[!DNL Snowflake]实体的各种权限如下所示：

| [!DNL Snowflake]实体 | 需要角色权限 |
| --- | --- |
| 仓库 | 操作、使用 |
| 数据库 | 使用情况 |
| 架构 | 使用情况 |
| 表 | 选择 |

>[!NOTE]
>
>必须在仓库的高级设置配置中启用自动恢复和自动暂停。

有关角色和权限管理的详细信息，请参阅[[!DNL Snowflake] API参考](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>)。

## 将Unix时间转换为日期字段

[!DNL Snowflake Streaming]分析并写入`DATE`字段作为自Unix纪元以来的天数(1970-01-01)。 例如，`DATE`值为0表示1970年1月1日，而值为1表示1970年1月2日。 因此，在准备文件以在[!DNL Snowflake Streaming]源中创建映射时，请确保`DATE`列表示为整数。

您可以使用[数据准备数据和时间函数](../../../data-prep/functions.md#date-and-time-functions)将Unix时间转换为可引入Experience Platform的日期字段。 例如：

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

在此函数中：

* `{DATE_COLUMN}`是包含epoch天整数的日期列。
* 乘以86400000可将纪元天数转换为毫秒。
* “yyyy-MM-dd”指定所需的日期格式。

此转换可确保日期在您的数据集中正确显示。


## 限制和常见问题解答 {#limitations-and-frequently-asked-questions}

* [!DNL Snowflake]源的数据吞吐量为每秒2000条记录。
* 根据仓库的活动时间和仓库的大小，定价可能会有所不同。 对于[!DNL Snowflake]源集成，最小大小x小仓库就足够了。 建议启用自动暂停，以便仓库在不使用时能够自行暂停。
* [!DNL Snowflake]源每10秒轮询数据库一次新数据。
* 配置选项：
   * 创建源连接时，您可以为`backfill`源启用[!DNL Snowflake]布尔标记。
      * 如果回填设置为true ，则timestamp.initial的值将设置为0。 这意味着获取时间戳列大于0纪元时间的数据。
      * 如果回填设置为false，则timestamp.initial的值将设置为–1。 这意味着获取时间戳列大于当前时间（源开始摄取的时间）的数据。
   * 时间戳列的格式应该是： `TIMESTAMP_LTZ`或`TIMESTAMP_NTZ`。 如果时间戳列设置为`TIMESTAMP_NTZ`，则应通过`timezoneValue`参数传递存储值的相应时区。 如果未提供，该值将默认为UTC。
      * `TIMESTAMP_TZ`不能用于时间戳列或映射。

## 后续步骤

>[!NOTE]
>
>创建或更新流数据流后，需要短暂暂停数据摄取5分钟，以防出现任何潜在的数据丢失或数据丢失情况。

以下教程提供了有关如何使用API将[!DNL Snowflake]流源连接到Experience Platform的步骤：

* [使用流服务API将数据从 [!DNL Snowflake] 数据库流入Experience Platform](../../tutorials/api/create/databases/snowflake-streaming.md)
* [使用Experience Platform用户界面中的源工作区将数据从 [!DNL Snowflake] 数据库流式传输到Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
