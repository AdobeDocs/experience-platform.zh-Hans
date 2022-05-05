---
keywords: Experience Platform；主页；热门主题；IBM [!DNL IBM DB2];IBM;ibm [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: 创建IBM [!DNL IBM DB2] 使用流服务API的基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何连接IBM [!DNL IBM DB2] 到Adobe Experience Platform。
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 创建IBM [!DNL IBM DB2] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>IBM [!DNL IBM DB2] 连接器处于测试阶段。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL IBM DB2] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL IBM DB2] 使用 [!DNL Flow Service] API。

| 凭据 | 描述 |
| ---------- | ----------- |
| `server` | 的名称 [!DNL IBM DB2] 服务器。 您可以在服务器名称后面指定端口号，该名称以冒号分隔。 例如：server:port。 |
| `database` | 的名称 [!DNL IBM DB2] 数据库。 |
| `username` | 用于连接到的用户名 [!DNL IBM DB2] 数据库。 |
| `password` | 您为用户名指定的用户帐户的密码。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 的连接规范ID [!DNL IBM DB2] is `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

有关入门的更多信息，请参阅 [此 [!DNL IBM DB2] 文档](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL IBM DB2] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL IBM DB2]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.connectionString` | 与 [!DNL IBM DB2] 帐户。 |
| `connectionSpec.id` | 的 [!DNL IBM DB2] 连接规范ID: `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL IBM DB2] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)

