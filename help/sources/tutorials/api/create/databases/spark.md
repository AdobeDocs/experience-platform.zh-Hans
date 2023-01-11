---
keywords: Experience Platform；主页；热门主题；Apache Spark;Apache Spark;Azure HDInsights
solution: Experience Platform
title: 在Azure HDInsights Base连接上使用流量服务API创建Apache Spark
type: Tutorial
description: 了解如何使用流量服务API将Azure HDInsights上的Apache Spark连接到Adobe Experience Platform。
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 创建 [!DNL Apache Spark] on [!DNL Azure] HDInsights基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Apache Spark] on [!DNL Azure HDInsights] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Apache Spark] on [!DNL Azure HDInsights] (以下简称“[!DNL Spark]“)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Spark] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Spark]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Spark] 服务器。 |
| `username` | 用于访问的用户名 [!DNL Spark] 服务器。 |
| `password` | 与用户对应的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Spark] 为： `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

有关入门的更多信息，请参阅 [这个Spark文档](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Spark] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Spark]:


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
| `auth.params.username` | 与您的 [!DNL Spark] 连接。 |
| `auth.params.password` | 与 [!DNL Spark] 连接。 |
| `connectionSpec.id` | 的 [!DNL Spark] 连接规范ID: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Spark] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
