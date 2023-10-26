---
title: 使用流服务API创建Azure Blob基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 3%

---

# 创建 [!DNL Azure Blob] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程提供了创建基本连接的步骤 [!DNL Azure Blob] (以下简称“[!DNL Blob]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功创建所需的其他信息 [!DNL Blob] 源连接使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以与您的 [!DNL Blob] 存储时，必须提供以下连接属性的值：

>[!BEGINTABS]

>[!TAB 连接字符串验证]

| 凭据 | 描述 |
| --- | --- |
| `connectionString` | 一个字符串，其中包含进行身份验证所需的授权信息 [!DNL Blob] Experience Platform。 此 [!DNL Blob] 连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 有关连接字符串的详细信息，请参阅此 [!DNL Blob] 文档 [配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Blob] 为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!TAB SAS URI身份验证]

| 凭据 | 描述 |
| --- | --- |
| `sasUri` | 共享访问签名URI，您可以将其用作连接您的主机和计算机的 [!DNL Blob] 帐户。 此 [!DNL Blob] SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 有关更多信息，请参阅此 [!DNL Blob] 文档 [共享访问签名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | 要为其指定访问权限的容器的名称。 使用创建新帐户时 [!DNL Blob] 源，您可以提供容器名称以指定用户对所选子文件夹的访问权限。 |
| `folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Blob] 为： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!ENDTABS]

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

>[!TIP]
>
>创建后，便无法更改的身份验证类型 [!DNL Blob] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

此 [!DNL Blob] 源支持连接字符串和共享访问签名(SAS)身份验证。 共享访问签名(SAS) URI允许将安全授权委派给您的 [!DNL Blob] 帐户。 您可以使用SAS创建具有不同访问级别的身份验证凭据，因为基于SAS的身份验证允许您设置权限、开始和到期日期，以及配置给特定资源。

在此步骤中，您还可以通过定义容器名称和子文件夹的路径来指定帐户将有权访问的子文件夹。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Blob] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

>[!BEGINTABS]

>[!TAB 连接字符串]

以下请求为创建基本连接 [!DNL Blob] 使用基于连接字符串的身份验证：

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
| `auth.params.connectionString` | 访问Blob存储中的数据所需的连接字符串。 Blob连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Blob存储连接规范ID为： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++响应

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB SAS URI身份验证]

创建 [!DNL Blob] POST连接使用共享访问签名URI，向 [!DNL Flow Service] API，同时为提供值 [!DNL Blob] `sasUri`.

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
| `auth.params.connectionString` | 访问中数据所需的SAS URI [!DNL Blob] 存储。 此 [!DNL Blob] SAS URI模式为： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | 此 [!DNL Blob] 存储连接规范ID为： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++响应

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## 后续步骤

在本教程之后，您已创建一个 [!DNL Blob] 连接使用API，并在响应正文中获取了唯一ID。 您可以使用此连接ID来 [使用流服务API浏览云存储](../../explore/cloud-storage.md).
