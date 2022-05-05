---
keywords: Experience Platform；主页；热门主题；ServiceNow
solution: Experience Platform
title: 使用流服务API创建ServiceNow Base连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到ServiceNow服务器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 创建 [!DNL ServiceNow] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Google ServiceNow] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到 [!DNL ServiceNow] 服务器使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接到 [!DNL ServiceNow]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | 的端点 [!DNL ServiceNow] 服务器。 |
| `username` | 用于连接到的用户名 [!DNL ServiceNow] 服务器进行身份验证。 |
| `password` | 连接到的密码 [!DNL ServiceNow] 服务器进行身份验证。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL ServiceNow] 为： `eb13cb25-47ab-407f-ba89-c0125281c563`. |

有关入门的更多信息，请参阅 [此ServiceNow文档](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL ServiceNow] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL ServiceNow]:

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
| `auth.params.server` | 您的 [!DNL ServiceNow] 服务器。 |
| `auth.params.username` | 用于连接到的用户名 [!DNL ServiceNow] 服务器进行身份验证。 |
| `auth.params.password` | 连接到的密码 [!DNL ServiceNow] 服务器进行身份验证。 |
| `connectionSpec.id` | 的 [!DNL ServiceNow] 连接规范ID: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL ServiceNow] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/customer-success.md)
