---
keywords: Experience Platform；主页；热门主题；凤凰；凤凰
solution: Experience Platform
title: 使用流服务API创建Phoenix基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API将Phoenix数据库连接到Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Phoenix]基本连接

>[!NOTE]
>
>[!DNL Phoenix]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Phoenix]数据库连接到[!DNL Experience Platform]的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL Phoenix]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Phoenix]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Phoenix]服务器的IP地址或主机名。 |
| `username` | 用于访问[!DNL Phoenix]服务器的用户名。 |
| `password` | 与用户对应的密码。 |
| `port` | [!DNL Phoenix]服务器用于侦听客户端连接的TCP端口。 如果连接到[!DNL Azure] HDInsights，请将端口指定为443。 |
| `httpPath` | 与[!DNL Phoenix]服务器对应的部分URL。 如果使用[!DNL Azure] HDInsights群集，请指定/hbasephoenix0。 |
| `enableSsl` | 布尔值。 指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Phoenix]的连接规范ID是：`102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门的详细信息，请参阅[此Phoenix文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Phoenix]身份验证凭据时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
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
| `auth.params.username` | 与[!DNL Phoenix]连接关联的用户名。 |
| `auth.params.password` | 与[!DNL Phoenix]连接关联的密码。 |
| `auth.params.port` | [!DNL Phoenix]连接的TCP端口。 |
| `auth.params.httpPath` | [!DNL Phoenix]连接的部分http路径。 |
| `auth.params.enableSsl` | 布尔值，用于指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | [!DNL Phoenix]连接规范ID:`102706fb-a5cd-42ee-afe0-bc42f017ff43`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Phoenix]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/database-nosql.md)浏览数据库。
