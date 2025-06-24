---
title: 使用流服务API创建SFTP基本连接
description: 了解如何使用流量服务API将Adobe Experience Platform连接到SFTP（安全文件传输协议）服务器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建SFTP基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL SFTP]（安全文件传输协议）创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

>[!IMPORTANT]
>
>建议在摄取具有[!DNL SFTP]源连接的JSON对象时避免换行符或回车符。 要解决此限制，请每行使用一个JSON对象，并使用多行来生成文件。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL SFTP]服务器所需了解的其他信息。

### 收集所需的凭据

有关如何检索身份验证凭据的详细步骤，请阅读[[!DNL SFTP] 身份验证指南](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

>[!TIP]
>
>创建后，无法更改[!DNL SFTP]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

[!DNL SFTP]源支持基本身份验证和通过SSH公钥的身份验证。 在此步骤中，您还可以指定要提供访问权限的子文件夹的路径。

要创建基本连接ID，请在提供您的[!DNL SFTP]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

>[!IMPORTANT]
>
>[!DNL SFTP]连接器支持`ed25519`、`RSA`或`DSA`类型的OpenSSH密钥。 确保您的密钥文件内容以`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`开头并以`"-----END [RSA/DSA] PRIVATE KEY-----"`结尾。 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK转换为OpenSSH格式。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本身份验证]

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | SFTP服务器的主机名。 |
| `auth.params.port` | SFTP服务器的端口。 此整数值默认为22。 |
| `auth.params.username` | 与您的SFTP服务器关联的用户名。 |
| `auth.params.password` | 与您的SFTP服务器关联的密码。 |
| `auth.params.maxConcurrentConnections` | 将Experience Platform连接到SFTP时指定的最大并发连接数。 启用时，该值必须设置为至少1。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `auth.params.disableChunking` | 一个布尔值，用于确定SFTP服务器是否支持分块。 |
| `connectionSpec.id` | SFTP服务器连接规范ID： `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++响应

成功的响应返回新创建连接的唯一标识符(`id`)。 请在下一教程中探究您的SFTP服务器时，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB SSH公钥身份验证]

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
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | [!DNL SFTP]服务器的主机名。 |
| `auth.params.port` | SFTP服务器的端口。 此整数值默认为22。 |
| `auth.params.username` | 与您的[!DNL SFTP]服务器关联的用户名。 |
| `auth.params.privateKeyContent` | Base64编码的SSH私钥内容。 支持的OpenSSH密钥类型为`ed25519`、`RSA`和`DSA`。 |
| `auth.params.passPhrase` | 如果密钥文件或密钥内容受密码词组保护，则使用密码词组或密码解密私钥。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语（值）一起使用。 |
| `auth.params.maxConcurrentConnections` | 将Experience Platform连接到SFTP时指定的最大并发连接数。 启用时，该值必须设置为至少1。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `auth.params.disableChunking` | 一个布尔值，用于确定SFTP服务器是否支持分块。 |
| `connectionSpec.id` | [!DNL SFTP]服务器连接规范ID： `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++响应

成功的响应返回新创建连接的唯一标识符(`id`)。 请在下一教程中探究您的SFTP服务器时，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL SFTP]连接，并获得了此连接的唯一ID值。 您可以使用此连接ID以使用流服务API[&#128279;](../../explore/cloud-storage.md)来浏览云存储。
