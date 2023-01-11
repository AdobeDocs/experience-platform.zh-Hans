---
keywords: Experience Platform；主页；热门主题；Kinesis;Kinesis;Amazon Kinesis;Amazon Kinesis
solution: Experience Platform
title: 使用流服务API创建Amazon Kinesis源连接
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Amazon Kinesis源。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# 创建 [!DNL Amazon Kinesis] 源连接（使用流量服务API）

本教程将指导您完成连接的步骤 [!DNL Amazon Kinesis] (以下简称“[!DNL Kinesis]&quot;)Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可分隔单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接所需了解的其他信息 [!DNL Kinesis] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 与 [!DNL Amazon Kinesis] 帐户，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 访问密钥ID是用于验证您的 [!DNL Kinesis] 帐户到平台。 |
| `secretKey` | 密钥访问密钥是用于验证您的 [!DNL Kinesis] 帐户到平台。 |
| `region` | 您的 [!DNL Kinesis] 帐户。 请参阅 [向允许列表添加IP地址](../../../../ip-address-allow-list.md) 以了解有关区域的更多信息。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的 [!DNL Kinesis] 连接规范ID是： `86043421-563b-46ec-8e6c-e23184711bf6`. |

有关 [!DNL Kinesis] 访问密钥及其生成方法，请参阅此 [[!DNL AWS] 管理IAM用户访问密钥指南](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

创建源连接的第一步是验证您的 [!DNL Kinesis] 源并生成基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Kinesis] 身份验证凭据作为请求参数的一部分。

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
| `auth.params.accessKeyId` | 您的 [!DNL Kinesis] 帐户。 |
| `auth.params.secretKey` | 您的 [!DNL Kinesis] 帐户。 |
| `auth.params.region` | 您的 [!DNL Kinesis] 帐户。 |
| `connectionSpec.id` | 的 [!DNL Kinesis] 连接规范ID: `86043421-563b-46ec-8e6c-e23184711bf6` |

**响应**

成功的响应会返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接 {#source}

源连接创建并管理从中摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和IMS组织。

要创建源连接，请向 `/sourceConnections` 的端点 [!DNL Flow Service] API。

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
| `name` | 源连接的名称。 确保源连接的名称具有描述性，因为您可以使用该名称查找有关源连接的信息。 |
| `description` | 可提供的可选值，用于包含有关源连接的更多信息。 |
| `baseConnectionId` | 您的基本连接ID [!DNL Kinesis] 上一步中生成的源。 |
| `connectionSpec.id` | 的固定连接规范ID [!DNL Kinesis]. 此ID为： `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 的格式 [!DNL Kinesis] 要摄取的数据。 目前，唯一支持的数据格式是 `json`. |
| `params.stream` | 要从中提取记录的数据流的名称。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括： `raw` 和 `xdm`. |
| `params.reset` | 此参数定义数据的读取方式。 使用 `latest` 以开始从最新数据中读取，并使用 `earliest` 从流中的第一个可用数据开始读取。 |

**响应**

成功的响应会返回唯一标识符(`id`)。 在下一个教程中，需要此ID才能创建数据流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Kinesis] 源连接使用 [!DNL Flow Service] API。 在下一个教程中，您可以使用此源连接ID [使用创建流数据流 [!DNL Flow Service] API](../../collect/streaming.md).
