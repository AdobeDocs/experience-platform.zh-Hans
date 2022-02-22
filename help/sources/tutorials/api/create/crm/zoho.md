---
keywords: Experience Platform；主页；热门主题；Zoho CRM;Zoho CRM;Zoho;Zoho
solution: Experience Platform
title: 使用流服务API创建Zoho CRM基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Zoho CRM。
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 1%

---

# 创建 [!DNL Zoho CRM] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Zoho CRM] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Zoho CRM] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Zoho CRM]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| --- | --- |
| `endpoint` | 的端点 [!DNL Zoho CRM] 服务器。 |
| `accountsUrl` | 帐户URL用于生成访问和刷新令牌。 URL必须特定于域。 |
| `clientId` | 与 [!DNL Zoho CRM] 用户帐户。 |
| `clientSecret` | 与 [!DNL Zoho CRM] 用户帐户。 |
| `accessToken` | 访问令牌可授权您对 [!DNL Zoho CRM] 帐户。 |
| `refreshToken` | 刷新令牌是用于在您的访问令牌过期后生成新访问令牌的令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Zoho CRM] 为： `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

有关这些凭据的更多信息，请参阅 [[!DNL Zoho CRM] 身份验证](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Zoho CRM] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

>[!TIP]
>
>您的帐户URL域必须与您相应的域位置相对应。 以下是各种域及其相应的帐户URL:<ul><li>美国：https://accounts.zoho.com</li><li>澳大利亚：https://accounts.zoho.com.au</li><li>欧洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中国：https://accounts.zoho.com.cn</li></ul>

以下请求会为 [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 您的 [!DNL Zoho CRM] 基本连接。 您可以使用此名称查找 [!DNL Zoho CRM] 基本连接。 |
| `description` | 您的 [!DNL Zoho CRM] 基本连接。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.endpoint` | 的端点 [!DNL Zoho CRM] 服务器。 |
| `auth.params.accountsUrl` | 帐户URL用于生成访问和刷新令牌。 URL必须特定于域。 |
| `auth.params.clientId` | 与 [!DNL Zoho CRM] 用户帐户。 |
| `auth.params.clientSecret` | 与 [!DNL Zoho CRM] 用户帐户。 |
| `auth.params.accessToken` | 访问令牌可授权您对 [!DNL Zoho CRM] 帐户。 |
| `auth.params.refreshToken` | 刷新令牌是用于在您的访问令牌过期后生成新访问令牌的令牌。 |
| `connectionSpec.id` | 的连接规范ID [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Zoho CRM] 基本连接使用 [!DNL Flow Service] API，并已获取连接的唯一ID值。 在下一个教程中，您可以使用此ID来了解如何 [使用流量服务API探索CRM系统](../../explore/crm.md).
