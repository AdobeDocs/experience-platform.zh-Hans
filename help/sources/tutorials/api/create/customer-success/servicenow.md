---
keywords: Experience Platform；主页；热门主题；servicenow；ServiceNow
solution: Experience Platform
title: 使用流服务API创建ServiceNow基本连接
type: Tutorial
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到ServiceNow服务器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL ServiceNow]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Google ServiceNow]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL ServiceNow]服务器所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到[!DNL ServiceNow]，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow]服务器的终结点。 |
| `username` | 用于连接到[!DNL ServiceNow]服务器进行身份验证的用户名。 |
| `password` | 用于连接到[!DNL ServiceNow]服务器以进行身份验证的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL ServiceNow]的连接规范ID为： `eb13cb25-47ab-407f-ba89-c0125281c563`。 |

有关入门的详细信息，请参阅[此ServiceNow文档](https://developer.servicenow.com/app.do#!/rest_api_doc？v=newyork&amp;id=r_TableAPI-GET)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL ServiceNow]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL ServiceNow]创建基本连接：

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.server` | [!DNL ServiceNow]服务器的端点。 |
| `auth.params.username` | 用于连接到[!DNL ServiceNow]服务器进行身份验证的用户名。 |
| `auth.params.password` | 用于连接到[!DNL ServiceNow]服务器以进行身份验证的密码。 |
| `connectionSpec.id` | [!DNL ServiceNow]连接规范ID： `eb13cb25-47ab-407f-ba89-c0125281c563` |

**响应**

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL ServiceNow]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将客户成功数据引入Experience Platform](../../collect/customer-success.md)
