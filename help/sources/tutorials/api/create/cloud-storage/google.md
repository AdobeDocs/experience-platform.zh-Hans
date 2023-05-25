---
title: 使用流服务API创建Google Cloud Storage基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google Cloud Storage帐户。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 创建 [!DNL Google Cloud Storage] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Google Cloud Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用成功连接到Google云存储帐户 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以与您的 [!DNL Google Cloud Storage] 帐户，则必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 61个字符的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。 |
| `secretAccessKey` | 40个字符的base-64编码字符串，用于验证您的 [!DNL Google Cloud Storage] Platform帐户。 |
| `bucketName` | 您的名称 [!DNL Google Cloud Storage] 桶。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| `folderPath` | 要提供访问权限的文件夹的路径。 |

有关这些值的更多信息，请参见 [Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有关如何生成您自己的访问密钥ID和秘密访问密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Google Cloud Storage] 作为请求参数一部分的身份验证凭据。

>[!TIP]
>
>在此步骤中，您还可以通过定义存储段名称和子文件夹的路径，指定您的帐户将有权访问的子文件夹。

**API格式**

```http
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Google Cloud Storage]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
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
| `auth.params.accessKeyId` | 与您的关联的访问密钥ID [!DNL Google Cloud Storage] 帐户。 |
| `auth.params.secretAccessKey` | 与您的关联的访问密钥 [!DNL Google Cloud Storage] 帐户。 |
| `auth.params.bucketName` | 您的名称 [!DNL Google Cloud Storage] 桶。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | 此 [!DNL Google Cloud Storage] 连接规范ID： `32e8f412-cdf7-464c-9885-78184cb113fd` |

**响应**

成功响应将返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中，需要此ID来浏览您的云存储数据。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Google Cloud Storage] 连接使用API，并且获取了一个唯一ID作为响应正文的一部分。 您可以使用此连接ID来 [使用流服务API浏览云存储](../../explore/cloud-storage.md).
