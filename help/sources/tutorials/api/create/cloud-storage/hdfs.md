---
keywords: Experience Platform；主页；热门主题；ApacheHadoop分布式文件系统；Apachehadoop;hdfs;HDFS
solution: Experience Platform
title: 使用流服务API创建Apache HDFS基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将ApacheHadoop分布式文件系统连接到Adobe Experience Platform。
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Apache] HDFS基本连接

>[!NOTE]
>
>Apache HDFS连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Apache Hadoop Distributed File System]（以下称“[!DNL HDFS]”）创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL HDFS]。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | URL可以匿名定义连接到[!DNL HDFS]所需的身份验证参数。 有关如何获取此值的更多信息，请参阅[this [!DNL HDFS] document](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL AdWords]的连接规范ID是：`54e221aa-d342-4707-bcff-7a4bceef0001`。 |

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL HDFS]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL HDFS]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.url` | 用于以匿名方式定义连接到[!DNL HDFS]所需的身份验证参数的URL |
| `connectionSpec.id` | [!DNL HDFS]连接规范ID:`54e221aa-d342-4707-bcff-7a4bceef0001`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL HDFS]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何使用流量服务API](../../explore/cloud-storage.md)探索第三方云存储。[
