---
keywords: Experience Platform；主页；热门主题；veeva crm；Veeva CRM；Veeva；
solution: Experience Platform
title: 使用流服务API创建Veeva CRM基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Veeva CRM。
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Veeva CRM]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Veeva CRM]创建基本连接的步骤。

## 开始使用

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Veeva CRM]时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Veeva CRM]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM]实例的URL。 |
| `username` | [!DNL Veeva CRM]帐户的用户名值。 |
| `password` | [!DNL Veeva CRM]帐户的密码值。 |
| `securityToken` | [!DNL Veeva CRM]实例的安全令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Veeva CRM]的连接规范ID为： `fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

有关这些值的详细信息，请参阅此[[!DNL Veeva CRM] 文档](https://developer.veevacrm.com/doc/Content/rest-api.htm)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Veeva CRM]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Veeva CRM]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | [!DNL Veeva CRM]基本连接的名称。 您可以使用此名称查找您的[!DNL Veeva CRM]基本连接。 |
| `description` | [!DNL Veeva CRM]基本连接的可选描述。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.environmentUrl` | [!DNL Veeva CRM]实例的URL。 |
| `auth.params.username` | [!DNL Veeva CRM]帐户的用户名值。 |
| `auth.params.password` | [!DNL Veeva CRM]帐户的密码值。 |
| `auth.params.securityToken` | [!DNL Veeva CRM]实例的安全令牌。 |
| `connectionSpec.id` | [!DNL Veeva CRM]的连接规范ID： `fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Veeva CRM]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将CRM数据引入Experience Platform](../../collect/crm.md)
