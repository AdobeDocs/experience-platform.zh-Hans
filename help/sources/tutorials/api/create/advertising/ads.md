---
title: 使用API将Google Ads连接到Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google Ads。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API将[!DNL Google Ads]连接到Experience Platform

>[!NOTE]
>
>[!DNL Google Ads]源为测试版。 有关使用测试版标记源的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

阅读本教程，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Google Ads]帐户连接到Adobe Experience Platform。

## 开始使用

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Google Ads]所需了解的其他信息。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Google Ads] 源概述](../../../../connectors/advertising/ads.md)。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的Google Ads身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

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
              "refreshToken": "{REFRESH_TOKEN}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "googleAdsApiVersion": "v17"

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
| `auth.params.clientCustomerID` | [!DNL Google Ads]帐户的客户端客户ID。 |
| `auth.params.loginCustomerID` | 与您的[!DNL Google Ads]经理帐户对应的登录客户ID。 |
| `auth.params.developerToken` | [!DNL Google Ads]帐户的开发人员令牌。 |
| `auth.params.refreshToken` | [!DNL Google Ads]帐户的刷新令牌。 |
| `auth.params.clientID` | [!DNL Google Ads]帐户的客户端ID。 |
| `auth.params.clientSecret` | [!DNL Google Ads]帐户的客户端密钥。 |
| `auth.params.googleAdsApiVersion` | 您正在使用的[!DNL Google Ads] API版本。 Experience Platform支持的最新版本是`v17`。 |
| `connectionSpec.id` | [!DNL Google Ads]连接规范ID： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 创建数据流以摄取广告数据

通过学习本教程，您已使用[!DNL Flow Service] API创建了[!DNL Google Ads]基本连接，并将您的[!DNL Google Ads]帐户连接到Experience Platform。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将广告数据引入平台](../../collect/advertising.md)
