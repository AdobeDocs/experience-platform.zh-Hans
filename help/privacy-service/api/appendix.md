---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Privacy Service API指南附錄
description: 本檔案包含使用Privacy Service API的其他資訊。
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 5%

---

# Privacy Service API指南附錄

以下小節包含使用Adobe Experience Platform Privacy Service API的其他資訊。

## 標準身分名稱空間 {#standard-namespaces}

所有傳送至的身分 [!DNL Privacy Service] 必須在特定的身分名稱空間下提供。 身分名稱空間是的元件 [Adobe Experience Platform Identity Service](../../identity-service/home.md) 指示與身分相關的內容。

下表概述由提供的幾種常用的預先定義身分型別 [!DNL Experience Platform]，以及其相關聯的 `namespace` 值：

| 身分型別 | `namespace` | `namespaceId` |
| --- | --- | --- |
| 电子邮件 | `Email` | `6` |
| Phone | `Phone` | `7` |
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
| ADOBE AUDIENCE MANAGER UUID | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple] 廣告商ID | `IDFA` | `20915` |
| [!DNL Google] 广告 ID | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>每個身分型別也有 `namespaceId` 整數值，可用來取代 `namespace` 字串（設定身分時） `type` 屬性重新命名為「namespaceId」。 請參閱以下小節： [名稱空間限定詞](#namespace-qualifiers) 以取得詳細資訊。

您可以透過向以下網站發出GET要求，擷取貴組織正在使用的身分名稱空間清單： `idnamespace/identities` 中的端點 [!DNL Identity Service] API。 請參閱 [Identity Service開發人員指南](../../identity-service/api/getting-started.md) 以取得詳細資訊。

## 名稱空間限定詞

指定 `namespace` 中的值 [!DNL Privacy Service] API， a **名稱空間限定詞** 必須包含在相對應的 `type` 引數。 下表概述不同的接受名稱空間限定詞。

| 限定詞 | 定义 |
| --------- | ---------- |
| `standard` | 全域定義的標準名稱空間之一，不會繫結至個別組織資料集（例如電子郵件、電話號碼等）。 提供名稱空間ID。 |
| `custom` | 在組織內容中建立的唯一名稱空間，未在之間共用 [!DNL Experience Cloud]. 值代表要搜尋的易記名稱（「名稱」欄位）。 提供名稱空間ID。 |
| `integrationCode` | 整合代碼 — 類似「自訂」，但特別定義為要搜尋的資料來源的整合代碼。 提供名稱空間ID。 |
| `namespaceId` | 表示該值是通過名稱空間服務建立或對應的名稱空間的實際ID。 |
| `unregistered` | 名稱空間服務中未定義的自由格式字串，採用「原樣」處理。 處理這些型別名稱空間的任何應用程式會根據此類名稱空間進行檢查，並在適合公司內容和資料集時進行處理。 未提供名稱空間ID。 |
| `analytics` | 內部對應的自訂名稱空間，位於 [!DNL Analytics]，不在名稱空間服務中。 這會依照原始請求的指定直接傳入，不含名稱空間ID |
| `target` | 內部可瞭解的自訂名稱空間 [!DNL Target]，不在名稱空間服務中。 這會依照原始請求的指定直接傳入，不含名稱空間ID |

{style="table-layout:auto"}

## 接受的產品值

下表概述在「 」中指定Adobe產品的接受值 `include` 工作建立請求的屬性。

| 产品 | 在中使用的值 `include` 屬性 |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform （資料湖） | `aepDataLake` |
| Adobe Experience Platform （即時客戶個人檔案） | `profileService` |
| Adobe Primetime驗證 | `primetimeAuthentication` |
| Adobe Target | `target` |
| 客戶屬性(CRS) | `CRS` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |

{style="table-layout:auto"}
