---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics;microsoft Dynamics;dynamics;Dynamics
solution: Experience Platform
title: 使用Flow Service API创建Microsoft Dynamics连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Platform连接到Microsoft Dynamics（以下简称“Dynamics”）帐户以收集CRM数据的步骤。
translation-type: tm+mt
source-git-commit: 75566ef0dc45f59b47af0b85f4692c2496e53f29
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API创建[!DNL Microsoft Dynamics]连接器

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将平台连接到用于收集CRM数据的[!DNL Microsoft Dynamics]（以下简称“Dynamics”）帐户的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API将平台成功连接到Dynamics帐户所需了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]连接到[!DNL Dynamics]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的口令。 |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

有关入门的详细信息，请访问[this [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中的[如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用平台API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL Dynamics]帐户只需要一个连接，因为它可用于创建多个数据流以引入不同的数据。

### 使用基本身份验证创建[!DNL Dynamics]连接

要使用基本身份验证创建[!DNL Dynamics]连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`serviceUri`、`username`和`password`提供值。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL Dynamics]连接，其唯一连接规范ID必须作为POST请求的一部分提供。 [!DNL Dynamics]的连接规范ID为`38ad80fe-8b06-4938-94f4-d4ee80266b07`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUri` | 与[!DNL Dynamics]实例关联的服务URI。 |
| `auth.params.username` | 与您的[!DNL Dynamics]帐户关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Dynamics]帐户关联的密码。 |
| `connectionSpec.id` | 在上一步骤中检索的[!DNL Dynamics]帐户的连接规范`id`。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID才能在下一步中浏览您的CRM系统。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 使用基于服务主体密钥的身份验证创建[!DNL Dynamics]连接

要使用基于服务主体密钥的身份验证创建[!DNL Dynamics]连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`提供值。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUri` | 与[!DNL Dynamics]实例关联的服务URI。 |
| `auth.params.servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `auth.params.servicePrincipalKey` | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID才能在下一步中浏览您的CRM系统。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 后续步骤

按照本教程，您已使用[!DNL Flow Service] API创建了[!DNL Dynamics]连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/crm.md)浏览CRM系统。