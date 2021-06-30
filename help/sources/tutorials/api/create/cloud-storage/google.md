---
keywords: Experience Platform；主页；热门主题；Google云存储；Google云存储；Google
solution: Experience Platform
title: 使用流服务API创建Google云存储基础连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google云存储帐户。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Google Cloud Storage]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Google Cloud Storage]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到Google云存储帐户。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Google Cloud Storage]帐户连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 由61个字符组成的字母数字字符串，用于向Platform验证[!DNL Google Cloud Storage]帐户。 |
| `secretAccessKey` | 一个40个字符、基于64编码的字符串，用于向Platform验证[!DNL Google Cloud Storage]帐户。 |

有关这些值的更多信息，请参阅[Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有关如何生成您自己的访问密钥ID和密钥访问密钥的步骤，请参阅[[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Google Cloud Storage]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL Google Cloud Storage]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 与您的[!DNL Google Cloud Storage]帐户关联的访问密钥ID。 |
| `auth.params.secretAccessKey` | 与您的[!DNL Google Cloud Storage]帐户关联的密钥访问密钥。 |
| `connectionSpec.id` | [!DNL Google Cloud Storage]连接规范ID:`32e8f412-cdf7-464c-9885-78184cb113fd` |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

在本教程中，您已使用API创建了[!DNL Google Cloud Storage]连接，并且获取了作为响应主体一部分的唯一ID。 您可以使用此连接ID来[使用流量服务API](../../explore/cloud-storage.md)或[使用流量服务API](../../cloud-storage-parquet.md)摄取Parquet数据来浏览云存储。
