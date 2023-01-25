---
title: 使用流服务API创建Google云存储基础连接
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google云存储帐户。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 创建 [!DNL Google Cloud Storage] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Google Cloud Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了要使用成功连接到Google云存储帐户所需了解的其他信息 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 与 [!DNL Google Cloud Storage] 帐户，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 由61个字符组成的字母数字字符串，用于验证您的 [!DNL Google Cloud Storage] 帐户到平台。 |
| `secretAccessKey` | 一个40个字符、基于64编码的字符串，用于验证您的 [!DNL Google Cloud Storage] 帐户到平台。 |
| `bucketName` | 您的 [!DNL Google Cloud Storage] 存储段。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| `folderPath` | 要提供访问权限的文件夹的路径。 |

有关这些值的更多信息，请参阅 [Google云存储HMAC密钥](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的双曲余切值。 有关如何生成您自己的访问密钥ID和密钥的步骤，请参阅 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Google Cloud Storage] 身份验证凭据作为请求参数的一部分。

>[!TIP]
>
>在此步骤中，您还可以通过定义存储段名称和子文件夹的路径，指定您的帐户将有权访问的子文件夹。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Google Cloud Storage]:

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
| `auth.params.accessKeyId` | 与 [!DNL Google Cloud Storage] 帐户。 |
| `auth.params.secretAccessKey` | 与 [!DNL Google Cloud Storage] 帐户。 |
| `auth.params.bucketName` | 您的 [!DNL Google Cloud Storage] 存储段。 如果要提供对云存储中特定子文件夹的访问权限，则必须指定存储段名称。 |
| `auth.params.folderPath` | 要提供访问权限的文件夹的路径。 |
| `connectionSpec.id` | 的 [!DNL Google Cloud Storage] 连接规范ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Google Cloud Storage] 使用API进行连接，并在响应主体中获取唯一ID。 您可以将此连接ID用于 [使用流量服务API浏览云存储](../../explore/cloud-storage.md).
