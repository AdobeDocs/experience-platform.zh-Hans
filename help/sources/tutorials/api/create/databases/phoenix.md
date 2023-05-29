---
keywords: Experience Platform；主页；热门主题；凤凰城；凤凰城
solution: Experience Platform
title: 使用流服务API创建Phoenix Base连接
type: Tutorial
description: 了解如何使用流服务API将Phoenix数据库连接到Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 创建 [!DNL Phoenix] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Phoenix] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

[!DNL Flow Service] 用于从Adobe Experience Platform中各种不同的来源收集客户数据并对其进行集中。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从此API进行连接。

本教程使用 [!DNL Flow Service] API引导您完成连接 [!DNL Phoenix] 数据库至 [!DNL Experience Platform].

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Phoenix] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Phoenix]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Phoenix] 服务器。 |
| `username` | 用于访问的用户名 [!DNL Phoenix] 服务器。 |
| `password` | 对应于用户的密码。 |
| `port` | TCP端口， [!DNL Phoenix] 服务器使用来侦听客户端连接。 如果您连接到 [!DNL Azure] HDInsights，将端口指定为443。 |
| `httpPath` | 与对应的部分URL [!DNL Phoenix] 服务器。 如果使用，请指定/hbasephoenix0 [!DNL Azure] HDInsights群集。 |
| `enableSsl` | 布尔值。 指定是否使用SSL加密到服务器的连接。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL Phoenix] 为： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门指南的更多信息，请参阅 [这份Phoenix文件](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Phoenix] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Phoenix]：

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

成功响应将返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中，需要此ID来浏览您的数据。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Phoenix] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
