---
title: 配額API端點
description: 資料衛生API中的/quota端點可讓您根據貴組織每個工作型別的每月配額限制，監控資料衛生使用情況。
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 1c6a5df6473e572cae88a5980fe0db9dfcf9944e
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 配額端點

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料檢疫功能目前僅適用於已購買的組織 **AdobeHealthcare Shield** 或 **Adobe隱私權與安全性盾牌**.

此 `/quota` 資料衛生API中的端點可讓您根據貴組織的每個工作型別的配額限制，監控資料衛生使用情況。

系統會以下列方式為每個資料衛生工作型別執行配額：

* 記錄刪除和更新限製為每月特定數量的請求。
* 資料集有效期的同時作用中工作數有固定限制，無論何時執行有效期。

## 快速入门

本指南中使用的端點屬於資料衛生API。 在繼續之前，請檢閱 [概觀](./overview.md) 以取得下列資訊：

* 相關檔案的連結
* 閱讀本檔案中範例API呼叫的指南
* 成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊

## 清單配額 {#list}

您可以透過向以下網站發出GET要求來檢視貴組織的配額資訊： `/quota` 端點。

**API格式**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{QUOTA_TYPE}` | 指定要擷取的配額型別的可選查詢引數。 若否 `quotaType` 引數，則API回應中會傳回所有配額值。 接受的型別值包括：<ul><li>`expirationDatasetQuota`：資料集有效期</li><li>`deleteIdentityWorkOrderDatasetQuota`：記錄刪除</li><li>`fieldUpdateWorkOrderDatasetQuota`：記錄更新</li></ul> |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**响应**

成功的回應會傳回資料檢疫配額的詳細資料。

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Record Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `quotas` | 列出每個資料檢疫工作型別的配額資訊。 每個配額物件都包含以下屬性：<ul><li>`name`：資料衛生工作型別：<ul><li>`expirationDatasetQuota`：資料集有效期</li><li>`deleteIdentityWorkOrderDatasetQuota`：記錄刪除</li></ul></li><li>`description`：資料衛生工作型別的說明。</li><li>`consumed`：在目前每月期間執行的此型別工作數。</li><li>`quota`：此工作型別的配額限制。 對於記錄刪除和更新，這表示每個月期間可以執行的工作數量。 對於資料集有效期，這表示在指定時間可以並行作用中的工作數量。</li></ul> |

{style="table-layout:auto"}
