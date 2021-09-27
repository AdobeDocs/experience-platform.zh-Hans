---
keywords: Experience Platform；主页；热门主题；SFTP;SFTP；安全文件传输协议；安全文件传输协议
solution: Experience Platform
title: 使用流服务API创建SFTP基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到SFTP（安全文件传输协议）服务器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 9ad09fba3119b631576f22574a2151c74f91e07b
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建SFTP基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL SFTP]（安全文件传输协议）创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

>[!IMPORTANT]
>
>建议在摄取具有[!DNL SFTP]源连接的JSON对象时避免换行符或回车符。 要绕过限制，请每行使用一个JSON对象，并使用多行来生成后续文件。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL SFTP]服务器。

### 收集所需的凭据

要使[!DNL Flow Service]连接到[!DNL SFTP]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与[!DNL SFTP]服务器关联的名称或IP地址。 |
| `port` | 您连接到的SFTP服务器端口。 如果未提供，则该值默认为`22`。 |
| `username` | 具有[!DNL SFTP]服务器访问权限的用户名。 |
| `password` | [!DNL SFTP]服务器的密码。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语的保护，则解密私钥的密码短语或密码。 如果`privateKeyContent`受密码保护，则需要将此参数与私钥内容的密码短语一起用作值。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL SFTP]的连接规范ID是：`b7bf2577-4520-42c9-bae9-cad01560f7bc`。 |

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL SFTP]身份验证凭据时，向`/connections`端点发出POST请求。

### 使用基本身份验证创建[!DNL SFTP]基本连接

要使用基本身份验证创建[!DNL SFTP]基本连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`host`、`userName`和`password`提供值。

**API格式**

```http
POST /connections
```

**请求**

以下请求使用基本身份验证为[!DNL SFTP]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
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
| `auth.params.username` | 与SFTP服务器关联的用户名。 |
| `auth.params.password` | 与SFTP服务器关联的密码。 |
| `connectionSpec.id` | SFTP服务器连接规范ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**响应**

成功的响应会返回新创建连接的唯一标识符(`id`)。 在下一个教程中，浏览SFTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### 使用SSH公钥身份验证创建[!DNL SFTP]基本连接

要使用SSH公钥身份验证创建[!DNL SFTP]基本连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`host`、`userName`、`privateKeyContent`和`passPhrase`提供值。

>[!IMPORTANT]
>
>[!DNL SFTP]连接器支持RSA或DSA类型的OpenSSH密钥。 确保您的关键文件内容以`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`开头并以`"-----END [RSA/DSA] PRIVATE KEY-----"`结尾。 如果私钥文件是PPK格式的文件，请使用PuTTY工具将PPK格式转换为OpenSSH格式。

**API格式**

```http
POST /connections
```

**请求**

以下请求使用SSH公钥身份验证为[!DNL SFTP]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
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
| `auth.params.username` | 与[!DNL SFTP]服务器关联的用户名。 |
| `auth.params.privateKeyContent` | Base64编码的SSH私钥内容。 OpenSSH密钥的类型必须分类为RSA或DSA。 |
| `auth.params.passPhrase` | 如果密钥文件或密钥内容受密码短语的保护，则解密私钥的密码短语或密码。 如果PrivateKeyContent受密码保护，则此参数需要与PrivateKeyContent的密码短语一起用作值。 |
| `connectionSpec.id` | [!DNL SFTP]服务器连接规范ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**响应**

成功的响应会返回新创建连接的唯一标识符(`id`)。 在下一个教程中浏览[!DNL SFTP]服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL SFTP]连接，并获取了该连接的唯一ID值。 您可以使用此连接ID来[使用流量服务API](../../explore/cloud-storage.md)或[使用流量服务API](../../cloud-storage-parquet.md)摄取Parquet数据来浏览云存储。
