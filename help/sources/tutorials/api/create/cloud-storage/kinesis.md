---
keywords: Experience Platform;home;popular topics;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: 使用Flow Service API创建AmazonKinesis连接器
topic: overview
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到AmazonKinesis帐户的步骤。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 2%

---


# 使用 [!DNL Amazon Kinesis] Flow Service API创建连接器

>[!NOTE]
>
>连接 [!DNL Amazon Kineses] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接帐户 [!DNL Experience Platform] 的步 [!DNL Amazon Kinesis] 骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成 [!DNL Amazon Kinesis] 功连接到帐 [!DNL Flow Service] 户。

### 收集所需的凭据

要与您 [!DNL Flow Service] 的帐户连接， [!DNL Amazon Kinesis] 您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 您的帐户的访问密钥 [!DNL Kinesis] ID。 |
| `secretKey` | 帐户的秘密访问 [!DNL Kinesis] 密钥。 |
| `region` |  | 您帐户的 [!DNL Kinesis] 地区。 |
| `connectionSpec.id` | 连接 [!DNL Kinesis] 规范ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

有关这些值的详细信息，请参 [阅本Kinesis文档](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Flow Service]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个帐户只需要一 [!DNL Amazon Kinesis] 个连接，因为它可用于创建多个源连接器以导入不同的数据。

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "auth": {
            "specName": "Basic Authentication for Kinesis",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretKey": "secretKey"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 您的帐户的访问密钥 [!DNL Kinesis] ID。 |
| `auth.params.secretKey` | 帐户的秘密访问 [!DNL Kinesis] 密钥。 |
| `auth.params.region` | 您帐户的 [!DNL Kinesis] 地区。 |
| `connectionSpec.id` | 连接 [!DNL Kinesis] 规范ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览您的云存储数据时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

通过本教程，您已使用API [!DNL Amazon Kinesis] 创建了连接，并且作为响应主体的一部分获得了唯一ID。 您可以使用此连接ID [来使用流服务API浏览云存储](../../explore/cloud-storage.md)。