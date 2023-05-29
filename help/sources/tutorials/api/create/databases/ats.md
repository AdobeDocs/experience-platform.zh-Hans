---
keywords: Experience Platform；主页；热门主题；[!DNL Azure Table Storage]；[!DNL Azure Table Storage]；Azure表存储
solution: Experience Platform
title: 使用流服务API创建Azure表存储基连接
type: Tutorial
description: 了解如何使用流服务API将Azure Table Storage连接到Adobe Experience Platform。
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# 创建 [!DNL Azure Table Storage] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Azure Table Storage] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Azure Table Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Azure Table Storage] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Azure Table Storage]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到的连接字符串 [!DNL Azure Table Storage] 实例。 的连接字符串模式 [!DNL Azure Table Storage] 为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL Azure Table Storage] 是 `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

有关获取连接字符串的更多信息，请参阅 [此 [!DNL Azure Table Storage] 文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Azure Table Storage] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Azure Table Storage]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 用于连接到的连接字符串 [!DNL Azure Table Storage] 实例。 的连接字符串模式 [!DNL Azure Table Storage] 为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | 此 [!DNL Azure Table Storage] 连接规范ID： `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**响应**

成功响应将返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中，需要此ID来浏览您的数据。

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Azure Table Storage] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
