---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；Microsoft Dynamics；Dynamics；Dynamics
solution: Experience Platform
title: 使用流服务API创建Microsoft Dynamics基本连接
type: Tutorial
description: 了解如何使用Flow Service API将Platform连接到Microsoft Dynamics帐户。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API创建[!DNL Microsoft Dynamics]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Microsoft Dynamics]（以下称为“[!DNL Dynamics]”）创建基础连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时允许您使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功将Platform连接到Dynamics帐户所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到[!DNL Dynamics]，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 基本身份验证]

| 凭据 | 描述 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics]实例的服务URL。 |
| `username` | [!DNL Dynamics]用户帐户的用户名。 |
| `password` | [!DNL Dynamics]帐户的密码。 |

>[!TAB 服务主体和密钥身份验证]

| 凭据 | 描述 |
| --- | --- |
| `servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

>[!ENDTABS]

有关入门的详细信息，请参阅[此 [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

>[!TIP]
>
>创建后，无法更改[!DNL Dynamics]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL Dynamics]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

### 创建[!DNL Dynamics]基本连接

>[!TIP]
>
>创建后，无法更改[!DNL Dynamics]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

创建源连接的第一步是验证您的[!DNL Dynamics]源并生成基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并识别要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL Dynamics]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用基本身份验证创建[!DNL Dynamics]基本连接，请在提供连接的`serviceUri`、`username`和`password`的值时向[!DNL Flow Service] API发出POST请求。

+++请求

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | 与您的[!DNL Dynamics]实例关联的服务URI。 |
| `auth.params.username` | 与您的[!DNL Dynamics]帐户关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Dynamics]帐户关联的密码。 |
| `connectionSpec.id` | [!DNL Dynamics]连接规范ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++响应

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 基于服务主体密钥的身份验证]

要使用基于服务主体密钥的身份验证创建[!DNL Dynamics]基本连接，请向[!DNL Flow Service] API发出POST请求，同时为您连接的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`提供值。

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | 与您的[!DNL Dynamics]实例关联的服务URI。 |
| `auth.params.servicePrincipalId` | [!DNL Dynamics]帐户的客户端ID。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `auth.params.servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |
| `connectionSpec.id` | [!DNL Dynamics]连接规范ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++响应

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Microsoft Dynamics]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将CRM数据引入平台](../../collect/crm.md)
