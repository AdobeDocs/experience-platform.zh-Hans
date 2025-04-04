---
keywords: Experience Platform；主页；热门主题；源；API；浏览；流服务
title: 使用流服务API浏览表格式Source
description: 本教程使用流服务API来探索基于表的源的内容和结构。
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API浏览数据表

本教程提供了有关如何使用[[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API浏览和预览数据表结构和内容的步骤。

>[!NOTE]
>
> 要浏览数据表，您必须已经拥有表格式源的有效基本连接ID。 如果您没有此ID，请参阅以下教程，以了解如何为表格式源创建基本连接ID的步骤： <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客户成功](../../../home.md#customer-success)</li><li>[数据库](../../../home.md#database)</li><li>[电子商务](../../../home.md#ecommerce)</li><li>[营销自动化](../../../home.md#marketing-automation)</li><li>[付款](../../../home.md#payments)</li><li>[协议](../../../home.md#protocols)</li></ul>

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../landing/api-guide.md)指南。

## 浏览您的数据表

您可以在提供源的基本连接ID的同时向[!DNL Flow Service] API发出GET请求，以检索有关数据表结构的信息。

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

成功的响应会从源中返回表数组。 查找要带入Experience Platform的表并记下其`path`属性，因为在下一步中需要提供该表以检查其结构。

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

## 检查表的结构

要检查数据表的内容，请在将表的路径指定为查询参数时对[!DNL Flow Service] API执行GET请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本连接ID。 |
| `{TABLE_PATH}` | 要检查的表的path属性。 |

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

成功的响应将返回有关指定表的内容和结构的信息。 有关每个表列的详细信息位于`columns`数组的元素中。

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

通过学习本教程，您已收集有关数据表结构和内容的信息。 此外，您已检索要纳入Experience Platform的表的路径。 您可以使用此信息创建源连接和数据流，将您的数据引入到Experience Platform。 有关如何使用[!DNL Flow Service] API创建源连接和数据流的特定步骤，请参阅以下教程：

* [Advertising源](../collect/advertising.md)
* [CRM源](../collect/crm.md)
* [客户成功来源](../collect/customer-success.md)
* [数据库源](../collect/database-nosql.md)
* [电子商务来源](../collect/ecommerce.md)
* [营销自动化源](../collect/marketing-automation.md)
* [付款来源](../collect/payments.md)
* [协议源](../collect/protocols.md)
