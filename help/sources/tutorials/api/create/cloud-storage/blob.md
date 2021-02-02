---
keywords: Experience Platform；主页；热门主题；Azure;azure blob;blob;Blob
solution: Experience Platform
title: 使用流服务API创建Azure Blob连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到Azure Blob（以下称“Blob”）存储的步骤。
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API创建[!DNL Azure Blob]连接器

本教程使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)指导您完成将[!DNL Azure Blob]（以下简称“Blob”）连接到Experience Platform的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用[!DNL Flow Service] API成功创建[!DNL Blob]源连接器。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Blob]存储连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 包含验证[!DNL Blob]为Experience Platform所必需的授权信息的字符串。 [!DNL Blob]连接字符串模式为：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 有关连接字符串的详细信息，请参阅[配置连接字符串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)的此[!DNL Blob]文档。 |
| `sasUri` | 可用作连接[!DNL Blob]帐户的替代身份验证类型的共享访问签名URI。 [!DNL Blob] SAS URI模式为：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`有关详细信息，请参阅此[!DNL Blob]文档，关于[共享访问签名URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication)。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 [!DNL Blob]的连接规范ID为：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

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

连接指定源并包含该源的凭据。 每个[!DNL Blob]帐户只需要一个连接，因为它可用于创建多个数据流以引入不同的数据。

### 使用基于连接字符串的身份验证创建[!DNL Blob]连接

要使用基于连接字符串的身份验证创建[!DNL Blob]连接，请在提供[!DNL Blob] `connectionString`时向[!DNL Flow Service] API发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL Blob]连接，其唯一连接规范ID必须作为POST请求的一部分提供。 [!DNL Blob]的连接规范ID为`4c10e202-c428-4796-9208-5f1f5732b1cf`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
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
| `auth.params.connectionString` | 访问Blob存储中的数据所需的连接字符串。 Blob连接字符串模式为：`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |
| `connectionSpec.id` | Blob存储连接规范ID为：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览您的存储需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### 使用共享访问签名URI创建[!DNL Blob]连接

共享访问签名(SAS)URI允许对您的[!DNL Blob]帐户进行安全授权。 您可以使用SAS创建不同访问权限的身份验证凭据，因为基于SAS的身份验证允许您设置权限、开始和到期日期，以及为特定资源提供资源。

要使用共享访问签名URI创建[!DNL Blob]连接，请向[!DNL Flow Service] API发出POST请求，同时为[!DNL Blob] `sasUri`提供值。

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
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
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
| `auth.params.connectionString` | 访问[!DNL Blob]存储中的数据所需的SAS URI。 [!DNL Blob] SAS URI模式为：`https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`。 |
| `connectionSpec.id` | [!DNL Blob]存储连接规范ID为：`4c10e202-c428-4796-9208-5f1f5732b1cf` |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览您的存储需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 后续步骤

通过本教程，您已使用API创建了[!DNL Blob]连接，并且作为响应主体的一部分获得了唯一ID。 您可以使用此连接ID来[使用流服务API](../../explore/cloud-storage.md)或[使用流服务API](../../cloud-storage-parquet.md)采集拼花存储。