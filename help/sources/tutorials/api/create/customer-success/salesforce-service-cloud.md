---
keywords: Experience Platform；主页；热门主题；Salesforce服务云；Salesforce服务云
solution: Experience Platform
title: 使用流服务API创建Salesforce服务云源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: ff0f6bc6b8a57b678b329fe2b47c53919e0e2d64
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Salesforce Service Cloud]源连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Salesforce Service Cloud]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL Salesforce Service Cloud]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Salesforce Service Cloud]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | [!DNL Salesforce Service Cloud]用户帐户的用户名。 |
| `password` | [!DNL Salesforce Service Cloud]帐户的密码。 |
| `securityToken` | [!DNL Salesforce Service Cloud]帐户的安全令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Salesforce Service Cloud]的连接规范ID是：`b66ab34-8619-49cb-96d1-39b37ede86ea`。 |

有关入门的详细信息，请参阅[此Salesforce服务云文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Salesforce Service Cloud]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL Salesforce Service Cloud]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.username` | 与您的[!DNL Salesforce Service Cloud]帐户关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Salesforce Service Cloud]帐户关联的密码。 |
| `auth.params.securityToken` | 与您的[!DNL Salesforce Service Cloud]帐户关联的安全令牌。 |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud]连接规范ID:`b66ab34-8619-49cb-96d1-39b37ede86ea` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce Service Cloud]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何使用流量服务API](../../explore/customer-success.md)探索客户成功系统。[
