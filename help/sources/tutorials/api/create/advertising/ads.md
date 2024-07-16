---
title: 使用流服务API创建Google Ads基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google Ads。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API创建Google Ads基本连接

>[!WARNING]
>
>[!DNL Google Ads]源暂时不可用。 Adobe正在努力解决此源的问题。

>[!NOTE]
>
>Google广告源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为Google Ads创建基本连接的步骤。

## 开始使用

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到Google Ads时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与Google Ads连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | 客户端客户ID是与您要使用Google Ads API管理的Google Ads客户端帐户对应的帐号。 此ID遵循`123-456-7890`模板。 |
| `loginCustomerId` | 登录客户ID是与您的Google广告管理器帐户对应的帐号，用于从特定的运营客户获取报表数据。 有关登录客户ID的详细信息，请阅读[Google Ads API文档](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)。 |
| `developerToken` | 通过开发人员令牌，您可以访问Google Ads API。 您可以使用相同的开发人员令牌针对所有Google Ads帐户发出请求。 通过[登录到您的经理帐户](https://ads.google.com/home/tools/manager-accounts/)并导航到[!DNL API Center]页面来检索您的开发人员令牌。 |
| `refreshToken` | 刷新令牌是[!DNL OAuth2]身份验证的一部分。 此令牌允许您在访问令牌过期后重新生成访问令牌。 |
| `clientId` | 客户端ID与客户端密钥结合使用，作为[!DNL OAuth2]身份验证的一部分。 通过同时使用客户端ID和客户端密钥，您的应用程序可以在Google中标识您的应用程序，从而代表您的帐户运行。 |
| `clientSecret` | 客户端密钥与客户端ID结合使用，作为[!DNL OAuth2]身份验证的一部分。 通过同时使用客户端ID和客户端密钥，您的应用程序可以在Google中标识您的应用程序，从而代表您的帐户运行。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 Google Ads的连接规范ID为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

阅读[有关Google Ads入门的更多信息](https://developers.google.com/google-ads/api/docs/first-call/overview)的API概述文档。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供Google Ads身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建Google Ads的基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Google Ads帐户的客户端客户ID。 |
| `auth.params.loginCustomerID` | 与您的Google广告管理器帐户对应的登录客户ID 。 |
| `auth.params.developerToken` | Google Ads帐户的开发人员令牌。 |
| `auth.params.refreshToken` | Google Ads帐户的刷新令牌。 |
| `auth.params.clientID` | Google Ads帐户的客户端ID。 |
| `auth.params.clientSecret` | 您的Google Ads帐户的客户端密码。 |
| `connectionSpec.id` | Google Ads连接规范ID： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API创建了Google Ads基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将广告数据引入平台](../../collect/advertising.md)
