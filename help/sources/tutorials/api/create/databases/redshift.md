---
keywords: Experience Platform；主页；热门主题；Redshift;Redshift;Amazon Redshift;Amazon Redshift
solution: Experience Platform
title: 使用流服务API创建Amazon Redshift基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform与Amazon Redshift连接。
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 创建 [!DNL Amazon Redshift] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Amazon Redshift] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Amazon Redshift] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Amazon Redshift]，则必须提供以下连接属性：

| **凭据** | **描述** |
| -------------- | --------------- |
| `server` | 与 [!DNL Amazon Redshift] 帐户。 |
| `username` | 与您的 [!DNL Amazon Redshift] 帐户。 |
| `password` | 与 [!DNL Amazon Redshift] 帐户。 |
| `database` | 的 [!DNL Amazon Redshift] 您正在访问的数据库。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Amazon Redshift] is `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

有关入门的更多信息，请参阅此 [[!DNL Amazon Redshift] 文档](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

>[!NOTE]
>
>的默认编码标准 [!DNL Redshift] 为Unicode。 无法更改。

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Amazon Redshift] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.server` | 您的 [!DNL Amazon Redshift] 服务器。 |
| `auth.params.database` | 与 [!DNL Amazon Redshift] 帐户。 |
| `auth.params.password` | 与 [!DNL Amazon Redshift] 帐户。 |
| `auth.params.username` | 与您的 [!DNL Amazon Redshift] 帐户。 |
| `connectionSpec.id` | 的 [!DNL Amazon Redshift] 连接规范ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Amazon Redshift] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
