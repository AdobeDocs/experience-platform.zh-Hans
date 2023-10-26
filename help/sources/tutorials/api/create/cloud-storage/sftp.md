---
title: 使用流服务API创建SFTP基本连接
description: 了解如何使用流量服务API将Adobe Experience Platform连接到SFTP（安全文件传输协议）服务器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: a826bda356a7205f3d4c0e0836881530dbaaf54e
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 2%

---

# 使用创建SFTP基本连接 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL SFTP] （安全文件传输协议）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

>[!IMPORTANT]
>
>建议在使用引入JSON对象时避免换行符或回车符 [!DNL SFTP] 源连接。 要解决此限制，请每行使用一个JSON对象，并使用多行来生成文件。

以下部分提供成功连接到 [!DNL SFTP] 服务器使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接到 [!DNL SFTP]中，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的关联的名称或IP地址 [!DNL SFTP] 服务器。 |
| `port` | 您连接到的SFTP服务器端口。 如果未提供，则值默认为 `22`. |
| `username` | 对您的具有访问权限的用户名 [!DNL SFTP] 服务器。 |
| `password` | 您的密码 [!DNL SFTP] 服务器。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码词组保护，则使用密码词组或密码解密私钥。 如果 `privateKeyContent` 受密码保护，此参数需要作为私钥内容的密码短语值使用。 |
| `maxConcurrentConnections` | 此参数允许您指定在连接到SFTP服务器时，平台将创建的并发连接数的最大限制。 必须将此值设置为小于SFTP设置的限制。 **注意**：为现有SFTP帐户启用此设置时，它仅影响未来的数据流，而不影响现有的数据流。 |
| `folderPath` | 要提供访问权限的文件夹的路径。 [!DNL SFTP] 源，您可以提供文件夹路径以指定用户对所选子文件夹的访问权限。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL SFTP] 为： `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Dynamics] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

此 [!DNL SFTP] 源支持基本身份验证和通过SSH公钥进行的身份验证。 在此步骤中，您还可以指定要提供访问权限的子文件夹的路径。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL SFTP] 作为请求参数一部分的身份验证凭据。

>[!IMPORTANT]
>
>此 [!DNL SFTP] 连接器支持RSA或DSA类型的OpenSSH密钥。 确保您的关键文件内容开头为 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 结束于 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 如果私钥文件是PPK格式文件，请使用PuTTY工具从PPK转换为OpenSSH格式。

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.maxConcurrentConnections` | 在将Platform连接到SFTP时指定的最大并发连接数。 启用时，该值必须设置为至少1。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | SFTP服务器连接规范ID： `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++响应

成功的响应将返回唯一标识符(`id`)。 请在下一教程中探究您的SFTP服务器时，需要此ID。

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.username` | 与您的关联的用户名 [!DNL SFTP] 服务器。 |
| `auth.params.privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥类型必须分类为RSA或DSA。 |
| `auth.params.passPhrase` | 如果密钥文件或密钥内容受密码词组保护，则使用密码词组或密码解密私钥。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语（值）一起使用。 |
| `auth.params.maxConcurrentConnections` | 在将Platform连接到SFTP时指定的最大并发连接数。 启用时，该值必须设置为至少1。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | 此 [!DNL SFTP] 服务器连接规范ID： `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++响应

成功的响应将返回唯一标识符(`id`)。 请在下一教程中探究您的SFTP服务器时，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## 后续步骤

在本教程之后，您已创建一个 [!DNL SFTP] 连接使用 [!DNL Flow Service] API中，并获取了连接的唯一ID值。 您可以使用此连接ID来 [使用流服务API浏览云存储](../../explore/cloud-storage.md).
