---
title: 使用流服务API创建Amazon Kinesis Source连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Amazon Kinesis源。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 3%

---

# 使用流服务API创建[!DNL Amazon Kinesis]源连接

>[!IMPORTANT]
>
>[!DNL Amazon Kinesis]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

本教程将指导您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[!DNL Amazon Kinesis]（以下称为“[!DNL Kinesis]”）连接到Experience Platform的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功将[!DNL Kinesis]连接到Experience Platform所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与您的[!DNL Amazon Kinesis]帐户连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 访问密钥ID是用于向Experience Platform验证您的[!DNL Kinesis]帐户的访问密钥对的一半。 |
| `secretKey` | 访问密钥是访问密钥对的另一半，用于向Experience Platform验证您的[!DNL Kinesis]帐户。 |
| `region` | [!DNL Kinesis]帐户的地区。 有关地区的详细信息，请参阅[将IP地址添加到允许列表](../../../../ip-address-allow-list.md)指南。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Kinesis]连接规范ID为： `86043421-563b-46ec-8e6c-e23184711bf6`。 |

有关[!DNL Kinesis]访问密钥以及如何生成它们的详细信息，请参阅此[[!DNL AWS] 有关管理IAM用户的访问密钥的指南](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

创建源连接的第一步是验证您的[!DNL Kinesis]源并生成基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并识别要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Kinesis]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
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
| `auth.params.accessKeyId` | [!DNL Kinesis]帐户的访问密钥ID。 |
| `auth.params.secretKey` | [!DNL Kinesis]帐户的访问密钥。 |
| `auth.params.region` | [!DNL Kinesis]帐户的地区。 |
| `connectionSpec.id` | [!DNL Kinesis]连接规范ID： `86043421-563b-46ec-8e6c-e23184711bf6` |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步创建源连接时需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接 {#source}

源连接创建和管理与摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和组织。

要创建源连接，请向[!DNL Flow Service] API的`/sourceConnections`端点发出POST请求。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 在上一步中生成的[!DNL Kinesis]源的基本连接ID。 |
| `connectionSpec.id` | [!DNL Kinesis]的固定连接规范ID。 此ID为： `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 要摄取的[!DNL Kinesis]数据的格式。 当前，唯一支持的数据格式为`json`。 |
| `params.stream` | 要从中提取记录的数据流的名称。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw`和`xdm`。 |
| `params.reset` | 此参数定义数据的读取方式。 使用`latest`开始读取最新数据，并使用`earliest`开始读取流中的第一个可用数据。 |

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 在下一个教程中，创建数据流时需要此ID。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>创建或更新流数据流后，需要短暂暂停数据摄取5分钟，以防出现任何潜在的数据丢失或数据丢失情况。

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API创建了[!DNL Kinesis]源连接。 您可以在下一个教程中使用此源连接ID来[使用 [!DNL Flow Service] API](../../collect/streaming.md)创建流式数据流。
