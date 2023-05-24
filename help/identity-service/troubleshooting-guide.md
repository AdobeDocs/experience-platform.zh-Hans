---
keywords: Experience Platform；首頁；熱門主題；身分名稱空間；身分名稱空間
solution: Experience Platform
title: Identity Service疑難排解指南
description: 本檔案提供有關Adobe Experience Platform Identity Service常見問題的解答，以及常見錯誤的疑難排解指南。
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '2176'
ht-degree: 0%

---

# Identity Service疑難排解指南

本檔案提供有關Adobe Experience Platform常見問題的解答 [!DNL Identity Service]以及常見錯誤的疑難排解指南。 有關下列專案的問題和疑難排解： [!DNL Platform] API一般而言，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md).

用來識別單一客戶的資料，通常分散於客戶用來與您的品牌互動的各種裝置和系統。 [!DNL Identity Service] 將這些分散的身分識別彙集在一起，有助於全面瞭解客戶行為，以便您即時提供具影響力的數位體驗。 如需詳細資訊，請參閱 [Identity Service概觀](./home.md).

## 常见问题解答

以下為常見問題集的回答清單 [!DNL Identity Service].

## 什麼是身分資料？

身分資料是指可用於識別個人身分的任何資料。 根據組織內使用資料的方式環境，身分資料可以包含來自CRM系統的使用者名稱、電子郵件地址和ID。 身分資料不限於您網站或服務的註冊使用者，因為匿名使用者也可以透過其裝置或Cookie ID識別。

## 將資料欄位標示為身分有什麼好處？

將特定資料欄位標示為記錄和時間序列資料中的身分，可讓您在資料的自然結構內對應身分關係，並跨管道調解重複資料。 請參閱 [Identity Service概觀](./home.md) 以取得詳細資訊。

## 什麼是已知和匿名的身分？

已知的身分識別是指一個身分識別值，可以單獨使用，或搭配其他資訊使用，以識別、聯絡或尋找個別人員。 已知的身分範例可能包括電子郵件地址、電話號碼和CRM ID。

匿名身分是指無法單獨使用或搭配其他資訊使用，以識別、聯絡或尋找個別人員（例如Cookie ID）的身分值。

## 什麼是私人身分圖表？

私人身分圖表是拼接和連結的身分之間關係的私人對應，僅對您的組織可見。

從串流端點擷取或傳送至啟用的資料集的任何資料中包含多個身分時 [!DNL Identity Service]，這些身分會在私人身分圖表中進行連結。 [!DNL Identity Service] 會利用此圖表來收集指定消費者或實體的身分，以允許身分拼接和設定檔合併。

## 如何在XDM結構描述中建立多個身分欄位？

[體驗資料模型(XDM)](../xdm/home.md) 結構描述支援多個身分欄位。 任何型別的資料欄位 `string` 在實作XDM Individual Profile或XDM ExperienceEvent類別的結構描述中，可以標籤為身分欄位。 在標籤後，這些欄位中包含的任何資料都會新增到設定檔的身分對應。

有關如何使用使用者介面將XDM欄位標示為身分欄位的步驟，請參閱 [身分段落](../xdm/tutorials/create-schema-ui.md) 架構編輯器教學課程中的。 如果您使用API，請參閱 [身分描述項段落](../xdm/tutorials/create-schema-api.md) 在Schema Registry API教學課程中。

## 是否有某些欄位不應標示為身分的上下文？

身分欄位應該保留給每個人的唯一值。 例如，考慮客戶忠誠度計畫的資料集。 「忠誠度」欄位（金級、銀級、銅級）不是實用的身分欄位，而「忠誠度ID」（唯一值）則是。

郵遞區號和IP位址等欄位不應標籤為個人的身分，因為這些值可套用至多個個人。 這些型別的欄位應該只標籤為家庭層級行銷策略的身分。

## 為什麼我的身分識別欄位沒有依照我預期的方式連結？

使用 [`/cluster/members` 端點](./api/list-cluster-identites.md) 在Identity Service API中，您可以檢視一或多個身分欄位的關聯身分。 如果回應未傳回您期望的連結身分，請確定您在XDM資料中提供適當的身分資訊。 請參閱以下小節： [向Identity Service提供XDM資料](./home.md) 如需詳細資訊，請參閱Identity Service概觀。

## 什麼是身分名稱空間？

身分名稱空間會提供身分欄位與客戶身分的相關性的上下文。 例如，「電子郵件」名稱空間下的身分欄位應符合標準電子郵件格式（名稱）<span>@emailprovider.com)，而使用「電話」名稱空間的欄位應符合標準電話號碼（例如在北美洲987-555-1234）。

