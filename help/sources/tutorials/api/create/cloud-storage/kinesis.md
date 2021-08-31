---
keywords: Experience Platform；主页；热门主题；Kinesis;Kinesis;Amazon Kinesis;Amazon Kinesis
solution: Experience Platform
title: 使用流服务API创建Amazon Kinesis源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Amazon Kinesis源。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# 使用流服务API创建[!DNL Amazon Kinesis]源连接

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将[!DNL Amazon Kinesis]（以下称“[!DNL Kinesis]”）连接到Experience Platform的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功将[!DNL Kinesis]连接到平台。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Amazon Kinesis]帐户连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 访问密钥ID是用于向Platform验证[!DNL Kinesis]帐户的访问密钥对的一半。 |
| `secretKey` | 密钥访问密钥是用于向Platform验证[!DNL Kinesis]帐户的访问密钥对的另一半。 |
| `region` | [!DNL Kinesis]帐户的区域。 有关区域的更多信息，请参阅[向允许列表添加IP地址](../../../../ip-address-allow-list.md)指南。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Kinesis]连接规范ID为：`86043421-563b-46ec-8e6c-e23184711bf6`。 |

有关[!DNL Kinesis]访问密钥及其生成方法的更多信息，请参阅本[[!DNL AWS] 指南，其中介绍了如何管理IAM用户的访问密钥](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

创建源连接的第一步是验证[!DNL Kinesis]源并生成基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Kinesis]身份验证凭据时，向`/connections`端点发出POST请求。

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
| `auth.params.secretKey` | [!DNL Kinesis]帐户的密钥访问密钥。 |
| `auth.params.region` | [!DNL Kinesis]帐户的区域。 |
| `connectionSpec.id` | [!DNL Kinesis]连接规范ID:`86043421-563b-46ec-8e6c-e23184711bf6` |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 创建源连接 {#source}

源连接创建并管理从中摄取数据的外部源的连接。 源连接由数据源、数据格式和创建数据流所需的源连接ID等信息组成。 源连接实例特定于租户和IMS组织。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `baseConnectionId` | 在上一步中生成的[!DNL Kinesis]源的基本连接ID。 |
| `connectionSpec.id` | [!DNL Kinesis]的固定连接规范ID。 此ID为：`86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 要摄取的[!DNL Kinesis]数据的格式。 目前，唯一支持的数据格式是`json`。 |
| `params.stream` | 要从中提取记录的数据流的名称。 |
| `params.dataType` | 此参数定义正在摄取的数据的类型。 支持的数据类型包括：`raw`和`xdm`。 |
| `params.reset` | 此参数定义数据的读取方式。 使用`latest`开始从最新数据中读取数据，使用`earliest`开始从流中的第一个可用数据中读取数据。 |

**响应**

成功的响应会返回新创建源连接的唯一标识符(`id`)。 在下一个教程中，需要此ID才能创建数据流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Kinesis]源连接。 在下一个教程中，您可以使用此源连接ID来使用 [!DNL Flow Service] API](../../collect/streaming.md)创建流数据流。[
