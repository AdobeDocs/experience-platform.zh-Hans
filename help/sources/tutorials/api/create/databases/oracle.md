---
title: 使用流服务API将Oracle DB连接到Experience Platform
description: 了解如何使用API将Oracle DB连接到Experience Platform。
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---

# 使用[!DNL Oracle DB] API将[!DNL Flow Service]连接到Experience Platform

阅读本指南，了解如何使用[!DNL Oracle DB]API[[!DNL Flow Service] 将您的](https://developer.adobe.com/experience-platform-apis/references/flow-service/)帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Oracle] API成功连接到[!DNL Flow Service]所需了解的其他信息。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Oracle DB] 概述](../../../../connectors/databases/oracle.md#prerequisites)。

## 将[!DNL Oracle DB]连接到Azure上的Experience Platform {#azure}

有关如何将您的[!DNL Oracle DB]帐户连接到Azure上的Experience Platform的信息，请阅读以下步骤。

### 在Azure上的Experience Platform上为[!DNL Oracle DB]创建基础连接 {#azure-base}

基本连接可将您的源链接到Experience Platform，以存储身份验证详细信息、连接状态和唯一ID。 使用此ID浏览源文件并标识要摄取的特定项目，包括其数据类型和格式。

**API格式**

```https
POST /connections
```

要创建基本连接ID，请向`/connections`端点发出POST请求，并在请求参数中提供[!DNL Oracle DB]身份验证凭据。

**请求**

以下请求使用连接字符串身份验证为[!DNL Oracle DB]创建基本连接。

+++查看请求


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 用于连接到[!DNL Oracle DB]的连接字符串。 [!DNL Oracle DB]连接字符串模式为： `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL Oracle]连接规范ID： `d6b52d86-f0f8-475f-89d4-ce54c8527328`。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看响应

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## 将[!DNL Oracle DB]连接到Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将您的[!DNL Oracle DB]帐户连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 在AWS上的Experience Platform上为[!DNL Oracle DB]创建基本连接 {#aws-base}

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Oracle DB]创建基本连接以连接到AWS上的Experience Platform。

+++查看请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL Oracle DB]服务器的IP地址或主机名。 |
| `auth.params.port` | [!DNL Oracle DB]服务器的端口号。 |
| `auth.params.database` | 要连接的[!DNL Oracle DB]实例的名称。 |
| `auth.params.username` | 与您的[!DNL Oracle DB]实例关联的用户帐户。 |
| `auth.prams.password` | 与您的[!DNL Oracle DB]用户帐户对应的密码。 |
| `auth.params.schema` | 包含数据库对象的方案。 |
| `auth.params.sslMode` | 一个布尔值，指示是否强制执行SSL度量。 |
| `connectionSpec.id` | 与[!DNL Oracle DB]源对应的连接规范ID。 此ID值固定为： `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)和相应的标识符。 你可以使用此ID [创建源连接](../../collect/database-nosql.md#create-a-source-connection)，并使用`etag`更新你的帐户[。](../../update.md)

+++查看响应

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## 为[!DNL Oracle DB]数据创建数据流

现在您已成功连接[!DNL Oracle DB]帐户，您现在可以[创建数据流并将数据库中的数据摄取到Experience Platform](../../collect/database-nosql.md)。