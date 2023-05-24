---
title: 工單API端點
description: 資料衛生API中的/workorder端點可讓您以程式設計方式管理身分的刪除任務。
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 3%

---

# 工單端點

此 `/workorder` 資料衛生API中的端點可讓您以程式設計方式管理Adobe Experience Platform中的記錄刪除請求。

>[!IMPORTANT]
>
>記錄刪除請求僅適用於已購買的組織 **AdobeHealthcare Shield**.
>
>
>記錄刪除旨在用於資料清理、匿名資料移除或資料最小化。 它們是 **not** 根據一般資料保護規範(GDPR)等隱私權法規用於資料主體權利請求（法規遵循）。 對於所有合規性使用案例，請使用 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 而非。

## 快速入门

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱 [概觀](./overview.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 建立記錄刪除請求 {#create}

您可以透過向以下專案發出POST請求，從單一資料集或所有資料集中刪除一個或多個身分： `/workorder` 端點。

**API格式**

```http
POST /workorder
```

**请求**

根據 `datasetId` API呼叫會從您指定的所有資料集或單一資料集中刪除身分。 以下請求會從特定資料集中刪除三個身分。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Record Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `action` | 要執行的動作。 值必須設定為 `delete_identity` 記錄刪除。 |
| `datasetId` | 如果您要從單一資料集中刪除，此值必須是相關資料集的ID。 如果您要從所有資料集中刪除，請將值設定為 `ALL`.<br><br>如果您指定單一資料集，資料集的相關Experience Data Model (XDM)結構描述必須定義主要身分。 |
| `displayName` | 記錄刪除請求的顯示名稱。 |
| `description` | 記錄刪除請求的說明。 |
| `identities` | 一個陣列，包含您要刪除其資訊之至少一個使用者的身分。 每個身分識別都由 [身分名稱空間](../../identity-service/namespaces.md) 和一個值：<ul><li>`namespace`：包含單一字串屬性， `code`，代表身分名稱空間。 </li><li>`id`：身分值。</ul>若 `datasetId` 會指定單一資料集，每個實體位於 `identities` 必須使用與結構描述的主要身分相同的身分名稱空間。<br><br>若 `datasetId` 設為 `ALL`，則 `identities` 陣列不受限於任何單一名稱空間，因為每個資料集可能不同。 不過，您的請求仍受限於貴組織可用的名稱空間，如報告所述 [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**响应**

成功的回應會傳回記錄刪除的詳細資料。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 刪除訂單的ID。 這可用於稍後查詢刪除狀態。 |
| `orgId` | 您的组织 ID。 |
| `bundleId` | 與此刪除順序相關聯的套件組合ID，用於偵錯。 多個刪除訂單會整合在一起，由下游服務處理。 |
| `action` | 工單正在執行的動作。 對於記錄刪除，值為 `identity-delete`. |
| `createdAt` | 建立刪除順序的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的目前狀態。 |
| `createdBy` | 建立刪除訂單的使用者。 |
| `datasetId` | 受限於請求的資料集的ID。 如果請求是針對所有資料集，則值將設為 `ALL`. |

{style="table-layout:auto"}

## 擷取記錄刪除的狀態(#lookup)

晚於 [建立記錄刪除請求](#create)，您可以使用GET要求來檢查其狀態。

**API格式**

```http
GET /workorder/{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 此 `workorderId` 您正在查詢的記錄刪除專案。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回刪除操作的詳細資訊，包括其目前狀態。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 刪除訂單的ID。 這可用於稍後查詢刪除狀態。 |
| `orgId` | 您的组织 ID。 |
| `bundleId` | 與此刪除順序相關聯的套件組合ID，用於偵錯。 多個刪除訂單會整合在一起，由下游服務處理。 |
| `action` | 工單正在執行的動作。 對於記錄刪除，值為 `identity-delete`. |
| `createdAt` | 建立刪除順序的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的目前狀態。 |
| `createdBy` | 建立刪除訂單的使用者。 |
| `datasetId` | 受限於請求的資料集的ID。 如果請求是針對所有資料集，則值將設為 `ALL`. |
| `productStatusDetails` | 一個陣列，列出與請求相關的下游處理序的目前狀態。 每個陣列物件都包含以下屬性：<ul><li>`productName`：下游服務的名稱。</li><li>`productStatus`：來自下游服務的請求的目前處理狀態。</li><li>`createdAt`：服務發佈最新狀態的時間戳記。</li></ul> |

## 更新記錄刪除請求

您可以更新 `displayName` 和 `description` 請求刪除PUT記錄。

**API格式**

```http
PUT /workorder{WORK_ORDER_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{WORK_ORDER_ID}` | 此 `workorderId` 您正在查詢的記錄刪除專案。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `displayName` | 記錄刪除請求的更新顯示名稱。 |
| `description` | 記錄刪除請求的更新說明。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回記錄刪除的詳細資料。

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `workorderId` | 刪除訂單的ID。 這可用於稍後查詢刪除狀態。 |
| `orgId` | 您的组织 ID。 |
| `bundleId` | 與此刪除順序相關聯的套件組合ID，用於偵錯。 多個刪除訂單會整合在一起，由下游服務處理。 |
| `action` | 工單正在執行的動作。 對於記錄刪除，值為 `identity-delete`. |
| `createdAt` | 建立刪除順序的時間戳記。 |
| `updatedAt` | 上次更新刪除順序的時間戳記。 |
| `status` | 刪除順序的目前狀態。 |
| `createdBy` | 建立刪除訂單的使用者。 |
| `datasetId` | 受限於請求的資料集的ID。 如果請求是針對所有資料集，則值將設為 `ALL`. |
| `productStatusDetails` | 一個陣列，列出與請求相關的下游處理序的目前狀態。 每個陣列物件都包含以下屬性：<ul><li>`productName`：下游服務的名稱。</li><li>`productStatus`：來自下游服務的請求的目前處理狀態。</li><li>`createdAt`：服務發佈最新狀態的時間戳記。</li></ul> |

{style="table-layout:auto"}
