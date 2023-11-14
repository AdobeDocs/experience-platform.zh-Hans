---
keywords: Experience Platform；主页；热门主题；IBM [!DNL IBM DB2]；IBM；ibm [!DNL IBM DB2]；[!DNL IBM DB2]；[!DNL IBM DB2]
solution: Experience Platform
title: 创建IBM [!DNL IBM DB2] 使用流服务API进行基本连接
type: Tutorial
description: 了解如何连接IBM [!DNL IBM DB2] 流服务API添加到Adobe Experience Platform。
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 4%

---

# 创建IBM [!DNL IBM DB2] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>IBM [!DNL IBM DB2] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL IBM DB2] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL IBM DB2] 使用 [!DNL Flow Service] API。

| 凭据 | 描述 |
| ---------- | ----------- |
| `server` | 的名称 [!DNL IBM DB2] 服务器。 您可以在用冒号分隔的服务器名称后面指定端口号。 例如：server：port。 |
| `database` | 的名称 [!DNL IBM DB2] 数据库。 |
| `username` | 用于连接到 [!DNL IBM DB2] 数据库。 |
| `password` | 您为用户名指定的用户帐户的密码。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 的连接规范ID [!DNL IBM DB2] 是 `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

有关入门的更多信息，请参阅 [此 [!DNL IBM DB2] 文档](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL IBM DB2] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL IBM DB2]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的关联的连接字符串 [!DNL IBM DB2] 帐户。 |
| `connectionSpec.id` | 此 [!DNL IBM DB2] 连接规范ID： `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL IBM DB2] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)

