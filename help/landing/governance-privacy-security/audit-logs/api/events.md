---
title: 审核事件API端点
description: 了解如何使用审核查询API在Experience Platform中检索审核事件。
role: Developer
feature: Audits, API
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: dec895e3ea625fb86d1891bad713185d39c47c81
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 审核事件端点

审核日志用于提供各种服务和功能的用户活动的详细信息。 日志中记录的每个操作都包含元数据，这些元数据指示操作类型、日期和时间、执行操作的用户的电子邮件ID以及与操作类型相关的其他属性。 `/audit/events` API中的[!DNL Audit Query]端点允许您以编程方式检索[!DNL Experience Platform]中组织活动的事件数据。

## 快速入门

本指南中使用的API端点是[[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、此文档中示例API调用的阅读指南，以及有关成功调用任何[!DNL Experience Platform] API所需的所需标头的重要信息。

## 列出审核事件

您可以通过向`/audit/events`端点发出GET请求，指定要在有效负载中检索的事件，来检索事件数据。

**API格式**

```http
GET /audit/events
```

[!DNL Audit Query] API支持在列出事件时使用查询参数来分页和筛选结果。

| 参数 | 描述 |
| --- | --- |
| `limit` | 响应中返回的最大记录数。 默认`limit`为50。 |
| `start` | 指向返回搜索结果的第一个项的指针。 要访问结果的下一页，此参数的增量应该与限制指示的增量相同。 示例：要访问限制为50的请求的下一页结果，请使用参数start=50，然后为之后的页面使用start=100，依此类推。 |
| `queryId` | 向/audit/events端点发出查询时，响应将包含queryId字符串属性。 要在单独的调用中进行相同的查询，您可以将ID值包含为单个查询参数，而不是再次手动配置搜索参数。 |

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events?limit=10
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**响应**

成功的响应会返回请求中指定的量度和过滤器的结果数据点。

```json
{
  "_embedded": {
    "events": [
      {
        "id": "6ecc125d-da03-4882-a944-88c707ddc3f7",
        "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
        "permissionResource": "Dataset",
        "permissionType": "WRITE",
        "assetType": "Dataset",
        "action": "Create",
        "status": "Allow",
        "failureCode": "",
        "timestamp": "2025-06-24T16:50:28.318+0000",
        "version": "1.0",
        "imsOrgId": "{ORGANIZATION_ID}",
        "region": "VA7",
        "authId": "e6b46821-e2b4-4729-952f-2e4afd713b31",
        "assetId": "685ad754fb1abe2b263df4b3",
        "assetName": "my-dataset",
        "sandboxName": "prod",
        "sandboxId": "{SANDBOX_ID}",
        "userEmail": "{USER_EMAIL}",
        "userIpAddresses": [
          "130.*.*.*",
          "10.*.*.*"
        ],
        "enhancedEvents": [
          {
            "id": "0ee91e42-ac46-4f35-a01a-f74a1569c404",
            "requestId": "5YGdpTX5PvRrdqCfrCT8p8lWphZPzxl8",
            "permissionResource": "Dataset",
            "permissionType": "Write",
            "assetType": "Dataset",
            "action": "Create",
            "status": "Success",
            "failureCode": "",
            "timestamp": "2025-06-24T16:50:28.883+0000",
            "assetId": "685ad754fb1abe2b263df4b3",
            "assetName": "my-dataset"
          }
        ]
      }
    ]
  },
  "_links": {
    "self": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?property=user%253D%253Ddraghici%2540adobe.com"
    },
    "page": {
      "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3&limit=50{&start}",
      "templated": true
    }
  },
  "page": {
    "size": 1,
    "totalElements": 1,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "b3JkZXJCeVJ1bGVzPSZwcm9wZXJ0eT11c2VyPT1kcmFnaGljaUBhZG9iZS5jb20mdGltZXN0YW1wSW5kZXg9MTc1MDc4MzgyODMxOCZ0b3RhbEVsZW1lbnRzPTE3"
}
```

| 属性 | 描述 |
| --- | --- |
| `events` | 一个数组，其对象表示请求中指定的每个事件。 每个对象都包含有关过滤器配置和返回的事件数据的信息。 |
| `userEmail` | 执行事件的用户的电子邮件。 |
| `eventType` | 事件的类型。 事件类型包括`Core`和`Enhanced`。 |
| `imsOrgId` | 发生事件的组织的ID。 |
| `permissionResource` | 提供权限的产品或功能会执行该操作。 资源可以是以下任一资源： <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | 操作涉及的权限类型。 |
| `assetType` | 执行操作的Experience Platform资源的类型。 |
| `assetId` | 执行操作的Experience Platform资源的唯一标识符。 |
| `assetName` | 执行操作的Experience Platform资源的名称。 |
| `action` | 为事件记录的操作类型。 操作可以是以下任一操作： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | 操作的状态。 状态可以是以下任一状态： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
