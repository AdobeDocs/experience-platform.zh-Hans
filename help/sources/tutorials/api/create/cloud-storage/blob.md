---
title: 使用流服务API创建Azure Blob基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API创建[!DNL Azure Blob]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程提供了使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Azure Blob]（以下称为“[!DNL Blob]”）创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功创建[!DNL Blob]源连接所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]连接到[!DNL Blob]存储，您必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 连接字符串身份验证]

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 一个字符串，其中包含向Experience Platform验证[!DNL Blob]所需的授权信息。 [!DNL Blob]连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有关连接字符串的详细信息，请参阅[配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)上的此[!DNL Blob]文档。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Blob]的连接规范ID为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

>[!TAB SAS URI身份验证]

| 凭据 | 描述 |
| --- | --- |
| `sasUri` | 共享访问签名URI，您可以将其用作替代身份验证类型来连接您的[!DNL Blob]帐户。 [!DNL Blob] SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`有关详细信息，请参阅[共享访问签名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)上的此[!DNL Blob]文档。 |
| `container` | 要为其指定访问权限的容器的名称。 在使用[!DNL Blob]源创建新帐户时，您可以提供容器名称以指定用户对您选择的子文件夹的访问权限。 |
| `folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Blob]的连接规范ID为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

>[!ENDTABS]

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

>[!TIP]
>
>创建后，无法更改[!DNL Blob]基本连接的身份验证类型。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

[!DNL Blob]源支持连接字符串和共享访问签名(SAS)身份验证。 共享访问签名(SAS) URI允许向您的[!DNL Blob]帐户安全委派授权。 您可以使用SAS创建具有不同访问级别的身份验证凭据，因为基于SAS的身份验证允许您设置权限、开始和到期日期，以及配置给特定资源。

在此步骤中，您还可以通过定义容器名称和子文件夹的路径来指定帐户将有权访问的子文件夹。

要创建基本连接ID，请在提供您的[!DNL Blob]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

>[!BEGINTABS]

>[!TAB 连接字符串]

以下请求使用基于连接字符串的身份验证为[!DNL Blob]创建基本连接：

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
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
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

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 访问Blob存储中的数据所需的连接字符串。 Blob连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | Blob存储连接规范ID为： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++响应

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB SAS URI身份验证]

若要使用共享访问签名URI创建[!DNL Blob]连接，请在为[!DNL Blob] `sasUri`提供值的同时向[!DNL Flow Service] API发出POST请求。

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
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
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

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 访问[!DNL Blob]存储中的数据所需的SAS URI。 [!DNL Blob] SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`。 |
| `connectionSpec.id` | [!DNL Blob]存储连接规范ID为： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++响应

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## 后续步骤

按照本教程，您已使用API创建了[!DNL Blob]连接，并获取了唯一ID作为响应正文的一部分。 您可以使用此连接ID以使用流服务API[&#128279;](../../explore/cloud-storage.md)来浏览云存储。
