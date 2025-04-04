---
keywords: Experience Platform；主页；热门主题；营销自动化
solution: Experience Platform
title: 使用流服务API探索营销自动化系统
description: 本教程使用流服务API来探索营销自动化系统。
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 11%

---

# 使用[!DNL Flow Service] API浏览营销自动化系统

[!DNL Flow Service]用于收集和集中Adobe Experience Platform中各种不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从该API连接。

本教程使用[!DNL Flow Service] API来探索营销自动化系统。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到营销自动化系统所需的其他信息。

### 收集所需的凭据

本教程要求您与希望从中摄取数据的第三方营销自动化应用程序建立有效连接。 有效的连接涉及应用程序的连接规范ID和连接ID。 有关创建营销自动化连接和检索这些值的更多信息，请参阅[将营销自动化源连接到Experience Platform](../../api/create/marketing-automation/hubspot.md)教程。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name： `{SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的媒体类型标头：

* 内容类型： `application/json`

## 浏览您的数据表

使用营销自动化系统的基本连接，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或纳入[!DNL Experience Platform]的表的路径。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 营销自动化系统的基本连接的ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应是由一系列表组成的从到营销自动化系统的响应。 查找要引入[!DNL Experience Platform]的表并记下其`path`属性，因为您需要在下一步中提供该表以检查其结构。

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## 检查表的结构

要从营销自动化系统中检查表的结构，请在将表的路径指定为查询参数时执行GET请求。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 营销自动化系统的连接ID。 |
| `{TABLE_PATH}` | 您的营销自动化系统中表的路径。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回表的结构。 有关每个表列的详细信息位于`columns`数组的元素中。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 后续步骤

通过学习本教程，您已探索您的营销自动化系统，找到要引入[!DNL Experience Platform]的表的路径，并获取有关其结构的信息。 可在下一教程中使用此信息从营销自动化系统[收集数据并将其导入Experience Platform](../collect/marketing-automation.md)。
