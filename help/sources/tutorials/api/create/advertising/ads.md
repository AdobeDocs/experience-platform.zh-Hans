---
keywords: Experience Platform；主页；热门主题；Google广告；Google广告；Google广告；广告
title: 使用流服务API创建Google Ads基连接
description: 了解如何使用流量服务API将Adobe Experience Platform与Google Ads连接。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# 使用创建Google Ads基连接 [!DNL Flow Service] API

>[!NOTE]
>
>Google Ads源处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用创建Google Ads基本连接的步骤 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Experience Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 要与Google Ads连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | 客户ID是与您要通过Google Ads API管理的Google Ads客户帐户对应的帐号。 此ID遵循的模板是 `123-456-7890`. |
| `developerToken` | 开发人员令牌允许您访问Google Ads API。 您可以使用相同的开发人员令牌对所有Google广告帐户发出请求。 通过检索开发人员令牌 [登录您的manager帐户](https://ads.google.com/home/tools/manager-accounts/) 然后导航到 [!DNL API Center] 页面。 |
| `refreshToken` | 刷新令牌是 [!DNL OAuth2] 身份验证。 此令牌允许您在访问令牌过期后重新生成该令牌。 |
| `clientId` | 客户端ID与客户端密钥一起使用，作为 [!DNL OAuth2] 身份验证。 客户端ID和客户端密钥通过将您的应用程序标识到Google，使您的应用程序能够代表您的帐户运行。 |
| `clientSecret` | 客户端密钥与作为 [!DNL OAuth2] 身份验证。 客户端ID和客户端密钥通过将您的应用程序标识到Google，使您的应用程序能够代表您的帐户运行。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 Google广告的连接规范ID是： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

阅读API概述文档，以了解 [有关Google Ads快速入门的更多信息](https://developers.google.com/google-ads/api/docs/first-call/overview).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 端点时，将您的Google Ads身份验证凭据作为请求参数的一部分提供。

**API格式**

```https
POST /connections
```

**请求**

以下请求为Google Ads创建基本连接：

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
| `auth.params.clientCustomerID` | 您的Google Ads帐户的客户客户ID。 |
| `auth.params.developerToken` | 您的Google Ads帐户的开发人员令牌。 |
| `auth.params.refreshToken` | 您的Google Ads帐户的刷新令牌。 |
| `auth.params.clientID` | 您的Google Ads帐户的客户端ID。 |
| `auth.params.clientSecret` | 您的Google Ads帐户的客户端密钥。 |
| `connectionSpec.id` | Google Ads连接规范ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过阅读本教程，您已使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API](../../collect/advertising.md)
