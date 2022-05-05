---
keywords: Experience Platform；主页；热门主题；凤凰；凤凰
solution: Experience Platform
title: 使用流服务API创建Phoenix基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API将Phoenix数据库连接到Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---

# 创建 [!DNL Phoenix] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Phoenix] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用 [!DNL Flow Service] 用于指导您完成连接 [!DNL Phoenix] 数据库到 [!DNL Experience Platform].

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Phoenix] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Phoenix]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Phoenix] 服务器。 |
| `username` | 用于访问的用户名 [!DNL Phoenix] 服务器。 |
| `password` | 与用户对应的密码。 |
| `port` | TCP端口 [!DNL Phoenix] 服务器使用侦听客户端连接。 如果您连接到 [!DNL Azure] HDInsights，指定端口为443。 |
| `httpPath` | 与 [!DNL Phoenix] 服务器。 如果使用 [!DNL Azure] HDInsights群。 |
| `enableSsl` | 布尔值。 指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Phoenix] 为： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门的更多信息，请参阅 [这份凤凰号文件](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Phoenix] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Phoenix]:

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
| `auth.params.username` | 与您的 [!DNL Phoenix] 连接。 |
| `auth.params.password` | 与 [!DNL Phoenix] 连接。 |
| `auth.params.port` | 您的TCP端口 [!DNL Phoenix] 连接。 |
| `auth.params.httpPath` | 您的部分http路径 [!DNL Phoenix] 连接。 |
| `auth.params.enableSsl` | 布尔值，用于指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | 的 [!DNL Phoenix] 连接规范ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Phoenix] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
