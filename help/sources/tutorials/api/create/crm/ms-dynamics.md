---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: 使用流服务API创建Microsoft Dynamics基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Platform连接到Microsoft Dynamics帐户。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 8035539321f5016521208aa110a4ee2881cb5d1e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL Microsoft Dynamics]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Microsoft Dynamics]（以下称“[!DNL Dynamics]”）创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了要使用[!DNL Flow Service] API将Platform成功连接到Dynamics帐户所需了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]连接到[!DNL Dynamics]，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的密码。 |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Dynamics]的连接规范ID是：`38ad80fe-8b06-4938-94f4-d4ee80266b07`。 |

有关入门的更多信息，请访问[this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Dynamics]身份验证凭据时，向`/connections`端点发出POST请求。

### 使用基本身份验证创建[!DNL Dynamics]基本连接

要使用基本身份验证创建[!DNL Dynamics]基本连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`serviceUri`、`username`和`password`提供值。

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
| `connectionSpec.id` | [!DNL Dynamics]连接规范ID:`38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### 使用基于服务主体密钥的身份验证创建[!DNL Dynamics]基本连接

要使用基于服务主体密钥的身份验证创建[!DNL Dynamics]基本连接，请向[!DNL Flow Service] API发出POST请求，同时为连接的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`提供值。

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
| `connectionSpec.id` | [!DNL Dynamics]连接规范ID:`38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID，才能在下一步中探索您的CRM系统。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Dynamics]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流量服务API](../../explore/crm.md)探索CRM系统。