名稱空間會區分不同CRM系統之間的類似身分值。 例如，假設某個設定檔包含與公司獎勵計畫相關聯的數位熟客ID。 「忠誠度」的名稱空間會將此值與也出現在相同設定檔中的電子商務系統的類似數值ID分開。

請參閱 [身分名稱空間總覽](./home.md) 以取得詳細資訊。

## 如何將身分與身分名稱空間建立關聯？

身分欄位建立時，必須與現有的身分名稱空間相關聯。 任何新名稱空間都必須是 [使用API建立](#how-do-i-create-a-custom-namespace-for-my-organization) 將它們與身分欄位建立關聯之前。

如需在使用API建立身分描述項時定義名稱空間的逐步指示，請參閱 [建立描述項](../xdm/tutorials/create-schema-ui.md) 在Schema Registry開發人員指南中。 若要在UI中將結構描述欄位標示為身分，請依照 [結構描述編輯器教學課程](../xdm/tutorials/create-schema-api.md).

## Experience Platform提供哪些標準身分名稱空間？ {#standard-namespaces}

標準身分名稱空間是可供所有組織使用的名稱空間。 請參閱 [身分名稱空間概觀](./namespaces.md) 以取得可用標準名稱空間的完整清單。

## 我可以在哪裡找到我的組織可用的身分名稱空間清單？

使用 [身分識別服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以透過向以下網站發出GET請求，列出貴組織所有可用的身分名稱空間： `/idnamespace/identities` 端點。 請參閱以下小節： [列出可用的名稱空間](./api/list-namespaces.md) 如需詳細資訊，請參閱Identity Service API總覽。

## 如何為我的組織建立自訂名稱空間？

使用 [身分識別服務API](https://www.adobe.io/experience-platform-apis/references/identity-service)，您可以透過向以下網站發出POST請求，為您的組織建立自訂身分名稱空間： `/idnamespace/identities` 端點。 請參閱以下小節： [建立自訂名稱空間](./api/create-custom-namespace.md) 如需詳細資訊，請參閱Identity Service API總覽。

## 什麼是複合身分和XID？

在API呼叫中，身分會由其複合身分或XID參照。 複合身分是包含ID值和名稱空間的身分的表示法。 XID是單值識別碼，代表與複合身分相同的結構（ID和名稱空間），當身分識別服務持續存在時，會自動指派給新身分。 請參閱 [Identity Service API總覽](./home.md) 以取得詳細資訊。

## Identity Service如何處理個人識別資訊(PII)？

Identity Service具有標準名稱空間，可支援擷取電話號碼和電子郵件的雜湊身分值。 不過，您必須負責雜湊值。 若要進一步瞭解如何對擷取至Platform的資料進行雜湊處理，請參閱 [[!DNL Data Prep] 對應函式指南](../data-prep/functions.md#hashing).

## 雜湊處理PII型身分時，是否有任何考量事項？

如果您將雜湊PII值傳送至Identity Service，您必須在資料集中使用相同的加密方法。 這可確保跨資料集的相同身分值會產生相同的雜湊值，並能夠在身分圖表中正確比對和連結。

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## 為何無法存取身分圖表頁面或API？

您的平台管理員必須為您布建 `view-identity-graph` 許可權供您檢視身分圖表資料。 若沒有此許可權，您將在身分圖表檢視器頁面上以及呼叫Platform API時，收到許可權遭拒訊息。 請參閱 [存取控制概述](../access-control/home.md) 以取得許可權的詳細資訊。

## 故障排除

下節針對您在使用時可能會遇到的特定錯誤碼和意外行為，提供疑難排解建議 [!DNL Identity Service] API。

## [!DNL Identity Service] 錯誤訊息

以下為使用時可能會遇到的錯誤訊息清單 [!DNL Identity Service] API。

### 缺少必要的查詢引數

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

請求路徑中未包含必要的查詢引數時，便會顯示此錯誤。 此 `detail` 錯誤訊息的)提供遺失引數的名稱。 此錯誤訊息的變化包括：

- 缺少必要的查詢引數 — nsId
- 缺少必要的查詢引數 — id
- 缺少必要的查詢引數 — xid或(nsid，id)
- 缺少必要的查詢引數 — targetNs
- 缺少必要的查詢引數 — xids或compositeXids

在重試之前，請檢查您在請求路徑中是否正確包含指示的引數。

### 時間戳記應在過去180天內

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] 會清除超過180天的資料。 當您嘗試存取超過此的資料時，會顯示此錯誤訊息。

### 單一呼叫中有1000個XID的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

當您嘗試擷取的身分資訊超過最大數量時，此錯誤訊息便會顯示 [XID](#what-are-composite-identities-and-xids) 單一API呼叫中允許。 將請求中的XID數量減少至顯示限制以下，即可解決此問題。


### 單一呼叫中有1000個compositeXid的限制

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

當您嘗試擷取的身分資訊超過最大數量時，此錯誤訊息便會顯示 [複合身分](#what-are-composite-identities-and-xids) 單一API呼叫中允許。 將請求中的複合身分數量減少到低於顯示的限制以解決此問題。

### 指定的圖表型別無效

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

此錯誤訊息會在以下情況下顯示： `graph-type` 請求路徑中的查詢引數指定了無效值。 請參閱以下小節： [身分圖表](./home.md) 在 [!DNL Identity Service] 概觀以瞭解支援的圖表型別。

### 服務權杖沒有有效的範圍

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

當您的組織尚未布建適當的許可權時，此錯誤訊息便會顯示 [!DNL Identity Service]. 請聯絡您的系統管理員以解決此問題。

### 閘道服務權杖無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

發生此錯誤時，您的存取Token無效。 存取權杖每24小時過期一次，且必須重新產生才能繼續使用 [!DNL Platform] API。 請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以取得有關產生新存取Token的說明。

### 授權服務權杖無效

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

發生此錯誤時，您的存取Token無效。 存取權杖每24小時過期一次，且必須重新產生才能繼續使用 [!DNL Platform] API。 請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以取得有關產生新存取Token的說明。

### 使用者權杖沒有有效的產品內容

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

尚未從「 」產生存取權杖時，此錯誤訊息便會顯示。 [!DNL Experience Platform] 整合。 請參閱 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以取得為使用者產生新存取權杖的說明。 [!DNL Experience Platform] 整合。

### 從身分和名稱空間程式碼取得原生XID時發生內部錯誤

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

時間 [!DNL Identity Service] 會儲存身分，身分的ID和關聯的名稱空間ID會指派一個稱為XID的唯一識別碼。 在尋找指定ID值和名稱空間的XID過程中發生錯誤時，會顯示此訊息。

### IMS組織未布建給 [!DNL Identity Service] 使用狀況

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

當您的組織尚未布建適當的許可權時，此錯誤訊息便會顯示 [!DNL Identity Service]. 請聯絡您的系統管理員以解決此問題。

### 內部伺服器錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

當執行時發生非預期的例外狀況時，就會顯示此錯誤 [!DNL Platform] 維修電話。 最佳實務是在收到此錯誤時，設定您的自動呼叫程式，以某個計時間隔重試其要求。 如果問題仍然存在，請聯絡您的系統管理員。

## 批次擷取錯誤代碼

[!DNL Identity Service] 從記錄中擷取身分資料，並將時間序列資料上傳至 [!DNL Platform] 使用批次擷取。 由於批次擷取是非同步流程，因此您必須檢視批次的詳細資料才能檢視錯誤。 錯誤會隨著批次進行而累積，直到批次完成。

以下是與相關的錯誤訊息清單 [!DNL Identity Service] 您在使用時可能會遇到 [批次擷取API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### 未知的XDM結構描述

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] 僅會使用符合「 」之記錄或時間序列資料的身分 [!DNL Profile] 或 [!DNL ExperienceEvent] 類別。 嘗試擷取以下專案的資料： [!DNL Identity Service] 不符合任一類別的動作都會觸發此錯誤。

### 已處理批次的前100列中有0個有效身分

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

當批次的前100列未顯示任何身分時，會顯示此錯誤。 不過，此錯誤並未明確表示在後續記錄中找不到身分。

### 已略過記錄，因為每個XDM記錄只有1個身分

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] 僅當單一記錄存在兩個或多個身分值時，才會連結身分。 此錯誤訊息會針對每個擷取的批次出現一次，並顯示僅能找到一個身分且不會導致身分圖表發生任何變更的記錄數量。

### 此IMS組織未註冊名稱空間程式碼

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

當擷取的記錄呈現的身分關聯名稱空間不存在或您的組織無法存取時，會顯示此錯誤。

### 正在略過批次內嵌，因為未針對私人身分圖表布建IMS組織

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

擷取批次資料時，如果您的組織尚未布建適當的許可權，系統會顯示此錯誤訊息。 [!DNL Identity Service]. 請聯絡您的系統管理員以解決此問題。

### 內部錯誤

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

當批次擷取期間發生非預期的例外狀況時，會顯示此錯誤。 最佳實務是在收到此錯誤時，設定您的自動呼叫程式，以某個計時間隔重試其要求。 如果問題仍然存在，請聯絡您的系統管理員。
