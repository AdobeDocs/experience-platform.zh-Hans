---
title: 审核事件API端点
description: 了解如何使用审核查询API在Experience Platform中检索审核事件。
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 9%

---

# 审核事件端点

审核日志用于提供各种服务和功能的用户活动详细信息。 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。的 `/audit/events` 的端点 [!DNL Audit Query] API允许您以编程方式在 [!DNL Platform].

## 快速入门

本指南中使用的API端点是 [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). 在继续之前，请查看 [入门指南](./getting-started.md) 有关相关文档的链接、本文档中的API调用示例指南，以及有关成功调用任何代码所需标头的重要信息 [!DNL Experience Platform] API。

## 列出审核事件

您可以通过向 `/audit/events` 端点，指定要在有效负载中检索的事件。

**API格式**

```http
GET /audit/events
```

的 [!DNL Audit Query] API支持在列出事件时使用查询参数来筛选页面和结果。

| 参数 | 描述 |
| --- | --- |
| `limit` | 响应中要返回的最大记录数。 默认 `limit` 是50。 |
| `start` | 指向返回的搜索结果的第一个项目的指针。 要访问下一页结果，此参数应以所指示的相同数量递增。 示例：要访问限制为50的请求的下一页结果，请使用参数start=50，然后为之后的页面使用start=100，依此类推。 |
| `queryId` | 在对/audit/events端点进行查询时，响应将包含queryId字符串属性。 要在单独的调用中进行相同的查询，您可以将ID值作为单个查询参数包含在内，而无需再次手动配置搜索参数。 |

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

成功的响应会返回在请求中指定的量度和过滤器的生成数据点。

```json
{
   "_embedded": {
     "customerAuditLogList": [
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "32b72208-3035-4bc6-b434-39e34401a864",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "5NphpgUQdQnjTWOcS9DSMs2wD1EUMlYG",
         "authId": "96715f98-d100-4575-8491-ebbcea654eb9",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:58:09.745+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "a178736a-8fa1-47da-bac5-b0d9e741e414",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "7AlGIAhWvaEzYWHLzvuf26AAFAkqSyKg",
         "authId": "60fc1077-4aef-4e1f-a5ff-f64183e060f4",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T21:28:00.301+0000"
       },
       {
         "userEmail": "{USER_ID}",
         "userIpAddresses": [ ],
         "eventType": "Core",
         "id": "ccfe8c77-9b93-481d-a561-0b2edf3b77dc",
         "version": "1.0",
         "imsOrgId": "{ORGANIZATION_ID}",
         "sandboxName": "prod",
         "region": "VA7",
         "requestId": "hArqS4CAa8wfRPnKuxV4yaA82atxwzYu",
         "authId": "80b7d887-9338-4cd5-9d79-2483b03f0160",
         "permissionResource": "Sandbox",
         "permissionType": "RESET",
         "assetType": "Sandbox",
         "assetId": "prod",
         "assetName": "prod",
         "action": "Reset",
         "status": "Allow",
         "failureCode": "",
         "timestamp": "2021-08-04T20:58:07.750+0000"
       }
     ]    
   },
   "_links": {
     "self": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?limit=10&start=0&property=type%253D%253Dcore"
     },
     "next": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&start=10&limit=10"
     },
     "page": {
       "href": "https://platform.adobe.io/data/foundation/audit/events?queryId=cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2&limit=10{&start}",
       "templated": true
     }
  },
  "page": {
    "size": 10,
    "totalElements": 3,
    "totalPages": 1,
    "number": 1
  },
  "queryId": "cXVlcnlJZD0xYjA4MDM4MV81ZWNkXzRjNTZfYTM2N18zYWExOWI5YzNhNTlfMTYyODExNDY5MTg1NSZ0b3RhbEVsZW1lbnRzPTI2"
}
```

| 属性 | 描述 |
| --- | --- |
| `customerAuditLogList` | 一个数组，其对象表示请求中指定的每个事件。 每个对象都包含有关过滤器配置和返回的事件数据的信息。 |
| `userEmail` | 执行事件的用户的电子邮件。 |
| `eventType` | 事件的类型。 事件类型包括 `Core` 和 `Enhanced`. |
| `imsOrgId` | 发生事件的组织的ID。 |
| `permissionResource` | 提供权限的产品或功能可执行该操作。 资源可以是以下任一类型： <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | 操作涉及的权限类型。 |
| `assetType` | 执行操作的平台资源类型。 |
| `assetId` | 执行操作的平台资源的唯一标识符。 |
| `assetName` | 执行操作的平台资源的名称。 |
| `action` | 为事件记录的操作类型。 操作可以是以下任一操作： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | 操作的状态。 状态可以是以下任一状态： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style=&quot;table-layout:auto&quot;}
