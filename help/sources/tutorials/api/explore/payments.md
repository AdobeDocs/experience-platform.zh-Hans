---
keywords: Experience Platform;home;popular topics;payment
solution: Experience Platform
title: 使用Flow Service API探索支付系统
topic: overview
description: 本教程使用Flow Service API来浏览付款应用程序。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---


# 使用API浏览支付系 [!DNL Flow Service] 统

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用 [!DNL Flow Service] API探索付款应用程序。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到付款应用程 [!DNL Flow Service] 序。

### 收集所需的凭据

本教程要求您与要从中获取数据的第三方支付应用程序建立有效连接。 有效的连接涉及应用程序的连接规范ID和连接ID。 有关创建付款连接和检索这些值的更多信息，请参 [阅将付款源连接到平台教程](../../api/create/payments/paypal.md) 。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 浏览数据表

使用付款系统的连接ID，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或收录到的表的路径 [!DNL Platform]。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 付款基础连接的ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从付款系统返回一组表。 查找要引入的表并 [!DNL Platform] 记下其属 `path` 性，因为您需要在下一步中提供它来检查其结构。

```json
[
    {
        "type": "table",
        "name": "PayPal.Billing_Plans",
        "path": "PayPal.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Billing_Plans_Payment_Definition",
        "path": "PayPal.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "PayPal.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Catalog_Products",
        "path": "PayPal.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect桌子的结构

要从付款系统检查表的结构，请在将表的路径指定为GET参数时执行查询请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 付款系统的连接ID。 |
| `{TABLE_PATH}` | 支付系统中表的路径。 |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定表的结构。 有关每个表列的详细信息位于数组元素 `columns` 中。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
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

通过本教程，您探索了支付系统，找到了要收录的表的路径，并获 [!DNL Platform]得了有关其结构的信息。 您可以在下一个教程中使用此信 [息从支付系统收集数据并将其引入平台](../collect/payments.md)。