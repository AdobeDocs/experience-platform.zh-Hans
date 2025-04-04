---
keywords: Experience Platform；主页；热门主题；Zoho CRM；zoho crm；Zoho；Zoho
solution: Experience Platform
title: 使用流服务API创建Zoho CRM基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Zoho CRM。
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API创建[!DNL Zoho CRM]基本连接

>[!WARNING]
>
>[!DNL Zoho CRM]源将于2025年6月底弃用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Zoho CRM]创建基本连接的步骤。

## 开始使用

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Zoho CRM]时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Zoho CRM]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | 您向其发出请求的[!DNL Zoho CRM]服务器的端点。 |
| `accountsUrl` | 帐户URL用于生成访问和刷新令牌。 URL必须特定于域。 |
| `clientId` | 与您的[!DNL Zoho CRM]用户帐户对应的客户端ID。 |
| `clientSecret` | 与您的[!DNL Zoho CRM]用户帐户对应的客户端密钥。 |
| `accessToken` | 访问令牌授权您对您的[!DNL Zoho CRM]帐户的安全临时访问。 |
| `refreshToken` | 刷新令牌是在您的访问令牌过期后用于生成新的访问令牌的令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Zoho CRM]的连接规范ID为： `929e4450-0237-4ed2-9404-b7e1e0a00309`。 |

有关这些凭据的详细信息，请参阅有关[[!DNL Zoho CRM] 身份验证](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html)的文档。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Zoho CRM]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

>[!TIP]
>
>您的帐户URL域必须与适当的域位置相对应。 以下是各个域及其相应的帐户URL：<ul><li>美国： https://accounts.zoho.com</li><li>澳大利亚：https://accounts.zoho.com.au</li><li>欧洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中国： https://accounts.zoho.com.cn</li></ul>

以下请求为[!DNL Zoho CRM]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | [!DNL Zoho CRM]基本连接的名称。 您可以使用此名称查找您的[!DNL Zoho CRM]基本连接。 |
| `description` | [!DNL Zoho CRM]基本连接的可选描述。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | 您向其发出请求的[!DNL Zoho CRM]服务器的端点。 |
| `auth.params.accountsUrl` | 帐户URL用于生成访问和刷新令牌。 URL必须特定于域。 |
| `auth.params.clientId` | 与您的[!DNL Zoho CRM]用户帐户对应的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL Zoho CRM]用户帐户对应的客户端密钥。 |
| `auth.params.accessToken` | 访问令牌授权您对您的[!DNL Zoho CRM]帐户的安全临时访问。 |
| `auth.params.refreshToken` | 刷新令牌是在您的访问令牌过期后用于生成新的访问令牌的令牌。 |
| `connectionSpec.id` | [!DNL Zoho CRM]的连接规范ID： `929e4450-0237-4ed2-9404-b7e1e0a00309`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Zoho]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将CRM数据引入Experience Platform](../../collect/crm.md)
