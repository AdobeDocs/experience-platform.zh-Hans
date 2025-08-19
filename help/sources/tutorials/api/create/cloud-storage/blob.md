---
title: 使用流服务API将Azure Blob Storage连接到Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# 使用API将[!DNL Azure Blob Storage]连接到Experience Platform

阅读本指南，了解如何使用[!DNL Azure Blobg Storage]API[[!DNL Flow Service] 将您的](https://developer.adobe.com/experience-platform-apis/references/flow-service/)帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Azure Blob Storage] 概述](../../../../connectors/cloud-storage/blob.md#authentication)。

## 将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform {#connect}

有关如何将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform的信息，请阅读以下步骤。

### 创建基本连接

>[!NOTE]
>
>创建后，无法更改[!DNL Azure Blob Storage]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

基本连接可将您的源链接到Experience Platform，以存储身份验证详细信息、连接状态和唯一ID。 使用此ID浏览源文件并标识要摄取的特定项目，包括其数据类型和格式。

您可以使用以下身份验证类型将您的[!DNL Azure Blob Storage]帐户连接到Experience Platform：

* **帐户密钥身份验证**：使用存储帐户的访问密钥进行身份验证并连接到您的[!DNL Azure Blob Storage]帐户。
* **共享访问签名(SAS)**：使用SAS URI为您的[!DNL Azure Blob Storage]帐户中的资源提供委派的、有时间限制的访问。
* **基于服务主体的身份验证**：使用Azure Active Directory (AAD)服务主体（客户端ID和密码）对您的Azure Blob存储帐户进行安全身份验证。

**API格式**

```https
POST /connections
```

要创建基本连接ID，请向`/connections`端点发出POST请求，并提供您的身份验证凭据作为请求参数的一部分。

>[!BEGINTABS]

>[!TAB 帐户密钥身份验证]

若要使用帐户密钥身份验证，请提供您的`connectionString`、`container`和`folderPath`的值。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `connectionString` | [!DNL Azure Blob Storage]帐户的连接字符串。 连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`。 |
| `container` | 存储数据文件的[!DNL Azure Blob Storage]容器的名称。 |
| `folderPath` | 指定容器中文件所在的路径。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]源的连接规范ID。 此ID被固定为： `4c10e202-c428-4796-9208-5f1f5732b1cf`。 |

>[!TAB 共享访问签名]

要使用共享访问签名，请为您的`sasUri`、`container`和`folderPath`提供值。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `sasUri` | 共享访问签名URI，您可以将其用作连接帐户的替代身份验证类型。 SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`。 |
| `container` | 存储数据文件的[!DNL Azure Blob Storage]容器的名称。 |
| `folderPath` | 指定容器中文件所在的路径。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]源的连接规范ID。 此ID被固定为： `4c10e202-c428-4796-9208-5f1f5732b1cf`。 |

>[!TAB 基于服务主体的身份验证]

要通过基于服务主体的身份验证进行连接，请提供以下各项的值： `serviceEndpoint`、`servicePrincipalId`、`servicePrincipalKey`、`accountKind`、`tenant`、`container`和`folderPath`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `serviceEndpoint` | [!DNL Azure Blob Storage]帐户的终结点URL。 通常采用以下格式： `https://{ACCOUNT_NAME}.blob.core.windows.net`。 |
| `servicePrincipalId` | 用于身份验证的Azure Active Directory (AAD)服务主体的客户端/应用程序ID。 |
| `servicePrincipalKey` | 与Azure服务主体关联的客户端密钥或密码。 |
| `accountKind` | [!DNL Azure Blob Storage]帐户的类型。 通用值包括`StorageV2`、`BlobStorage`或`Storage`。 |
| `tenant` | 注册服务主体的Azure Active Directory (AAD)租户ID。 |
| `container` | 存储数据文件的[!DNL Azure Blob Storage]容器的名称。 |
| `folderPath` | 指定容器中文件所在的路径。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]源的连接规范ID。 此ID被固定为： `4c10e202-c428-4796-9208-5f1f5732b1cf`。 |

>[!ENDTABS]

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## 后续步骤

按照本教程，您已使用API创建了[!DNL Blob]连接，并获取了唯一ID作为响应正文的一部分。 您可以使用此连接ID以使用流服务API[来](../../explore/cloud-storage.md)浏览云存储。
