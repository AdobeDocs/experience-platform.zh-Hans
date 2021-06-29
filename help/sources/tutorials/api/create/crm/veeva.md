---
keywords: Experience Platform；主页；热门主题；Veeva CRM;Veeva CRM;Veeva;
solution: Experience Platform
title: 使用流服务API创建Veeva CRM基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Veeva CRM。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 9bd241d5f986759268edd072cee72d02f40f858f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# （Beta版）使用[!DNL Flow Service] API创建[!DNL Veeva CRM]基本连接

>[!NOTE]
>
>[!DNL Veeva CRM]源位于测试版中。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Veeva CRM]创建基本连接的步骤。

## 入门指南

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用[!DNL Flow Service] API成功连接到[!DNL Veeva CRM]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Veeva CRM]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM]实例的URL。 |
| `username` | [!DNL Veeva CRM]帐户的用户名值。 |
| `password` | [!DNL Veeva CRM]帐户的密码值。 |
| `securityToken` | [!DNL Veeva CRM]实例的安全令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Veeva CRM]的连接规范ID是：`fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

有关这些值的详细信息，请参阅此[[!DNL Veeva CRM] 文档](https://developer.veevacrm.com/api/#order-management-rest-api)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Veeva CRM]身份验证凭据时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | [!DNL Veeva CRM]基本连接的名称。 您可以使用此名称查找[!DNL Veeva CRM]基本连接。 |
| `description` | [!DNL Veeva CRM]基本连接的可选描述。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.environmentUrl` | [!DNL Veeva CRM]实例的URL。 |
| `auth.params.username` | [!DNL Veeva CRM]帐户的用户名值。 |
| `auth.params.password` | [!DNL Veeva CRM]帐户的密码值。 |
| `auth.params.securityToken` | [!DNL Veeva CRM]实例的安全令牌。 |
| `connectionSpec.id` | [!DNL Veeva CRM]的连接规范ID:`fcad62f3-09b0-41d3-be11-449d5a621b69`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Veeva CRM]基本连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流量服务API](../../explore/crm.md)探索CRM系统。
