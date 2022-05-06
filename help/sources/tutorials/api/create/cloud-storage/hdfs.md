---
keywords: Experience Platform；主页；热门主题；ApacheHadoop分布式文件系统；Apachehadoop;hdfs;HDFS
solution: Experience Platform
title: 使用流服务API创建Apache HDFS基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将ApacheHadoop分布式文件系统连接到Adobe Experience Platform。
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# 创建 [!DNL Apache] HDFS基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>Apache HDFS连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Apache Hadoop Distributed File System] (以下简称“[!DNL HDFS]“)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL HDFS] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | URL定义连接到所需的身份验证参数 [!DNL HDFS] 匿名。 有关如何获取此值的更多信息，请参阅 [此 [!DNL HDFS] 文档](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL AdWords] 为： `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL HDFS] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL HDFS]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.url` | 用于定义连接到所需的身份验证参数的URL [!DNL HDFS] 匿名 |
| `connectionSpec.id` | 的 [!DNL HDFS] 连接规范ID: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL HDFS] 使用 [!DNL Flow Service] API，并已获取连接的唯一ID值。 在下一个教程中，您可以使用此ID来了解如何 [使用流量服务API探索第三方云存储](../../explore/cloud-storage.md).
