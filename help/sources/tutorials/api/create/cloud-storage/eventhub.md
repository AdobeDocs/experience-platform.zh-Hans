---
title: 使用流服务API创建Azure事件中心Source连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure事件中心帐户。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL Azure Event Hubs]源连接

>[!IMPORTANT]
>
>[!DNL Azure Event Hubs]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本教程，了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[!DNL Azure Event Hubs]（以下简称“[!DNL Event Hubs]”）连接到Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

- [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
- [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功将[!DNL Event Hubs]连接到Experience Platform所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与您的[!DNL Event Hubs]帐户连接，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 标准身份验证]

| 凭据 | 描述 |
| --- | --- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | [!DNL Event Hubs]命名空间的主键。 `sasKey`对应的`sasPolicy`必须配置`manage`权限才能填充[!DNL Event Hubs]列表。 |
| `namespace` | 您正在访问的[!DNL Event Hub]的命名空间。 [!DNL Event Hub]命名空间提供了一个唯一的范围容器，您可以在其中创建一个或多个[!DNL Event Hubs]。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Event Hubs]连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

>[!TAB SAS身份验证]

| 凭据 | 描述 |
| --- | --- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | [!DNL Event Hubs]命名空间的主键。 `sasKey`对应的`sasPolicy`必须配置`manage`权限才能填充[!DNL Event Hubs]列表。 |
| `namespace` | 您正在访问的[!DNL Event Hub]的命名空间。 [!DNL Event Hub]命名空间提供了一个唯一的范围容器，您可以在其中创建一个或多个[!DNL Event Hubs]。 |
| `eventHubName` | 填写您的[!DNL Azure Event Hub]名称。 有关[!DNL Event Hub]名称的详细信息，请阅读[Microsoft文档](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Event Hubs]连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |

有关[!DNL Event Hubs]的共享访问签名(SAS)身份验证的更多信息，请阅读有关使用SAS](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)的[[!DNL Azure] 指南。

>[!TAB 事件中心Azure Active Directory身份验证]

| 凭据 | 描述 |
| --- | --- |
| `tenantId` | 要从中请求权限的租户ID。 可以将您的租户ID格式化为GUID或友好名称。 **注意**：租户ID在[!DNL Microsoft Azure]界面中称为“目录ID”。 |
| `clientId` | 分配给您应用程序的应用程序ID。 您可以从注册[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]门户检索此ID。 |
| `clientSecretValue` | 与客户端ID一起用于对应用程序进行身份验证的客户端密码。 您可以从注册[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]门户中检索客户端密钥。 |
| `namespace` | 您正在访问的[!DNL Event Hub]的命名空间。 [!DNL Event Hub]命名空间提供了一个唯一的范围容器，您可以在其中创建一个或多个[!DNL Event Hubs]。 |

有关[!DNL Azure Active Directory]的详细信息，请阅读有关使用Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)的[Azure指南。

>[!TAB 事件中心范围的Azure Active Directory身份验证]

| 凭据 | 描述 |
| --- | --- |
| `tenantId` | 要从中请求权限的租户ID。 可以将您的租户ID格式化为GUID或友好名称。 **注意**：租户ID在[!DNL Microsoft Azure]界面中称为“目录ID”。 |
| `clientId` | 分配给您应用程序的应用程序ID。 您可以从注册[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]门户检索此ID。 |
| `clientSecretValue` | 与客户端ID一起用于对应用程序进行身份验证的客户端密码。 您可以从注册[!DNL Azure Active Directory]的[!DNL Microsoft Entra ID]门户中检索客户端密钥。 |
| `namespace` | 您正在访问的[!DNL Event Hub]的命名空间。 [!DNL Event Hub]命名空间提供了一个唯一的范围容器，您可以在其中创建一个或多个[!DNL Event Hubs]。 |
| `eventHubName` | 填写您的[!DNL Azure Event Hub]名称。 有关[!DNL Event Hub]名称的详细信息，请阅读[Microsoft文档](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)。 |

>[!ENDTABS]

有关这些值的详细信息，请参阅[此事件中心文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

>[!TIP]
>
>创建后，无法更改[!DNL Event Hubs]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

创建源连接的第一步是验证您的[!DNL Event Hubs]源并生成基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并识别要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Event Hubs]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 标准身份验证]

