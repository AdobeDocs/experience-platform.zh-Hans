---
keywords: Experience Platform；主页；热门主题；SFTP;sftp；安全文件传输协议；安全文件传输协议
solution: Experience Platform
title: 使用流服务API创建SFTP连接器
topic: overview
type: Tutorial
description: 本教程使用流服务API指导您完成将Experience Platform连接到SFTP（安全文件传输协议）服务器的步骤。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API创建SFTP连接器

>[!NOTE]
>
>SFTP连接器处于测试状态。 功能和文档可能会发生更改。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

本教程使用[!DNL Flow Service] API指导您完成将Experience Platform连接到SFTP（安全文件传输协议）服务器的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

>[!IMPORTANT]
>
>建议在使用SFTP源连接引入JSON对象时避免换行或回车。 要绕过限制，请每行使用一个JSON对象，然后使用多行生成后续文件。

以下各节提供了使用[!DNL Flow Service] API成功连接到SFTP服务器时需要了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]连接到SFTP，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的SFTP服务器关联的名称或IP地址。 |
| `username` | 有权访问SFTP服务器的用户名。 |
| `password` | SFTP服务器的口令。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 SSH私钥OpenSSH(RSA/DSA)格式。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语保护，则用于解密私钥的密码或密码。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中的[如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用平台API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 只需一个连接，因为它可用于创建多个数据流以引入不同的数据。

### 使用基本身份验证创建SFTP连接

要使用基本身份验证创建SFTP连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`host`、`userName`和`password`提供值。

**API格式**

```http
POST /connections
```

**请求**

要创建SFTP连接，其唯一连接规范ID必须作为POST请求的一部分提供。 SFTP的连接规范ID为`b7bf2577-4520-42c9-bae9-cad01560f7bc`。

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
| `auth.params.username` | 与您的SFTP服务器关联的用户名。 |
| `auth.params.password` | 与您的SFTP服务器关联的密码。 |
| `connectionSpec.id` | SFTP服务器连接规范ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**响应**

成功的响应会返回新创建的连接的唯一标识符(`id`)。 在下一个教程中浏览SFTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### 使用SSH公钥身份验证创建SFTP连接

要使用SSH公钥身份验证创建SFTP连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`host`、`userName`、`privateKeyContent`和`passPhrase`提供值。

**API格式**

```http
POST /connections
```

**请求**

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
| `auth.params.host` | SFTP服务器的主机名。 |
| `auth.params.username` | 与您的SFTP服务器关联的用户名。 |
| `auth.params.privateKeyContent` | base64编码的SSH私钥内容。 SSH私钥OpenSSH(RSA/DSA)格式。 |
| `auth.params.passPhrase` | 如果密钥文件或密钥内容受密码短语保护，则用于解密私钥的密码或密码。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |
| `connectionSpec.id` | SFTP服务器连接规范ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**响应**

成功的响应会返回新创建的连接的唯一标识符(`id`)。 在下一个教程中浏览SFTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了SFTP连接，并获得了该连接的唯一ID值。 您可以使用此连接ID来[使用流服务API](../../explore/cloud-storage.md)或[使用流服务API](../../cloud-storage-parquet.md)采集拼花存储。
