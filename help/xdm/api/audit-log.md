---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；稽核；稽核記錄；變更記錄；變更記錄；rpc；
solution: Experience Platform
title: 稽核記錄API端點
description: 結構描述登入API中的/auditlog端點可讓您擷取對現有XDM資源所做的變更的年代順序清單。
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# 稽核記錄端點

對於每個Experience Data Model (XDM)資源， [!DNL Schema Registry] 維護在不同更新之間發生的所有變更記錄。 此 `/auditlog` 中的端點 [!DNL Schema Registry] API可讓您為ID指定的任何類別、結構描述欄位群組、資料型別或結構描述擷取稽核記錄。

## 快速入门

本指南中使用的端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

此 `/auditlog` 端點是遠端程式呼叫(RPC)的一部分，受 [!DNL Schema Registry]. 不像 [!DNL Schema Registry] API、RPC端點不需要其他標頭，例如 `Accept` 或 `Content-Type`，且請勿使用 `CONTAINER_ID`. 相反地，他們必須使用 `/rpc` 名稱空間，如下面的API呼叫所示。

## 擷取資源的稽核記錄

您可以在「架構資料庫」中擷取任何類別、欄位群組、資料型別或架構的稽核記錄，方法是在GET要求的路徑中指定資源的ID， `/auditlog` 端點。

**API格式**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{RESOURCE_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要擷取其稽核記錄之資源的URL。 |

{style="table-layout:auto"}

**请求**

下列要求會擷取結構的稽核記錄。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回資源變更的時間順序清單（從最近到最近）。

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| 属性 | 描述 |
| --- | --- |
| `updates` | 一個物件陣列，每個物件代表對指定資源或其相依資源之一所做的變更。 |
| `id` | 此 `$id` 已變更的資源的檔案名稱。 此值通常代表請求路徑中指定的資源，但如果是變更的來源，則可能代表相依資源。 |
| `xdmType` | 已變更的資源型別。 |
| `action` | 已進行的變更型別。 |
| `path` | A [JSON指標](../../landing/api-fundamentals.md#json-pointer) 字串，指出已變更或新增之特定欄位的路徑。 |
| `value` | 指派給新欄位或更新欄位的值。 |

{style="table-layout:auto"}