要使用标准身份验证创建帐户，请在为您的`sasKeyName`、`sasKey`和`namespace`提供值时向`/connections`端点发出POST请求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}"
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `auth.params.sasKey` | 生成的共享访问签名。 |
| `auth.params.namespace` | 您正在访问的[!DNL Event Hubs]的命名空间。 |
| `connectionSpec.id` | [!DNL Event Hubs]连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++响应

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB SAS身份验证]

要使用SAS身份验证创建帐户，请在为您的`sasKeyName`、`sasKey`、`namespace`和`eventHubName`提供值时向`/connections`端点发出POST请求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `auth.params.sasKey` | 生成的共享访问签名。 |
| `auth.params.namespace` | 您正在访问的[!DNL Event Hubs]的命名空间。 |
| `params.eventHubName` | [!DNL Event Hubs]源的名称。 |
| `connectionSpec.id` | [!DNL Event Hubs]连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++响应

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB 事件中心Azure Active Directory身份验证]

要使用Azure Active Directory身份验证创建帐户，请在为您的`tenantId`、`clientId`、`clientSecretValue`和`namespace`提供值时向`/connections`端点发出POST请求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.tenantId` | 应用程序的租户ID。 **注意**：租户ID在[!DNL Microsoft Azure]界面中称为“目录ID”。 |
| `auth.params.clientId` | 您组织的客户端ID。 |
| `auth.params.clientSecretValue` | 您组织的客户端密钥值。 |
| `auth.params.namespace` | 您正在访问的[!DNL Event Hubs]的命名空间。 |
| `connectionSpec.id` | [!DNL Event Hubs]连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++响应

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB 事件中心范围的Azure Active Directory身份验证]

要使用Azure Active Directory身份验证创建帐户，请在为您的`tenantId`、`clientId`、`clientSecretValue`、`namespace`和`eventHubName`提供值时向`/connections`端点发出POST请求。

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
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.tenantId` | 应用程序的租户ID。 **注意**：租户ID在[!DNL Microsoft Azure]界面中称为“目录ID”。 |
| `auth.params.clientId` | 您组织的客户端ID。 |
| `auth.params.clientSecretValue` | 您组织的客户端密钥值。 |
| `auth.params.namespace` | 您正在访问的[!DNL Event Hubs]的命名空间。 |
| `auth.params.eventHubName` | [!DNL Event Hubs]源的名称。 |
| `connectionSpec.id` | [!DNL Event Hubs]连接规范ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++响应

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此连接ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## 创建源连接

>[!TIP]
>
>[!DNL Event Hubs]使用者组只能在给定时间用于单个流。

源连接创建和管理与摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和组织。

要创建源连接，请向[!DNL Flow Service] API的`/sourceConnections`端点发出POST请求。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Azure Event Hubs source connection",
      "description": "A source connection for Azure Event Hubs",
      "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 在上一步中生成的[!DNL Event Hubs]源的连接ID。 |
| `connectionSpec.id` | [!DNL Event Hubs]的固定连接规范ID。 此ID为： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`。 |
| `data.format` | 要摄取的[!DNL Event Hubs]数据的格式。 当前，唯一支持的数据格式为`json`。 |
| `params.eventHubName` | [!DNL Event Hubs]源的名称。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw`和`xdm`。 |
| `params.reset` | 此参数定义数据的读取方式。 使用`latest`开始读取最新数据，并使用`earliest`开始读取流中的第一个可用数据。 此参数是可选的，如果未提供，则默认为`earliest`。 |
| `params.consumerGroup` | 要用于[!DNL Event Hubs]的发布或订阅机制。 此参数是可选的，如果未提供，则默认为`$Default`。 有关详细信息，请参阅此[[!DNL Event Hubs] 关于事件使用者](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers)的指南。 **注意**： [!DNL Event Hubs]使用者组只能在给定时间用于单个流。 |

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API创建了[!DNL Event Hubs]源连接。 您可以在下一个教程中使用此源连接ID来[使用 [!DNL Flow Service] API](../../collect/streaming.md)创建流式数据流。
