---
title: 使用流服务API创建Google云存储基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Google Cloud Storage帐户。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Google Cloud Storage]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Google Cloud Storage]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到Google云存储帐户所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与您的[!DNL Google Cloud Storage]帐户连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 一个由61个字符组成的字母数字字符串，用于向Experience Platform验证您的[!DNL Google Cloud Storage]帐户。 |
| `secretAccessKey` | 用于向Experience Platform验证您的[!DNL Google Cloud Storage]帐户的40个字符Base-64编码字符串。 |
| `bucketName` | [!DNL Google Cloud Storage]存储段的名称。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| `folderPath` | 要提供访问权限的文件夹的路径。 |

有关这些值的更多信息，请参阅[Google Cloud Storage HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview)指南。 有关如何生成自己的访问密钥ID和访问密钥的步骤，请参阅[[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Google Cloud Storage]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

>[!TIP]
>
>在此步骤中，您还可以通过定义存储段名称和子文件夹的路径，指定您的帐户将有权访问的子文件夹。

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
| `auth.params.accessKeyId` | 与您的[!DNL Google Cloud Storage]帐户关联的访问密钥ID。 |
| `auth.params.secretAccessKey` | 与您的[!DNL Google Cloud Storage]帐户关联的访问密钥。 |
| `auth.params.bucketName` | [!DNL Google Cloud Storage]存储段的名称。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | [!DNL Google Cloud Storage]连接规范ID： `32e8f412-cdf7-464c-9885-78184cb113fd` |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 需要在下一个教程中探究您的云存储数据时使用此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

按照本教程，您已使用API创建了[!DNL Google Cloud Storage]连接，并获取了唯一ID作为响应正文的一部分。 您可以使用此连接ID以使用流服务API[&#128279;](../../explore/cloud-storage.md)来浏览云存储。
