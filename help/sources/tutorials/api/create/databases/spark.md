---
keywords: Experience Platform；主页；热门主题；Apache Spark；Apache Spark；Azure HDInsights
solution: Experience Platform
title: 使用流服务API在Azure HDInsights基本连接上创建Apache Spark
type: Tutorial
description: 了解如何使用流服务API将Azure HDInsights上的Apache Spark连接到Adobe Experience Platform。
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 4%

---

# 创建 [!DNL Apache Spark] 日期 [!DNL Azure] HDInsights基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Apache Spark] 日期 [!DNL Azure HDInsights] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Apache Spark] 日期 [!DNL Azure HDInsights] (以下简称“[!DNL Spark]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Spark] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Spark]中，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Spark] 服务器。 |
| `username` | 用于访问的用户名 [!DNL Spark] 服务器。 |
| `password` | 对应于用户的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Spark] 为： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

有关入门的更多信息，请参阅 [此Spark文档](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Spark] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Spark]：


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的主机 [!DNL Spark] 服务器。 |
| `auth.params.username` | 与您的关联的用户名 [!DNL Spark] 连接。 |
| `auth.params.password` | 与您的关联的密码 [!DNL Spark] 连接。 |
| `connectionSpec.id` | 此 [!DNL Spark] 连接规范ID： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Spark] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
