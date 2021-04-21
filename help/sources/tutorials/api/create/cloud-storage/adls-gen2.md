---
keywords: Experience Platform；主页；热门主题；Azure数据湖存储Gen2;azure数据湖存储;Azure
solution: Experience Platform
title: 使用流服务API创建Azure Data Lake 存储 Gen2源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Azure Data Lake 存储 Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Azure] Data Lake 存储 Gen2源连接

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL Azure] Data Lake 存储 Gen2（以下称“ADLS Gen2”）的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个平台实例分区为单独的虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便使用[!DNL Flow Service] API成功创建ADLS Gen2源连接。

### 收集所需凭据

要使[!DNL Flow Service]连接到ADLS Gen2，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | 地址URL。 |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |

有关这些值的详细信息，请参阅[此ADLS Gen2文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

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

连接指定源并包含该源的凭据。 每个ADLS Gen2帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建ADLS-Gen2连接，必须在POST请求中提供其唯一连接规范ID。 ADLS-Gen2的连接规范ID为`0ed90a81-07f4-4586-8190-b40eccef1c5a`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.url` | 您的ADLS Gen2帐户的URL端点。 |
| `auth.params.servicePrincipalId` | 您的ADLS Gen2帐户的服务主体ID。 |
| `auth.params.servicePrincipalKey` | 您的ADLS Gen2帐户的服务主体密钥。 |
| `auth.params.tenant` | ADLS Gen2帐户的租户信息。 |
| `connectionSpec.id` | ADLS Gen2连接规范ID:`0ed90a81-07f4-4586-8190-b40eccef1c5a1`。 |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 需要此ID才能在下一步中浏览您的云存储。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 后续步骤

通过本教程，您已使用API创建了ADLS Gen2连接，并获取了作为响应主体一部分的唯一ID。 您可以使用此连接ID来使用流服务API](../../explore/cloud-storage.md)或[使用流服务API](../../cloud-storage-parquet.md)收录Parke存储来浏览云数据。[
