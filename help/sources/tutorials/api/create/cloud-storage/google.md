---
keywords: Experience Platform；主页；热门主题；Google Cloud存储;google Cloud存储;google;Google
solution: Experience Platform
title: 使用流服务API创建Google Cloud存储源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Google Cloud存储帐户。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL Google Cloud Storage]源连接

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL Google Cloud Storage]帐户的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用[!DNL Flow Service] API成功连接到Google Cloud存储帐户。

### 收集所需凭据

要使[!DNL Flow Service]与您的[!DNL Google Cloud Storage]帐户连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| 访问密钥ID | 一个61个字符的字母数字字符串，用于向平台验证您的[!DNL Google Cloud Storage]帐户。 |
| 密钥访问密钥 | 一个40个字符、基本64编码的字符串，用于向平台验证您的[!DNL Google Cloud Storage]帐户。 |

有关这些值的详细信息，请参阅[Google Cloud 存储 HMAC键](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有关如何生成您自己的访问密钥ID和密钥访问密钥的步骤，请参阅[[!DNL Google Cloud Storage] overview](../../../../connectors/cloud-storage/google-cloud-storage.md)。

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

连接指定源并包含该源的凭据。 每个[!DNL Google Cloud Storage]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL Google Cloud Storage]连接，必须在POST请求中提供其唯一连接规范ID。 [!DNL Google Cloud Storage]的连接规范ID为`32e8f412-cdf7-464c-9885-78184cb113fd`。

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
| `auth.params.secretAccessKey` | 与[!DNL Google Cloud Storage]帐户关联的秘密访问密钥。 |
| `connectionSpec.id` | [!DNL Google Cloud Storage]连接规范ID:`32e8f412-cdf7-464c-9885-78184cb113fd` |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览您的云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过本教程，您已使用API创建了[!DNL Google Cloud Storage]连接，并获取了作为响应体一部分的唯一ID。 您可以使用此连接ID来使用流服务API](../../explore/cloud-storage.md)或[使用流服务API](../../cloud-storage-parquet.md)收录Parke存储来浏览云数据。[
