---
keywords: Experience Platform；主页；热门主题；付款
solution: Experience Platform
title: 利用流服务API开发支付系统
topic-legacy: overview
description: 本教程使用流量服务API来探索支付应用程序。
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用 [!DNL Flow Service] 用于探索支付应用程序的API。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 收集所需的凭据

本教程要求您与要从中摄取数据的第三方支付应用程序建立有效连接。 有效的连接涉及您的应用程序的连接规范ID和连接ID。 有关创建付款连接和检索这些值的更多信息，请参阅 [将支付源连接到平台](../../api/create/payments/paypal.md) 教程。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

## 浏览数据表

使用支付系统的连接ID，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或摄取到的表的路径 [!DNL Platform].

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 支付基础连接的ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从支付系统返回一组表。 找你想进去的桌子 [!DNL Platform] 并注意 `path` 资产，因为您需要在下一步中提供该资产以检查其结构。

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

## Inspect表的结构

要从支付系统检查表的结构，请在将表的路径指定为查询参数时执行GET请求。

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定表的结构。 有关每个表列的详细信息位于 `columns` 数组。

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

通过阅读本教程，您探索了您的支付系统，找到了要引入的表的路径 [!DNL Platform]，并获取了有关其结构的信息。 在下一个教程中，您可以在 [从支付系统收集数据并将其导入平台](../collect/payments.md).
