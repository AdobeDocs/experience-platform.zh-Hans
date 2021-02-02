---
keywords: Experience Platform；主页；热门主题；电子商务；电子商务
solution: Experience Platform
title: 使用Flow Service API浏览电子商务连接
topic: overview
description: 本教程使用Flow Service API浏览电子商务连接。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API浏览电子商务连接

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用[!DNL Flow Service] API浏览第三方&#x200B;**[!UICONTROL 电子商务]**&#x200B;连接。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用[!DNL Flow Service] API成功连接到&#x200B;**[!UICONTROL eCommerce]**&#x200B;连接。

### 获取连接ID

要使用[!DNL Platform] API探索&#x200B;**[!UICONTROL 电子商务]**&#x200B;连接，您必须拥有有效的连接ID。 如果您尚未连接要使用的&#x200B;**[!UICONTROL eCommerce]**&#x200B;连接，则可以通过以下教程创建一个：

* [Shopify](../create/ecommerce/shopify.md)

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见[!DNL Experience Platform]疑难解答指南中关于如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的一节。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 浏览数据表

使用&#x200B;**[!UICONTROL 电子商务]**&#x200B;连接ID，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或收录到[!DNL Platform]中的表的路径。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_ID}` | 您的&#x200B;**[!UICONTROL 电子商务]**&#x200B;连接ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从&#x200B;**[!UICONTROL eCommerce]**&#x200B;连接返回一组表。 查找要引入[!DNL Platform]的表并记下其`path`属性，因为您需要在下一步中提供它来检查其结构。

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

## Inspect桌子的结构

要从&#x200B;**[!UICONTROL eCommerce]**&#x200B;连接检查表的结构，请在指定`object`GET参数中表的路径时执行查询请求。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | **[!UICONTROL eCommerce]**&#x200B;连接的连接ID。 |
| `{TABLE_PATH}` | **[!UICONTROL eCommerce]**&#x200B;连接中表的路径。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定表的结构。 有关每个表列的详细信息位于`columns`数组的元素中。

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

通过本教程，您探索了&#x200B;**[!UICONTROL 电子商务]**&#x200B;连接，找到了要收录到[!DNL Platform]中的表的路径，并获取了有关其结构的信息。 您可以在下一个教程中使用此信息来收集电子商务数据并将其引入Platform](../collect/ecommerce.md)。[
