---
title: 使用流服务API将AWS Redshift连接到Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到AWS Redshift。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API将[!DNL AWS Redshift]连接到Experience Platform

>[!IMPORTANT]
>
>[!DNL AWS Redshift]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL AWS Redshift]源帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 将[!DNL AWS Redshift]连接到Azure上的Experience Platform {#azure}

有关如何将[!DNL AWS Redshift]源连接到Azure上的Experience Platform的信息，请阅读以下步骤。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL AWS Redshift]连接，您必须提供以下连接属性：

| 凭据 | 描述 |
| `server` | [!DNL AWS Redshift]实例的服务器名称。 |
| `port` | [!DNL AWS Redshift]服务器用于侦听客户端连接的TCP端口。 |
| `username` | 与您的[!DNL AWS Redshift]帐户关联的用户名。 |
| `password` | 与用户帐户对应的密码。 |
| `database` | 从中提取数据的[!DNL AWS Redshift]数据库。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL AWS Redshift]的连接规范ID为`3416976c-a9ca-4bba-901a-1f08f66978ff`。 |

有关入门的详细信息，请参阅此[[!DNL AWS Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)。

### 在Azure [#azure-base]上的Experience Platform上为[!DNL AWS Redshift]创建基础连接

>[!NOTE]
>
>[!DNL Redshift]的默认编码标准为Unicode。 无法更改此设置。

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL AWS Redshift]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

+++选择以查看示例

以下请求为[!DNL AWS Redshift]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS-redshift base connection",
      "description": "base connection for AWS-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL AWS Redshift]实例的服务器名称。 |
| `auth.params.port` | [!DNL AWS Redshift]服务器用于侦听客户端连接的TCP端口。 |
| `auth.params.username` | 与您的[!DNL AWS Redshift]帐户关联的用户名。 |
| `auth.params.password` | 与用户帐户对应的密码。 |
| `auth.params.database` | 从中获取数据的[!DNL AWS Redshift]数据库。 |
| `connectionSpec.id` | [!DNL AWS Redshift]连接规范ID： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**响应**

+++选择以查看示例

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

+++

## 将[!DNL AWS Redshift]连接到AWS Web服务(AWS)上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在AWS Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将[!DNL AWS Redshift]源连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 在AWS上的Experience Platform上为[!DNL AWS Redshift]创建基本连接 {#aws-base}

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL AWS Redshift]创建基本连接：

+++选择以查看示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "AWS Redshift base connection for Experience Platform on AWS",
      "description": "AWS Redshift base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "5439",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL AWS Redshift]实例的服务器名称。 |
| `auth.params.port` | [!DNL AWS Redshift]服务器用于侦听客户端连接的TCP端口。 |
| `auth.params.username` | 与您的[!DNL AWS Redshift]帐户关联的用户名。 |
| `auth.params.password` | 与用户帐户对应的密码。 |
| `auth.params.database` | 从中获取数据的[!DNL AWS Redshift]数据库。 |
| `auth.params.schema` | 与您的[!DNL AWS Redshift]数据库关联的架构的名称。 您必须确保要为其授予数据库访问权限的用户也具有此架构的访问权限。 |
| `connectionSpec.id` | [!DNL AWS Redshift]连接规范ID： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

+++

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中，需要此ID来浏览您的存储。

+++选择以查看示例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++


## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL AWS Redshift]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)
