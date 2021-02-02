---
keywords: Experience Platform；主页；热门主题；ssc;SSC;Salesforce Service Cloud;salesforce Service Cloud
solution: Experience Platform
title: 使用流服务API创建Salesforce Service Cloud连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到Salesforce Service Cloud（以下简称“SSC”）的步骤。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API创建[!DNL Salesforce Service Cloud]连接器

>[!NOTE]
>
>[!DNL Salesforce Service Cloud]接头为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL Salesforce Service Cloud]（以下称“SSC”）的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到SSC所需了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]与SSC连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 用户帐户的用户名。 |
| `password` | 用户帐户的密码。 |
| `securityToken` | 用户帐户的安全令牌。 |

有关入门的详细信息，请参阅[此Salesforce服务云文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个SSC帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建SSC连接，其唯一连接规范ID必须作为POST请求的一部分提供。 SSC的连接规范ID为`b66ab34-8619-49cb-96d1-39b37ede86ea`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.username` | 与您的SSC帐户关联的用户名。 |
| `auth.params.password` | 与您的SSC帐户关联的密码。 |
| `auth.params.securityToken` | 与您的SSC帐户关联的安全令牌。 |
| `connectionSpec.id` | 在上一步骤中检索的SSC帐户的连接规范`id`。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一标识符(`id`)。 需要此ID才能在下一步中浏览您的CRM系统。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

通过本教程，您已使用[!DNL Flow Service] API创建了SSC连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何[使用流服务API](../../explore/customer-success.md)探索客户成功系统。
