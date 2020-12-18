---
keywords: Experience Platform;home;popular topics;Apache Spark;apache spark;Azure HDInsights
solution: Experience Platform
title: 在Azure HDInsights连接器上使用Flow Service API创建Apache Spark
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Azure HDInsights上的Apache Spark（以下简称“Spark”）连接到Experience Platform的步骤。
translation-type: tm+mt
source-git-commit: 36620a229fc8e6e3fa4545bfc775a49bc89935bb
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API在[!DNL Azure] HDInsights连接器上创建[!DNL Apache Spark]

>[!NOTE]
>
>[!DNL Azure HDInsights]连接器上的[!DNL Apache Spark]为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Azure HDInsights]（下称“[!DNL Spark]”）上的[!DNL Apache Spark]连接到[!DNL Experience Platform]的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到[!DNL Spark]时需要了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Spark]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Spark]服务器的IP地址或主机名。 |
| `username` | 用于访问[!DNL Spark]服务器的用户名。 |
| `password` | 与用户对应的口令。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 [!DNL Spark]的连接规范ID为：`6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

有关入门的详细信息，请参阅[此Spark文档](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)疑难解答指南中关于如何阅读示例API调用[的一节。[!DNL Experience Platform]

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL Spark]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建[!DNL Spark]连接，其唯一连接规范ID必须作为POST请求的一部分提供。 [!DNL Spark]的连接规范ID为`6a8d82bc-1caf-45d1-908d-cadabc9d63a6`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}"
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
| `auth.params.host` | [!DNL Spark]服务器的主机。 |
| `auth.params.username` | 与[!DNL Spark]连接关联的用户名。 |
| `auth.params.password` | 与[!DNL Spark]连接关联的密码。 |
| `connectionSpec.id` | [!DNL Spark]连接规范ID:`6a8d82bc-1caf-45d1-908d-cadabc9d63a6`。 |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 后续步骤

按照本教程，您已使用[!DNL Flow Service] API创建了[!DNL Spark]连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/database-nosql.md)浏览数据库。