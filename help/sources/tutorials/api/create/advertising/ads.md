---
keywords: Experience Platform；主页；热门主题；Google AdWords;Google AdWords;Adwords
solution: Experience Platform
title: 使用流服务API创建Google AdWords基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google AdWords。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# 创建 [!DNL Google AdWords] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Google AdWords] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Google AdWords] (以下简称“[!DNL AdWords]“)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL AdWords] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL AdWords]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | 的客户ID [!DNL AdWords] 帐户。 |
| `developerToken` | 与管理员帐户关联的开发人员令牌。 |
| `refreshToken` | 从获取的刷新令牌 [!DNL Google] 授权访问 [!DNL AdWords]. |
| `clientId` | 的客户端ID [!DNL Google] 用于获取刷新令牌的应用程序。 |
| `clientSecret` | 的客户端密钥 [!DNL Google] 用于获取刷新令牌的应用程序。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL AdWords] 为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

有关这些值的更多信息，请参阅此 [Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL AdWords] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL AdWords]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
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
| `auth.params.clientCustomerID` | 您的客户客户ID [!DNL AdWords] 帐户。 |
| `auth.params.developerToken` | 您的开发人员令牌 [!DNL AdWords] 帐户。 |
| `auth.params.refreshToken` | 的刷新令牌 [!DNL AdWords] 帐户。 |
| `auth.params.clientID` | 您的客户端ID [!DNL AdWords] 帐户。 |
| `auth.params.clientSecret` | 您的客户端密钥 [!DNL AdWords] 帐户。 |
| `connectionSpec.id` | 的 [!DNL Google AdWords] 连接规范ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Google AdWords] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API](../../collect/advertising.md)
