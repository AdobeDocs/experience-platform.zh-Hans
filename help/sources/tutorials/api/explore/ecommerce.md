---
keywords: Experience Platform；主页；热门主题；电子商务；电子商务
solution: Experience Platform
title: 使用流服务API探索电子商务连接
description: 本教程使用流服务API来探索电子商务连接。
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# 使用探索电子商务连接 [!DNL Flow Service] API

[!DNL Flow Service] 用于从Adobe Experience Platform中各种不同的来源收集客户数据并对其进行集中。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从此API进行连接。

本教程使用 [!DNL Flow Service] 用于探索第三方的API **[!UICONTROL 电子商务]** 连接。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Sources]](../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接到 **[!UICONTROL 电子商务]** 连接使用 [!DNL Flow Service] API。

### 获取连接ID

为了探索您的 **[!UICONTROL 电子商务]** 连接使用 [!DNL Platform] API，您必须拥有有效的连接ID。 如果您尚未为 **[!UICONTROL 电子商务]** 要使用的连接，可通过以下教程创建一个连接：

* [Shopify](../create/ecommerce/shopify.md)

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 浏览您的数据表

使用您的 **[!UICONTROL 电子商务]** 连接ID，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或摄取的表的路径 [!DNL Platform].

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_ID}` | 您的 **[!UICONTROL 电子商务]** 连接ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从 **[!UICONTROL 电子商务]** 连接。 查找您要引入的表 [!DNL Platform] 并注意其 `path` 属性，因为您需要在下一步中提供它以检查其结构。

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表的结构

要从检查表中表的结构，请执行以下操作 **[!UICONTROL 电子商务]** 连接，执行GET请求时指定表在 `object` 查询参数。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的连接ID **[!UICONTROL 电子商务]** 连接。 |
| `{TABLE_PATH}` | 中的表路径 **[!UICONTROL 电子商务]** 连接。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回指定表的结构。 有关每个表列的详细信息位于 `columns` 数组。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## 后续步骤

通过学习本教程，您已探索 **[!UICONTROL 电子商务]** connection ，找到要摄取的表的路径 [!DNL Platform]，并获得了有关其结构的信息。 您可以在下一教程中使用此信息来 [收集电子商务数据并将其引入平台](../collect/ecommerce.md).
