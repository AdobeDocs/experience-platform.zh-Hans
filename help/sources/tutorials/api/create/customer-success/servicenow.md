---
keywords: Experience Platform；主页；热门主题；ServiceNow
solution: Experience Platform
title: 使用流服务API创建ServiceNow Base连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到ServiceNow服务器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL ServiceNow]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Google ServiceNow]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL ServiceNow]服务器。

### 收集所需的凭据

要使[!DNL Flow Service]连接到[!DNL ServiceNow]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow]服务器的端点。 |
| `username` | 用于连接到[!DNL ServiceNow]服务器以进行身份验证的用户名。 |
| `password` | 连接到[!DNL ServiceNow]服务器以进行身份验证的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL ServiceNow]的连接规范ID是：`eb13cb25-47ab-407f-ba89-c0125281c563`。 |

有关入门的更多信息，请参阅[此ServiceNow文档](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL ServiceNow]身份验证凭据时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.username` | 用于连接到[!DNL ServiceNow]服务器以进行身份验证的用户名。 |
| `auth.params.password` | 连接到[!DNL ServiceNow]服务器以进行身份验证的密码。 |
| `connectionSpec.id` | [!DNL ServiceNow]连接规范ID:`eb13cb25-47ab-407f-ba89-c0125281c563` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL ServiceNow]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何使用流量服务API](../../explore/customer-success.md)探索客户成功系统。[
