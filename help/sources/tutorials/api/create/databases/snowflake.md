---
title: 使用流服务API创建基于Snowflake的连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Snowflake。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# 创建 [!DNL Snowflake] 基本连接使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>此 [!DNL Snowflake] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

使用下面的教程了解如何为创建基本连接 [!DNL Snowflake] 使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

以下部分提供了成功连接时需要了解的其他信息 [!DNL Snowflake] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

必须提供以下凭据属性的值才能验证您的 [!DNL Snowflake] 源。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

| 凭据 | 描述 |
| ---------- | ----------- |
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须唯一标识跨不同帐户的帐户 [!DNL Snowflake] 组织。 要实现此目的，您必须在帐户名称前添加组织名称。 例如：`orgname-account_name`。有关帐户名称的更多信息，请阅读 [!DNL Snowflake] 文档 [帐户标识符](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个 [!DNL Snowflake] 数据仓库相互独立，在将数据传送到Platform时必须单独进行访问。 |
| `database` | 此 [!DNL Snowflake] 数据库包含您要带入Platform的数据。 |
| `username` | 的用户名 [!DNL Snowflake] 帐户。 |
| `password` | 的密码 [!DNL Snowflake] 用户帐户。 |
| `role` | 在中使用的默认访问控制角色 [!DNL Snowflake] 会话。 该角色应为已分配给指定用户的现有角色。 默认角色为 `PUBLIC`. |
| `connectionString` | 用于连接到 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB 密钥对身份验证]

要使用密钥对身份验证，您必须生成一个2048位RSA密钥对，然后在创建帐户时提供以下值 [!DNL Snowflake] 源。

| 凭据 | 描述 |
| --- | --- |
| `account` | 帐户名称可唯一标识组织内的帐户。 在这种情况下，您必须唯一标识跨不同帐户的帐户 [!DNL Snowflake] 组织。 要实现此目的，您必须在帐户名称前添加组织名称。 例如：`orgname-account_name`。有关帐户名称的更多信息，请阅读 [!DNL Snowflake] 文档 [帐户标识符](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | 您的用户名 [!DNL Snowflake] 帐户。 |
| `privateKey` | 此 [!DNL Base64-]已编码私钥的 [!DNL Snowflake] 帐户。 您可以生成加密或未加密的私钥。 如果您使用的是加密的私钥，那么在针对Experience Platform进行身份验证时，您还必须提供私钥密码。 |
| `privateKeyPassphrase` | 私钥密码是附加的安全层，在使用加密的私钥进行身份验证时必须使用该安全层。 如果您使用未加密的私钥，则无需提供密码。 |
| `database` | 此 [!DNL Snowflake] 包含要摄取到Experience Platform的数据的数据库。 |
| `warehouse` | 此 [!DNL Snowflake] warehouse管理应用程序的查询执行过程。 每个 [!DNL Snowflake] warehouse相互独立，在将数据转移到Experience Platform中时必须单独访问。 |

有关这些值的详细信息，请参阅 [[!DNL Snowflake] 密钥对身份验证指南](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>您必须设置 `PREVENT_UNLOAD_TO_INLINE_URL` 标记到 `FALSE` 允许从卸载数据 [!DNL Snowflake] Experience Platform数据库。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Snowflake] 作为请求正文一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 连接字符串]

+++请求

以下请求为创建基本连接 [!DNL Snowflake]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 用于连接到 [!DNL Snowflake] 实例。 的连接字符串模式 [!DNL Snowflake] 是 `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | 此 [!DNL Snowflake] 连接规范ID： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++响应

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB 使用加密的私钥进行密钥对身份验证]

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.account` | 您的名称 [!DNL Snowflake] 帐户。 |
| `auth.params.username` | 与您的关联的用户名 [!DNL Snowflake] 帐户。 |
| `auth.params.database` | 此 [!DNL Snowflake] 从中提取数据的数据库。 |
| `auth.params.privateKey` | 此 [!DNL Base64-]您的加密私钥的编码 [!DNL Snowflake] 帐户。 |
| `auth.params.privateKeyPassphrase` | 与您的私钥对应的密码。 |
| `auth.params.warehouse` | 此 [!DNL Snowflake] 您正在使用的仓库。 |
| `connectionSpec.id` | 此 [!DNL Snowflake] 连接规范ID： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++响应

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB 使用未加密的私钥进行密钥对身份验证]

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.account` | 您的名称 [!DNL Snowflake] 帐户。 |
| `auth.params.username` | 与您的关联的用户名 [!DNL Snowflake] 帐户。 |
| `auth.params.database` | 此 [!DNL Snowflake] 从中提取数据的数据库。 |
| `auth.params.privateKey` | 此 [!DNL Base64-]已编码但未加密的私钥 [!DNL Snowflake] 帐户。 |
| `auth.params.warehouse` | 此 [!DNL Snowflake] 您正在使用的仓库。 |
| `connectionSpec.id` | 此 [!DNL Snowflake] 连接规范ID： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++响应

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

在本教程之后，您已创建一个 [!DNL Snowflake] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
