---
title: 使用流服务API创建Phoenix Base连接
description: 了解如何使用流服务API将Phoenix数据库连接到Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Phoenix]基本连接

>[!WARNING]
>
>[!DNL Phoenix]源将于2025年6月底弃用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程提供了有关如何创建基本连接以及如何使用[!DNL Flow Service] API将您的[!DNL Phoenix]帐户连接到Adobe Experience Platform的步骤。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Phoenix]所需了解的其他信息。

### 收集所需的凭据

您必须提供以下身份验证凭据，才能将您的[!DNL Phoenix]帐户连接到Experience Platform。

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Phoenix]服务器的IP地址或主机名。 |
| `username` | 用于访问[!DNL Phoenix]服务器的用户名。 |
| `password` | 对应于用户的密码。 |
| `port` | [!DNL Phoenix]服务器用于侦听客户端连接的TCP端口。 如果您要连接到[!DNL Azure HDInsights]，则将端口指定为443。 如果未提供此参数，则值默认为8765。 |
| `httpPath` | 与[!DNL Phoenix]服务器对应的部分URL。 如果使用[!DNL Azure] HDInsights群集，请指定/hbasephoenix0。 |
| `enableSsl` | 布尔值。 指定是否使用SSL对到服务器的连接进行加密。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Phoenix]的连接规范ID为： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门的详细信息，请参阅[此Phoenix文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接，请在请求正文中提供您的[!DNL Phoenix]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Phoenix]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Phoenix]服务器的主机。 |
| `auth.params.username` | 与您的[!DNL Phoenix]连接关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Phoenix]连接关联的密码。 |
| `auth.params.port` | [!DNL Phoenix]连接的TCP端口。 |
| `auth.params.httpPath` | [!DNL Phoenix]连接的部分http路径。 |
| `auth.params.enableSsl` | 指定是否使用SSL加密到服务器的连接的布尔值。 |
| `connectionSpec.id` | [!DNL Phoenix]连接规范ID： `102706fb-a5cd-42ee-afe0-bc42f017ff43`。 |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Phoenix]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)
