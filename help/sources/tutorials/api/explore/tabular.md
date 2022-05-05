---
keywords: Experience Platform；主页；热门主题；源；API；浏览；流程服务
title: 使用流量服务API浏览表格源
description: 本教程使用流量服务API来探索基于表的源的内容和结构。
source-git-commit: 1333eac5e022ef32f051120496154a88e2f9324e
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教程提供了有关如何使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
> 要浏览数据表，您必须已拥有表格源的有效基本连接ID。 如果您没有此ID，请参阅以下教程，了解如何为表格源创建基本连接ID的步骤： <ul><li>[广告](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客户成功](../../../home.md#customer-success)</li><li>[数据库](../../../home.md#database)</li><li>[电子商务](../../../home.md#ecommerce)</li><li>[营销自动化](../../../home.md#marketing-automation)</li><li>[支付](../../../home.md#payments)</li><li>[协议](../../../home.md#protocols)</li></ul>

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../landing/api-guide.md).

## 浏览数据表

您可以通过向 [!DNL Flow Service] API，同时提供源的基本连接ID。

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

成功的响应会从源中返回一个表数组。 查找要引入Platform的表，并注意其 `path` 资产，因为您需要在下一步中提供该资产以检查其结构。

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

要检查数据表的内容，请向 [!DNL Flow Service] 将表的路径指定为查询参数时的API。

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

成功的响应会返回有关指定表的内容和结构的信息。 有关每个表列的详细信息位于 `columns` 数组。

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

通过阅读本教程，您已收集了有关数据表结构和内容的信息。 此外，您还检索了要摄取到平台中的表的路径。 您可以使用此信息创建源连接和数据流，以将数据引入平台。 有关如何使用创建源连接和数据流的具体步骤，请参阅以下教程 [!DNL Flow Service] API:

* [广告源](../collect/advertising.md)
* [CRM源](../collect/crm.md)
* [客户成功来源](../collect/customer-success.md)
* [数据库源](../collect/database-nosql.md)
* [电子商务来源](../collect/ecommerce.md)
* [营销自动化来源](../collect/marketing-automation.md)
* [付款来源](../collect/payments.md)
* [协议源](../collect/protocols.md)