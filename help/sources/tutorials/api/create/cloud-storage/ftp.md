---
keywords: Experience Platform；主页；热门主题；文件传输协议；文件传输协议
solution: Experience Platform
title: 使用流服务API创建FTP基本连接
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到FTP（文件传输协议）服务器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建FTP基本连接

>[!NOTE]
>
>FTP连接器处于测试阶段。 功能和文档可能会发生更改。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL FTP]（文件传输协议）创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL FTP]服务器所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到[!DNL FTP]，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 与您的[!DNL FTP]服务器关联的名称或IP地址。 |
| `username` | 有权访问您的[!DNL FTP]服务器的用户名。 |
| `password` | [!DNL FTP]服务器的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL FTP]的连接规范ID为： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`。 |

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL FTP]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL FTP]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | FTP服务器的主机名。 |
| `auth.params.username` | 与您的FTP服务器关联的用户名。 |
| `auth.params.password` | 与您的FTP服务器关联的密码。 |
| `connectionSpec.id` | FTP服务器连接规范ID： `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**响应**

成功的响应返回新创建连接的唯一标识符(`id`)。 请在下一教程中探究您的FTP服务器时需要使用此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了一个FTP连接，并获取了此连接的唯一ID值。 您可以使用此连接ID以使用流服务API[&#128279;](../../explore/cloud-storage.md)来浏览云存储。
