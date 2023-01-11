---
keywords: Experience Platform；主页；热门主题；Salesforce服务云；Salesforce服务云
solution: Experience Platform
title: 使用流服务API创建Salesforce服务云源连接
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 创建 [!DNL Salesforce Service Cloud] 源连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Salesforce Service Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Salesforce Service Cloud] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Salesforce Service Cloud]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 您的用户名 [!DNL Salesforce Service Cloud] 用户帐户。 |
| `password` | 您的密码 [!DNL Salesforce Service Cloud] 帐户。 |
| `securityToken` | 您的安全令牌 [!DNL Salesforce Service Cloud] 帐户。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Salesforce Service Cloud] 为： `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

有关入门的更多信息，请参阅 [此Salesforce服务云文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Salesforce Service Cloud] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.username` | 与您的 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.password` | 与 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.securityToken` | 与 [!DNL Salesforce Service Cloud] 帐户。 |
| `connectionSpec.id` | 的 [!DNL Salesforce Service Cloud] 连接规范ID: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Salesforce Service Cloud] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/customer-success.md)
