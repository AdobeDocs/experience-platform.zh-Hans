---
keywords: Experience Platform；主页；热门主题；Azure数据湖存储Gen2;Azure数据湖存储；Azure
solution: Experience Platform
title: 使用流服务API创建Azure Data Lake Storage Gen2基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Azure Data Lake Storage Gen2。
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# 创建 [!DNL Azure Data Lake Storage Gen2] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Azure Data Lake Storage Gen2] （以下简称ADLS Gen2） [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 要连接到ADLS Gen2，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端点。 端点模式为： `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 ADLS Gen2的连接规范ID是： `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

有关这些值的更多信息，请参阅 [此ADLS第2代文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 端点，同时将您的ADLS Gen2身份验证凭据作为请求参数的一部分提供。

**API格式**

```http
POST /connections
```

**请求**

以下请求为ADLS Gen2创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.url` | 您的ADLS Gen2帐户的URL端点。 |
| `auth.params.servicePrincipalId` | 您的ADLS Gen2帐户的服务主体ID。 |
| `auth.params.servicePrincipalKey` | 您的ADLS Gen2帐户的服务主密钥。 |
| `auth.params.tenant` | 您的ADLS Gen2帐户的租户信息。 |
| `connectionSpec.id` | ADLS Gen2连接规范ID: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## 后续步骤

通过阅读本教程，您已使用API创建了ADLS Gen2连接，并且获取了作为响应主体一部分的唯一ID。 您可以将此连接ID用于 [使用流量服务API浏览云存储](../../explore/cloud-storage.md).
