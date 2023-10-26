---
keywords: Experience Platform；主页；热门主题；Microsoft Dynamics；Microsoft Dynamics；Dynamics；Dynamics
solution: Experience Platform
title: 使用流服务API创建Microsoft Dynamics基本连接
type: Tutorial
description: 了解如何使用Flow Service API将Platform连接到Microsoft Dynamics帐户。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 3%

---

# 创建 [!DNL Microsoft Dynamics] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Microsoft Dynamics] (以下简称“[!DNL Dynamics]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了使用Platform成功连接到Dynamics帐户时需要了解的其他信息 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接到 [!DNL Dynamics]中，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 基本身份验证]

| 凭据 | 描述 |
| --- | --- |
| `serviceUri` | 您的服务URL [!DNL Dynamics] 实例。 |
| `username` | 的用户名 [!DNL Dynamics] 用户帐户。 |
| `password` | 您的密码 [!DNL Dynamics] 帐户。 |

>[!TAB 服务主体和密钥身份验证]

| 凭据 | 描述 |
| --- | --- |
| `servicePrincipalId` | 您的客户端ID [!DNL Dynamics] 帐户。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |

>[!ENDTABS]

有关入门的更多信息，请参阅 [此 [!DNL Dynamics] 文档](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Dynamics] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Dynamics] 作为请求参数一部分的身份验证凭据。

### 创建 [!DNL Dynamics] 基本连接

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Dynamics] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

创建源连接的第一步是验证您的 [!DNL Dynamics] 并生成基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并识别要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Dynamics] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本身份验证]

创建 [!DNL Dynamics] POST基本连接使用基本身份验证，向 [!DNL Flow Service] API，同时为您的连接提供值 `serviceUri`， `username`、和 `password`.

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
| `auth.params.serviceUri` | 与您的关联的服务URI [!DNL Dynamics] 实例。 |
| `auth.params.username` | 与您的关联的用户名 [!DNL Dynamics] 帐户。 |
| `auth.params.password` | 与您的关联的密码 [!DNL Dynamics] 帐户。 |
| `connectionSpec.id` | 此 [!DNL Dynamics] 连接规范ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++响应

成功响应将返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 基于服务主体密钥的身份验证]

创建 [!DNL Dynamics] 基本连接使用基于密钥的服务主体身份验证，向发出POST请求 [!DNL Flow Service] API，同时为您的连接提供值 `serviceUri`， `servicePrincipalId`、和 `servicePrincipalKey`.

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
| `auth.params.serviceUri` | 与您的关联的服务URI [!DNL Dynamics] 实例。 |
| `auth.params.servicePrincipalId` | 您的客户端ID [!DNL Dynamics] 帐户。 使用服务主体和基于密钥的身份验证时需要此ID。 |
| `auth.params.servicePrincipalKey` | 服务主体密钥。 使用服务主体和基于密钥的身份验证时需要此凭据。 |
| `connectionSpec.id` | 此 [!DNL Dynamics] 连接规范ID： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++响应

成功响应将返回新创建的连接，包括其唯一标识符(`id`)。 在下一步中探索您的CRM系统时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## 后续步骤

在本教程之后，您已创建一个 [!DNL Microsoft Dynamics] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将CRM数据引入Platform [!DNL Flow Service] API](../../collect/crm.md)
