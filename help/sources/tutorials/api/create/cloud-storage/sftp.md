---
keywords: Experience Platform；主页；热门主题；SFTP;SFTP；安全文件传输协议；安全文件传输协议
solution: Experience Platform
title: 使用流服务API创建SFTP基连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到SFTP（安全文件传输协议）服务器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 1%

---

# 使用创建SFTP基本连接 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL SFTP] （安全文件传输协议）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

>[!IMPORTANT]
>
>在使用 [!DNL SFTP] 源连接。 要绕过限制，请每行使用一个JSON对象，并使用多行来生成后续文件。

以下部分提供了成功连接到 [!DNL SFTP] 服务器使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接到 [!DNL SFTP]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的 [!DNL SFTP] 服务器。 |
| `port` | 您连接到的SFTP服务器端口。 如果未提供，则值默认为 `22`. |
| `username` | 有权访问您的 [!DNL SFTP] 服务器。 |
| `password` | 您的密码 [!DNL SFTP] 服务器。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语的保护，则解密私钥的密码短语或密码。 如果 `privateKeyContent` 受密码保护，此参数需要与私钥内容的密码短语一起用作值。 |
| `maxConcurrentConnections` | 此参数允许您为平台在连接到SFTP服务器时将创建的并发连接数指定最大限制。 您必须将此值设置为小于SFTP设置的限制。 **注意**:为现有SFTP帐户启用此设置后，它只会影响将来的数据流，而不会影响现有的数据流。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL SFTP] 为： `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

的 [!DNL SFTP] 源支持通过SSH公钥进行基本身份验证和身份验证。

要创建基本连接ID，请向 `/connections` 提供 [!DNL SFTP] 身份验证凭据作为请求参数的一部分。

>[!IMPORTANT]
>
>的 [!DNL SFTP] 连接器支持RSA或DSA类型OpenSSH密钥。 确保关键文件内容以 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 结尾为 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 如果私钥文件是PPK格式的文件，请使用PuTTY工具将PPK格式转换为OpenSSH格式。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL SFTP]:

>[!BEGINTABS]

>[!TAB 基本身份验证]

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
              "maxConcurrentConnections": 1
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
| `auth.params.username` | 与SFTP服务器关联的用户名。 |
| `auth.params.password` | 与SFTP服务器关联的密码。 |
| `auth.params.maxConcurrentConnections` | 将平台连接到SFTP时指定的并发连接数上限。 启用后，此值必须至少设置为1。 |
| `connectionSpec.id` | SFTP服务器连接规范ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB SSH公钥身份验证]

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
              "maxConcurrentConnections": 1

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
| `auth.params.host` | 的主机名 [!DNL SFTP] 服务器。 |
| `auth.params.port` | SFTP服务器的端口。 此整数值默认为22。 |
| `auth.params.username` | 与您的 [!DNL SFTP] 服务器。 |
| `auth.params.privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| `auth.params.passPhrase` | 如果密钥文件或密钥内容受密码短语的保护，则解密私钥的密码短语或密码。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语一起用作值。 |
| `auth.params.maxConcurrentConnections` | 将平台连接到SFTP时指定的并发连接数上限。 启用后，此值必须至少设置为1。 |
| `connectionSpec.id` | 的 [!DNL SFTP] 服务器连接规范ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**响应**

成功的响应会返回唯一标识符(`id`)。 在下一个教程中，浏览SFTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL SFTP] 使用 [!DNL Flow Service] API，并且已获取连接的唯一ID值。 您可以将此连接ID用于 [使用流量服务API浏览云存储](../../explore/cloud-storage.md).
