---
keywords: Experience Platform；主页；热门主题；Apache Hive；Hive；Hive
solution: Experience Platform
title: 使用流服务API在Azure HDInsights基本连接上创建Apache Hive
type: Tutorial
description: 了解如何使用流服务API将Azure HDInsights上的Apache Hive连接到Adobe Experience Platform。
exl-id: e1469a29-6f61-47ba-995e-39f06ee4a4a4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# 创建 [!DNL Apache Hive] 日期 [!DNL Azure HDInsights] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Apache Hive] 日期 [!DNL Azure HDInsights] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Apache Hive] 日期 [!DNL Azure HDInsights] (以下简称“ ”[!DNL Hive]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Hive] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Hive]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Hive] 服务器。 |
| `username` | 用于访问的用户名 [!DNL Hive] 服务器。 |
| `password` | 对应于用户的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL Hive] 为： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

有关入门指南的更多信息，请参阅 [此Hive文档](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Hive] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Hive]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的关联的连接字符串 [!DNL Hive] 帐户。 |
| `connectionSpec.id` | 此 [!DNL Hive] 连接规范ID： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`. |

**响应**

成功响应将返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中，需要此ID来浏览您的数据。

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Apache Hive] 日期 [!DNL Azure HDInsights] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
