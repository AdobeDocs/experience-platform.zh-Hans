---
keywords: Experience Platform；主页；热门主题；源；API；浏览；流服务
title: 使用流服务API浏览表格源
description: 本教程使用流服务API来探索基于表的源的内容和结构。
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 2%

---

# 使用浏览数据表 [!DNL Flow Service] API

本教程提供了有关如何使用来浏览和预览数据表的结构和内容的步骤。 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
> 要浏览数据表，您必须已经拥有表格式源的有效基本连接ID。 如果您没有此ID，请参阅以下教程，以了解如何为表格式源创建基本连接ID的步骤： <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客户成功](../../../home.md#customer-success)</li><li>[数据库](../../../home.md#database)</li><li>[电子商务](../../../home.md#ecommerce)</li><li>[营销自动化](../../../home.md#marketing-automation)</li><li>[支付](../../../home.md#payments)</li><li>[协议](../../../home.md#protocols)</li></ul>

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../landing/api-guide.md).

## 浏览您的数据表

您可以通过对以下对象发出GET请求，检索有关数据表结构的信息 [!DNL Flow Service] 提供源的基本连接ID时的API。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本连接ID。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从源中返回表数组。 找到您要带入Platform的表格并记下该表格 `path` 属性，因为您需要在下一步中提供它以检查其结构。

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表的结构

GET要检查数据表的内容，请向 [!DNL Flow Service] 将表的路径指定为查询参数时使用的API。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本连接ID。 |
| `{TABLE_PATH}` | 要检查的表的路径属性。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回有关指定表的内容和结构的信息。 有关每个表列的详细信息位于 `columns` 数组。

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## 后续步骤

通过阅读本教程，您已收集有关数据表结构和内容的信息。 此外，您已检索要摄取到Platform中的表的路径。 您可以使用此信息创建源连接和数据流，以将您的数据传送到Platform。 有关如何使用创建源连接和数据流的特定步骤，请参阅以下教程 [!DNL Flow Service] API：

* [广告源](../collect/advertising.md)
* [CRM源](../collect/crm.md)
* [客户成功来源](../collect/customer-success.md)
* [数据库源](../collect/database-nosql.md)
* [电子商务来源](../collect/ecommerce.md)
* [营销自动化源](../collect/marketing-automation.md)
* [付款来源](../collect/payments.md)
* [协议源](../collect/protocols.md)
