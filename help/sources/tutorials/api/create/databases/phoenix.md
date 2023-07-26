---
title: 使用流服务API创建Phoenix Base连接
description: 了解如何使用流服务API将Phoenix数据库连接到Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 创建 [!DNL Phoenix] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程提供了有关如何创建基本连接和连接 [!DNL Phoenix] Adobe Experience Platform帐户 [!DNL Flow Service] API。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Phoenix] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

您必须提供以下身份验证凭据才能连接 [!DNL Phoenix] 帐户到Experience Platform。

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Phoenix] 服务器。 |
| `username` | 用于访问的用户名 [!DNL Phoenix] 服务器。 |
| `password` | 对应于用户的密码。 |
| `port` | TCP端口 [!DNL Phoenix] 服务器使用来侦听客户端连接。 如果您要连接到 [!DNL Azure HDInsights]，然后将端口指定为443。 如果未提供此参数，则值默认为8765。 |
| `httpPath` | 与对应的部分URL [!DNL Phoenix] 服务器。 如果使用的话，指定/hbasephoenix0 [!DNL Azure] HDInsights群集。 |
| `enableSsl` | 布尔值。 指定是否使用SSL对到服务器的连接进行加密。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Phoenix] 为： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门的更多信息，请参阅 [凤凰城文件](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接，请向 `/connections` 端点，同时提供 [!DNL Phoenix] 请求正文中的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Phoenix]：

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
| `auth.params.host` | 的主机 [!DNL Phoenix] 服务器。 |
| `auth.params.username` | 与您的关联的用户名 [!DNL Phoenix] 连接。 |
| `auth.params.password` | 与您的关联的密码 [!DNL Phoenix] 连接。 |
| `auth.params.port` | 您的TCP端口 [!DNL Phoenix] 连接。 |
| `auth.params.httpPath` | 的部分http路径 [!DNL Phoenix] 连接。 |
| `auth.params.enableSsl` | 指定是否使用SSL加密到服务器的连接的布尔值。 |
| `connectionSpec.id` | 此 [!DNL Phoenix] 连接规范ID： `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Phoenix] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
