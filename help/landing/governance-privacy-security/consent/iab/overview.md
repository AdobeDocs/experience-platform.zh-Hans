---
keywords: Experience Platform；首頁；IAB；IAB 2.0；同意；同意
solution: Experience Platform
title: Experience Platform中的IAB TCF 2.0支援
description: 瞭解如何設定資料作業和結構描述，以在對Adobe Experience Platform中的目的地啟用區段時傳達客戶同意選擇。
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 1%

---

# Experience Platform中的IAB TCF 2.0支援

此 [!DNL Transparency & Consent Framework] (TCF)，如 [!DNL Interactive Advertising Bureau] (IAB)是開放標準的技術架構，旨在讓組織能夠取得、記錄及更新消費者同意，以便依照歐盟的 [!DNL General Data Protection Regulation] (GDPR)。 此架構的第二個版本TCF 2.0為消費者提供或拒絕同意的方式提供更大的彈性，包括廠商是否及如何使用特定資料處理功能，例如精確的地理位置。

>[!NOTE]
>
>有關TCF 2.0的更多資訊可在以下網址找到： [IAB歐洲網站](https://iabeurope.eu/tcf-2-0/)，包括支援資料和技術規格。

Adobe Experience Platform隸屬於已註冊的 [IAB TCF 2.0廠商清單](https://iabeurope.eu/vendor-list-tcf-v2-0/)，位於ID下 **565**. 為符合TCF 2.0的要求，Platform可讓您收集客戶同意資料，並將其整合至您儲存的客戶設定檔中。 之後，可根據設定檔的使用案例，將此同意資料納入是否包含於匯出的受眾區段中。

>[!IMPORTANT]
>
>Platform只能符合2.0版（或更新版本）的TCF。 不支援舊版TCF。

本檔案概述如何設定您的資料作業和設定檔結構描述以接受CMP產生的客戶同意資料，以及Platform在匯出區段時如何傳達使用者同意選擇。

## 先决条件

為了遵循本指南，您必須使用與IAB TCF整合且相容的商業或您自己的同意管理平台(CMP)。 請參閱 [符合規範的CMP清單](https://iabeurope.eu/cmp-list/) 以取得詳細資訊。

>[!IMPORTANT]
>
>如果CMP的ID無效，Platform會繼續依原樣處理您的資料。 若要強制執行TCF 2.0，您必須先確認您的CMP具備已向IAB TCF 2.0註冊的有效ID，才能將資料傳送至Platform。

本指南也需要深入瞭解下列Platform服務：

* [體驗資料模型(XDM)](../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md)：透過跨裝置和系統橋接身分，解決客戶體驗資料分散所造成的根本挑戰。
* [即時客戶個人檔案](../../../../profile/home.md)：利用 [!DNL Identity Service] 以即時從資料集建立詳細的客戶設定檔。 [!DNL Real-Time Customer Profile] 從Data Lake提取資料，並將客戶設定檔儲存在其自己的獨立資料存放區中。
* [Adobe Experience Platform Web SDK](../../../../edge/home.md)：使用者端JavaScript程式庫，可讓您將各種Platform服務整合到您面向客戶的網站上。
   * [SDK同意命令](../../../../edge/consent/supporting-consent.md)：本指南中顯示的同意相關SDK命令的使用案例概觀。
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md)：可讓您除 [!DNL Real-Time Customer Profile] 將資料分到具有相同類似特徵且對行銷策略有類似回應的一組個人中。

除了上述Platform服務以外，您也應該熟悉 [目的地](../../../../data-governance/home.md) 以及他們在Platform生態系統中的角色。

## 客戶同意流程摘要 {#summary}

以下各節說明在系統正確設定後，如何收集及執行同意資料。

### 同意資料收集

Platform可讓您透過下列程式收集客戶同意資料：

1. 客戶透過您網站上的對話方塊提供其資料收集的同意偏好設定。
1. 您的CMP會偵測同意偏好設定變更，並據此產生TCF同意資料。
1. 使用Platform Web SDK時，產生的同意資料（由CMP傳回）會傳送至Adobe Experience Platform。
1. 收集的同意資料會擷取至 [!DNL Profile]其結構描述包含TCF同意欄位的已啟用資料集。

Experience Platform除了CMP同意變更掛接所觸發的SDK命令外，同意資料也可以透過任何客戶產生的XDM資料(直接上傳至 [!DNL Profile] — 啟用的資料集。

Adobe Audience Manager與Platform共用的任何區段(透過 [!DNL Audience Manager] 來源聯結器或其他方式)可能也包含同意資料，但前提是已透過將適當的欄位套用至這些區段 [!DNL Experience Cloud Identity Service]. 如需有關在中收集同意資料的詳細資訊 [!DNL Audience Manager]，請參閱檔案： [適用於IAB TCF的Adobe Audience Manager外掛程式](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hans).

### 下游同意執行

成功擷取TCF同意資料後，下游Platform服務中將進行下列程式：

1. [!DNL Real-Time Customer Profile] 會更新該客戶設定檔的已儲存同意資料。
1. 只有在為叢集中的每個ID提供Platform (565)的廠商許可權時，Platform才會處理客戶ID。
1. 將區段匯出至屬於TCF 2.0廠商清單成員的目的地時，Platform僅會包含兩個平台的廠商許可權設定檔(565) *和* 叢集中的每個ID都會提供個別目的地。

本檔案的其餘章節提供如何設定Platform和您的資料作業，以符合上述收集和執行要求的指引。

## 決定如何在CMP內產生客戶同意資料 {#consent-data}

由於每個CMP系統都是唯一的，因此您必須決定讓客戶在與您的服務互動時提供同意的最佳方式。 達成此目標的常見方法是使用Cookie同意對話方塊，類似下列範例：

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

此對話方塊必須允許客戶選擇加入或退出下列專案：

| 同意選項 | 描述 |
| --- | --- |
| **用途** | 用途定義品牌可將客戶資料用於哪些廣告技術用途。 為了讓Platform處理客戶ID，您必須選擇下列用途： <ul><li>**用途1**：儲存和/或存取裝置上的資訊</li><li>**用途10**：開發和改善產品</li></ul> |
| **供應商許可權** | 除了廣告技術目的之外，此對話方塊也必須允許客戶選擇加入或退出讓特定廠商使用其資料，包括Adobe Experience Platform (565)。 |

### 同意字串 {#consent-strings}

無論您使用何種方法收集資料，目的都是根據客戶選擇的同意選項產生字串值，稱為同意字串。

在TCF規格中，同意字串是用來根據政策和廠商定義的特定行銷目的，編碼有關客戶同意設定的相關細節。 Platform會利用這些字串來儲存每個客戶的同意設定，因此每當這些設定變更時，都必須產生新的同意字串。

同意字串只能由已向IAB TCF註冊的CMP建立。 有關如何使用特定CMP產生同意字串的詳細資訊，請參閱 [同意字串格式設定指南](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) IAB TCF GitHub存放庫中。

## 使用TCF同意欄位建立資料集 {#datasets}

客戶同意資料必須傳送至其結構描述包含TCF同意欄位的資料集。 請參閱以下教學課程： [建立資料集以擷取TCF 2.0同意](./dataset.md) 瞭解如何建立必要的設定檔資料集（以及選用的Experience Event資料集），然後再繼續閱讀本指南。

## 更新 [!DNL Profile] 合併原則以包含同意資料 {#merge-policies}

一旦您建立 [!DNL Profile] — 已啟用用於收集同意資料的資料集，您必須確保合併原則已設定為一律在客戶設定檔中包含TCF同意欄位。 這涉及設定資料集優先順序，讓您的同意資料集優先於其他可能衝突的資料集。

有關如何使用合併原則的更多資訊，請參閱 [合併原則概觀](../../../../profile/merge-policies/overview.md). 設定合併原則時，您必須確保區段包含 [XDM隱私權結構描述欄位群組](./dataset.md#privacy-field-group)，如資料集準備指南中所述。

## 整合Experience PlatformWeb SDK以收集客戶同意資料 {#sdk}

>[!NOTE]
>
>您必須使用Experience PlatformWeb SDK，才能直接在Adobe Experience Platform中處理同意資料。 [!DNL Experience Cloud Identity Service] 目前不支援。
>
>[!DNL Experience Cloud Identity Service] 不過，Adobe Audience Manager中的同意處理仍受支援，而且符合TCF 2.0只需要將程式庫更新為 [5.0版](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

將CMP設定為產生同意字串後，您必須整合Experience PlatformWeb SDK以收集這些字串並將其傳送至Platform。 Platform SDK提供兩個命令，可用來將TCF同意資料傳送至Platform （以下小節中說明），且應在客戶首次提供同意資訊時，以及之後同意變更的任何時間使用。

**SDK不會與任何立即可用的CMP進行介面**. 您可以自行決定如何將SDK整合至您的網站、接聽CMP中的同意變更，以及呼叫適當的命令。

### 建立新的資料串流

為了讓SDK將資料傳送至Experience Platform，您必須先為Platform建立新的資料流。 有關如何建立新資料流的特定步驟，請參閱 [SDK檔案](../../../../edge/datastreams/overview.md).

為資料流提供唯一名稱后，選取「 」旁的切換按鈕 **[!UICONTROL Adobe Experience Platform]**. 接下來，使用下列值完成表單的其餘部分：

| 資料流欄位 | 值 |
| --- | --- |
| [!UICONTROL 沙盒] | 平台名稱 [沙箱](../../../../sandboxes/home.md) 包含設定資料流所需的串流連線和資料集。 |
| [!UICONTROL 串流入口] | Experience Platform的有效串流連線。 請參閱教學課程，位置如下： [建立串流連線](../../../../ingestion/tutorials/create-streaming-connection-ui.md) 如果您沒有現有的串流入口。 |
| [!UICONTROL 事件資料集] | 選取 [!DNL XDM ExperienceEvent] 資料集建立於 [上一步](#datasets). 若您包含 [[!UICONTROL IAB TCF 2.0同意] 欄位群組](../../../../xdm/field-groups/event/iab.md) 在此資料集的結構描述中，您可以使用 [`sendEvent`](#sendEvent) 命令，將該資料儲存在此資料集中。 請記住，儲存在此資料集中的同意值為 **not** 用於自動執行工作流程。 |
| [!UICONTROL 設定檔資料集] | 選取 [!DNL XDM Individual Profile] 資料集建立於 [上一步](#datasets). 使用回應CMP同意變更掛接時 [`setConsent`](#setConsent) 命令，收集的資料將會儲存在此資料集中。 由於此資料集已啟用設定檔，在自動執行工作流程期間，會遵循儲存在此資料集中的同意值。 |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

完成後，選取 **[!UICONTROL 儲存]** 在熒幕底部，並依照任何其他提示繼續完成設定。

### 發出同意變更命令

建立上節所述的資料流後，您就可以開始使用SDK命令將同意資料傳送至Platform。 以下各節提供如何在不同情境中使用每個SDK命令的範例。

>[!NOTE]
>
>如需所有Platform SDK命令通用語法的簡介，請參閱以下檔案： [正在執行命令](../../../../edge/fundamentals/executing-commands.md).

#### 使用CMP同意變更掛接 {#setConsent}

許多CMP提供立即可用的鉤點，可監聽同意變更事件。 當這些事件發生時，您可以使用 `setConsent` 命令以更新該客戶的同意資料。

此 `setConsent` command需要兩個引數：(1)指出命令型別的字串（在此例中為「setConsent」），以及(2)包含 `consent` 陣列，其中必須至少包含一個提供必要同意欄位的物件，如下所示：

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| 裝載屬性 | 描述 |
| --- | --- |
| `standard` | 使用的同意標準。 此值必須設定為 `IAB` 用於TCF 2.0同意處理。 |
| `version` | 下方所示的同意標準版本號碼 `standard`. 此值必須設定為 `2.0` 用於TCF 2.0同意處理。 |
| `value` | CMP產生的base-64編碼同意字串。 |
| `gdprApplies` | 布林值，指出GDPR是否適用於目前登入的客戶。 若要針對此客戶強制執行TCF 2.0，值必須設為 `true`. 預設為 `true` 若未定義。 |

此 `setConsent` 命令應該用作CMP掛接的一部分，以偵測同意設定中的變更。 以下JavaScript提供範例，說明 `setConsent` 命令可用於OneTrust的 `OnConsentChanged` 鉤點：

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### 使用事件 {#sendEvent}

您也可以使用，針對Platform中觸發的每個事件，收集TCF 2.0同意資料 `sendEvent` 命令。

>[!NOTE]
>
>若要使用此方法，您必須已將「體驗事件隱私權」欄位群組新增至 [!DNL Profile] — 啟用 [!DNL XDM ExperienceEvent] 結構描述。 請參閱以下小節： [更新ExperienceEvent結構](./dataset.md#event-schema) 資料集準備指南中的，瞭解設定步驟。

此 `sendEvent` 命令應該當做回呼用於網站上適當的事件接聽程式。 命令需要兩個引數：(1)字串，用來指示命令型別(在此案例中， `sendEvent`)和(2)包含 `xdm` 以JSON形式提供必要同意欄位的物件：

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| 裝載屬性 | 描述 |
| --- | --- |
| `xdm.consentStrings` | 一個陣列，其中必須至少包含一個提供必要同意欄位的物件。 |
| `consentStandard` | 使用的同意標準。 此值必須設定為 `IAB` 用於TCF 2.0同意處理。 |
| `consentStandardVersion` | 下方所示的同意標準版本號碼 `standard`. 此值必須設定為 `2.0` 用於TCF 2.0同意處理。 |
| `consentStringValue` | CMP產生的base-64編碼同意字串。 |
| `gdprApplies` | 布林值，指出GDPR是否適用於目前登入的客戶。 若要針對此客戶強制執行TCF 2.0，值必須設為 `true`. 預設為 `true` 若未定義。 |

### 處理SDK回應

全部 [!DNL Platform SDK] 命令會傳回promise ，指出呼叫成功或失敗。 然後，您可以將這些回應用於其他邏輯，例如向客戶顯示確認訊息。 請參閱以下小節： [處理成功或失敗](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) 請參閱執行SDK命令指南中的特定範例。

## 匯出區段 {#export}

>[!NOTE]
>
>開始匯出區段之前，您必須確保區段包含所有必要的同意欄位。 請參閱以下小節： [設定合併原則](#merge-policies) 以取得詳細資訊。

收集客戶同意資料並建立包含所需同意屬性的受眾區段後，您就可以接著在將這些區段匯出至下游目的地時強制執行TCF 2.0合規性。

前提是同意設定 `gdprApplies` 設為 `true` 對於一組客戶設定檔，會根據每個設定檔的TCF同意偏好設定，篩選從這些設定檔匯出到下游目的地的任何資料。 匯出程式會略過不符合必要同意偏好設定的任何設定檔。

客戶必須同意以下目的(如概述 [TCF 2.0原則](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions))，以便將其設定檔包含在匯出至目的地的區段中：

* **用途1**：儲存和/或存取裝置上的資訊
* **用途10**：開發和改善產品

TCF 2.0也要求資料來源必須先檢查目的地的廠商許可權，才能將資料傳送至該目的地。 因此，在包含繫結至該目的地的資料之前，Platform會先檢查是否針對叢集中的所有ID選擇加入目的地的廠商許可權。

>[!NOTE]
>
>與Adobe Audience Manager共用的任何區段都會包含與其Platform對應專案相同的TCF 2.0同意值。 從 [!DNL Audience Manager] 與Platform (565)共用相同的廠商ID，需要相同的用途和廠商許可權。 請參閱檔案： [適用於IAB TCF的Adobe Audience Manager外掛程式](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=zh-Hans) 以取得詳細資訊。

## 測試您的實作 {#test-implementation}

設定TCF 2.0實作並將區段匯出至目的地後，不符合約意要求的任何資料都不會匯出。 不過，為了檢視匯出期間是否篩選了正確的客戶設定檔，您必須手動檢查目的地上的資料存放區，以檢視是否正確執行同意。

請務必注意，如果叢集由多個ID組成，且TCF 2.0適用，則即使單一ID不包含正確的用途和廠商許可權，也會排除整個叢集。

## 后续步骤

本檔案說明如何設定Platform資料作業，以履行TCF 2.0所列的商業義務。請參閱以下文章的概觀： [治理、隱私和安全性](../../overview.md) 以進一步瞭解Platform的隱私權相關功能。
