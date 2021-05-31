---
keywords: Experience Platform；主页；热门主题；Vertica;Vertica
solution: Experience Platform
title: 使用流服务API创建HP Vertica源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API将HP Vertica连接到Adobe Experience Platform。
exl-id: 37f831c1-7c82-462a-8338-a0bcaaf08cd1
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建HP [!DNL Vertica]源连接

>[!NOTE]
>
>HP [!DNL Vertica]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将HP [!DNL Vertica]连接到[!DNL Experience Platform]的步骤。

## 入门指南

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](https://experienceleague.adobe.com/docs/experience-platform/source-connectors/home.html): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、映射和增强传入数 [!DNL Platform] 据。
* [沙盒](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到HP [!DNL Vertica]。

### 收集所需的凭据

要使[!DNL Flow Service]与HP [!DNL Vertica]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到HP [!DNL Vertica]实例的连接字符串。 HP [!DNL Vertica]的连接字符串模式为`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | 创建连接所需的标识符。 HP [!DNL Vertica]的固定连接规范ID是：`a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

有关获取连接字符串的详细信息，请参见[此HP Vertica文档](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个HP [!DNL Vertica]帐户只需要一个连接，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建HP [!DNL Vertica]连接，必须在POST请求中提供其唯一连接规范ID。 HP [!DNL Vertica]的连接规范ID为`a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的HP [!DNL Vertica]帐户关联的连接字符串。 HP [!DNL Vertica]的连接字符串模式为：`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | HP [!DNL Vertica]连接规范ID:`a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了HP [!DNL Vertica]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/database-nosql.md)浏览数据库。
