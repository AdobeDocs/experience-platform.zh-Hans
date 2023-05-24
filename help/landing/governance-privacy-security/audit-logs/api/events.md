---
title: 稽核事件API端點
description: 瞭解如何使用稽核查詢API在Experience Platform中擷取稽核事件。
exl-id: c365b6d8-0432-41a5-9a07-44a995f69b7d
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 8%

---

# 稽核事件端點

稽核記錄可用於提供各種服務和功能的使用者活動細節。 日志中记录的每个操作都包含元数据，这些元数据可指示操作类型、日期和时间、执行操作的用户的电子邮件 ID 以及与操作类型相关的其他属性。此 `/audit/events` 中的端點 [!DNL Audit Query] API可讓您以程式設計方式為貴組織的活動擷取事件資料，位置在： [!DNL Platform].

## 快速入门

本指南中使用的API端點是 [[!DNL Audit Query] API](https://developer.adobe.com/experience-platform-apis/references/audit-query/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 列出稽核事件

您可以向以下發出GET要求來擷取事件資料： `/audit/events` 端點，指定您要在裝載中擷取的事件。

**API格式**

```http
GET /audit/events
```

此 [!DNL Audit Query] API支援在列出事件時使用查詢引數來頁面和篩選結果。

| 参数 | 描述 |
| --- | --- |
| `limit` | 回應中可傳回的最大記錄數。 預設 `limit` 為50。 |
| `start` | 針對傳回的搜尋結果，指向第一個專案的指標。 若要存取結果的下一頁，此引數的增量應該與限制所指示的量相同。 範例：若要存取limit=50之要求的下一頁結果，請使用start=50引數，然後對其後的頁面使用start=100引數，以此類推。 |
| `queryId` | 向/audit/events端點提出查詢時，回應會包含queryId字串屬性。 若要在個別呼叫中進行相同的查詢，您可以將ID值納入為單一查詢引數，而非再次手動設定搜尋引數。 |

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

成功的回應會針對請求中指定的量度和篩選器傳回產生的資料點。

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
| `customerAuditLogList` | 一個陣列，其物件代表要求中指定的每個事件。 每個物件都包含有關篩選設定和傳回事件資料的資訊。 |
| `userEmail` | 執行事件之使用者的電子郵件。 |
| `eventType` | 事件型別。 事件型別包括 `Core` 和 `Enhanced`. |
| `imsOrgId` | 發生事件之組織的ID。 |
| `permissionResource` | 提供許可權的產品或功能會執行動作。 資源可以是下列任一專案： <ul><li>`Activation` </li><li>`ActivationAssociation` </li><li>`AnalyticSource` </li><li>`AudienceManagerSource` </li><li>`BizibleSource` </li><li>`CustomerAttributeSource` </li><li>`Dataset` </li><li>`EnterpriseSource` </li><li>`LaunchSource` </li><li>`MarketoSource` </li><li>`ProductProfile` </li><li>`ProfileConfig` </li><li>`Sandbox` </li><li>`Schema` </li><li>`Segment` </li><li>`StreamingSource` </li></ul> |
| `permissionType` | 動作涉及的許可權型別。 |
| `assetType` | 執行動作的Platform資源型別。 |
| `assetId` | 執行動作的Platform資源的唯一識別碼。 |
| `assetName` | 執行動作的Platform資源名稱。 |
| `action` | 為事件記錄的動作型別。 動作可以是下列任一專案： <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`remove` </li><li>`reset` </li><li>`segment activate` </li><li>`segment remove` </li><li>`update` </li></ul> |
| `status` | 動作的狀態。 狀態可以是下列任一專案： </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul> |

{style="table-layout:auto"}
