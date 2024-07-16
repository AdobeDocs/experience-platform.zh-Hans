---
title: 使用流服务API创建Amazon Redshift基本连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Amazon Redshift。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Amazon Redshift]基本连接

>[!IMPORTANT]
>
>[!DNL Amazon Redshift]源在源目录中可供已购买Real-time Customer Data Platform Ultimate的用户使用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Amazon Redshift]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Amazon Redshift]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Amazon Redshift]连接，您必须提供以下连接属性：

| **凭据** | **描述** |
| -------------- | --------------- |
| `server` | 与您的[!DNL Amazon Redshift]帐户关联的服务器。 |
| `port` | [!DNL Amazon Redshift]服务器用于侦听客户端连接的TCP端口。 |
| `username` | 与您的[!DNL Amazon Redshift]帐户关联的用户名。 |
| `password` | 与您的[!DNL Amazon Redshift]帐户关联的密码。 |
| `database` | 您正在访问的[!DNL Amazon Redshift]数据库。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Amazon Redshift]的连接规范ID为`3416976c-a9ca-4bba-901a-1f08f66978ff`。 |

有关入门的详细信息，请参阅此[[!DNL Amazon Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

>[!NOTE]
>
>[!DNL Redshift]的默认编码标准为Unicode。 无法更改此设置。

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL Amazon Redshift]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Amazon Redshift]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
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
| ------------- | --------------- |
| `auth.params.server` | 您的[!DNL Amazon Redshift]服务器。 |
| `auth.params.port` | [!DNL Amazon Redshift]服务器用于侦听客户端连接的TCP端口。 |
| `auth.params.database` | 与您的[!DNL Amazon Redshift]帐户关联的数据库。 |
| `auth.params.password` | 与您的[!DNL Amazon Redshift]帐户关联的密码。 |
| `auth.params.username` | 与您的[!DNL Amazon Redshift]帐户关联的用户名。 |
| `connectionSpec.id` | [!DNL Amazon Redshift]连接规范ID： `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**响应**

成功的响应返回新创建的连接，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Amazon Redshift]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将数据库数据引入平台](../../collect/database-nosql.md)
