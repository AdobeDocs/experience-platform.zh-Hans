---
keywords: Experience Platform；主页；热门主题；veeva crm；Veeva CRM；Veeva；
solution: Experience Platform
title: 使用流服务API创建Veeva CRM基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Veeva CRM。
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---

# 创建 [!DNL Veeva CRM] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Veeva CRM] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Veeva CRM] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Veeva CRM]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | 的URL [!DNL Veeva CRM] 实例。 |
| `username` | 的用户名值 [!DNL Veeva CRM] 帐户。 |
| `password` | 的密码值 [!DNL Veeva CRM] 帐户。 |
| `securityToken` | 您的安全令牌 [!DNL Veeva CRM] 实例。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL Veeva CRM] 为： `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

有关这些值的更多信息，请参阅此 [[!DNL Veeva CRM] 文档](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Veeva CRM] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Veeva CRM]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 您的名称 [!DNL Veeva CRM] 基本连接。 您可以使用此名称查找 [!DNL Veeva CRM] 基本连接。 |
| `description` | 的可选描述 [!DNL Veeva CRM] 基本连接。 |
| `auth.specName` | 用于连接的身份验证类型。 |
| `auth.params.environmentUrl` | 的URL [!DNL Veeva CRM] 实例。 |
| `auth.params.username` | 的用户名值 [!DNL Veeva CRM] 帐户。 |
| `auth.params.password` | 的密码值 [!DNL Veeva CRM] 帐户。 |
| `auth.params.securityToken` | 您的安全令牌 [!DNL Veeva CRM] 实例。 |
| `connectionSpec.id` | 的连接规范ID [!DNL Veeva CRM]： `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**响应**

成功响应将返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中创建源连接时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

## 后续步骤

按照本教程，您已创建了一个 [!DNL Veeva CRM] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将CRM数据引入平台 [!DNL Flow Service] API](../../collect/crm.md)
