---
keywords: Experience Platform；主页；热门主题；Advertising System；Advertising System
solution: Experience Platform
title: 使用流服务API浏览Advertising系统
description: 流量服务用于从Adobe Experience Platform内各种不同的来源收集和集中客户数据。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从该API连接。 本教程使用流服务API来探索广告系统。
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API浏览广告系统

在创建基本连接后，您现在可以使用唯一的基本连接ID来导航和浏览源的数据结构和内容。 这允许您在创建数据流并将它们引进Adobe Experience Platform之前，识别特定项目及其各自的数据类型和格式。

本教程使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)来浏览广告系统。

## 快速入门

>[!IMPORTANT]
>
>本教程要求您拥有广告源的唯一基本连接ID。 如果您没有此ID，请参阅有关[将广告源连接到Experience Platform](../../api/create/advertising/ads.md)的教程。

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功连接到广告系统所需了解的其他信息。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../landing/api-guide.md)指南。

## 浏览您的数据表

通过使用广告系统的基本连接，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或纳入[!DNL Experience Platform]的表的路径。

**API格式**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 广告系统的基本连接的ID。 |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应是从到广告系统的大量表。 查找要引入[!DNL Experience Platform]的表并记下其`path`属性，因为您需要在下一步中提供该表以检查其结构。

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 检查表的结构

要从广告系统检查表的结构，请在将表的路径指定为查询参数时执行GET请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 广告系统的连接ID。 |
| `{TABLE_PATH}` | 广告系统中表的路径。 |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
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
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## 后续步骤

通过完成本教程，您已探索广告系统，找到要引入[!DNL Experience Platform]的表的路径，并获取有关其结构的信息。 您可以在下一个教程中使用此信息从广告系统[收集数据并将其引入Experience Platform](../collect/advertising.md)。
