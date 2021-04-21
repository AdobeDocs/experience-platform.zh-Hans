---
keywords: Experience Platform；主页；热门主题；Salesforce;salesforce
solution: Experience Platform
title: 使用流服务API创建Salesforce源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Salesforce帐户。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL Salesforce]源连接

流服务用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成使用流服务API将[!DNL Platform]连接到[!DNL Salesforce]帐户的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用[!DNL Flow Service] API将[!DNL Platform]成功连接到[!DNL Salesforce]帐户。

### 收集所需凭据

要使[!DNL Flow Service]连接到[!DNL Salesforce]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Salesforce]源实例的URL。 |
| `username` | [!DNL Salesforce]用户帐户的用户名。 |
| `password` | [!DNL Salesforce]用户帐户的口令。 |
| `securityToken` | [!DNL Salesforce]用户帐户的安全令牌。 |

有关快速入门的详细信息，请访问[此Salesforce文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL Salesforce]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL Salesforce]连接，必须在POST请求中提供其唯一连接规范ID。 [!DNL Salesforce]的连接规范ID为`cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.username` | 与您的[!DNL Salesforce]帐户关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Salesforce]帐户关联的密码。 |
| `auth.params.securityToken` | 与您的[!DNL Salesforce]帐户关联的安全令牌。 |
| `connectionSpec.id` | 在上一步中检索到的[!DNL Salesforce]帐户的连接规范`id`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中浏览您的CRM系统时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce]连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如何[使用流服务API](../../explore/crm.md)浏览CRM系统。
