---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: 使用流服务API创建SFTP连接器
topic: overview
type: Tutorial
description: 本教程使用流服务API指导您完成将Experience Platform连接到SFTP（安全文件传输协议）服务器的步骤。
translation-type: tm+mt
source-git-commit: 781a26486a42f304308f567284cef53d591aa124
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 2%

---


# 使用API创建SFTP连 [!DNL Flow Service] 接器

>[!NOTE]
>
>SFTP连接器处于测试状态。 功能和文档可能会发生更改。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到SFTP(安 [!DNL Experience Platform] 全文件传输协议)服务器的步骤。

如果您希望在中使用用户 [!DNL Experience Platform]界面， [UI教程](../../../ui/create/cloud-storage/ftp-sftp.md) 提供了执行类似操作的分步说明。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到SFTP服 [!DNL Flow Service] 务器。

### 收集所需的凭据

要连接 [!DNL Flow Service] 到SFTP，您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的SFTP服务器关联的名称或IP地址。 |
| `username` | 有权访问SFTP服务器的用户名。 |
| `password` | SFTP服务器的口令。 |
| `privateKeyContent` | Base64编码的SSH私钥内容。 SSH私钥OpenSSH(RSA/DSA)格式。 |
| `passPhrase` | 如果密钥文件或密钥内容受密码短语保护，则用于解密私钥的密码或密码。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Flow Service]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个SFTP帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

### 使用基本身份验证创建SFTP连接

要使用基本身份验证创建SFTP连接，请向 [!DNL Flow Service] API发出POST请求，同时为连接、 `host`和 `userName`提供值 `password`。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "password": "{PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | SFTP服务器的主机名。 |
| `auth.params.username` | 与您的SFTP服务器关联的用户名。 |
| `auth.params.password` | 与您的SFTP服务器关联的密码。 |
| `connectionSpec.id` | SFTP服务器连接规范ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**响应**

成功的响应会返回新创建的连接`id`的唯一标识符()。 在下一个教程中浏览SFTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### 使用SSH公钥身份验证创建SFTP连接

要使用SSH公钥身份验证创建SFTP连接，请向 [!DNL Flow Service] API发出POST请求，同时为连接的 `host`、 `userName`、 `privateKeyContent`和提供 `passPhrase`值。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  "auth": {
        "specName": "SSH PublicKey Authentication for sftp",
        "params": {
            "host": "{HOST_NAME}",
            "userName": "{USER_NAME}",
            "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
            "passPhrase": "{PASS_PHRASE}"
        }
    },
    "connectionSpec": {
        "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "version": "1.0"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | SFTP服务器的主机名。 |
| `auth.params.username` | 与您的SFTP服务器关联的用户名。 |
| `auth.params.privateKeyContent` | base64编码的SSH私钥内容。 SSH私钥OpenSSH(RSA/DSA)格式。 |
| `auth.params.passPhrase` | 如果密钥文件或密钥内容受密码短语保护，则用于解密私钥的密码或密码。 如果PrivateKeyContent是密码保护的，则此参数需要与PrivateKeyContent的密码短语一起使用作值。 |
| `connectionSpec.id` | SFTP服务器连接规范ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**响应**

成功的响应会返回新创建的连接`id`的唯一标识符()。 在下一个教程中浏览SFTP服务器时需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

通过本教程，您已使用API创建了SFTP [!DNL Flow Service] 连接，并已获得该连接的唯一ID值。 您可以使用此连接ID [使用流服务API探索云存储](../../explore/cloud-storage.md) , [或使用流服务API获取拼花数据](../../cloud-storage-parquet.md)。
