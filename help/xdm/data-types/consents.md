---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；同意；同意；偏好設定；偏好設定；privacyOptOuts；marketingPreferences；optOutType；basisOfProcessing；同意；同意
title: 同意和偏好設定資料型別
description: 「隱私權同意、個人化和行銷偏好設定」資料型別旨在支援收集由同意管理平台(CMP)和資料作業的其他來源產生的客戶許可權和偏好設定。
exl-id: cdcc7b04-eeb9-40d3-b0b5-f736a5472621
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '2034'
ht-degree: 1%

---

# [!UICONTROL 同意和偏好設定] 資料型別

此 [!UICONTROL 隱私權、個人化和行銷偏好設定的同意] 資料型別(以下稱「 」[!UICONTROL 同意和偏好設定] data type&quot;)是 [!DNL Experience Data Model] (XDM)資料型別，旨在支援從您的資料作業收集由同意管理平台(CMP)和其他來源產生的客戶許可權和偏好設定。

本檔案說明提供的欄位結構和預期用途， [!UICONTROL 同意和偏好設定] 資料型別。

## 先决条件 {#prerequisites}

本檔案需要實際瞭解XDM以及中的結構描述使用 [!DNL Experience Platform]. 請先檢閱下列檔案，然後再繼續：

* [XDM 系统概述](https://www.adobe.com/go/xdm-home-en)
* [結構描述組合基本概念](https://www.adobe.com/go/xdm-schema-best-practices-en)

## 資料型別結構 {#structure}

>[!IMPORTANT]
>
>此 [!UICONTROL 同意和偏好設定] 資料型別旨在涵蓋一系列同意和偏好設定管理使用案例。 因此，本檔案以一般術語說明資料型別欄位的使用，並僅就您應如何解釋這些欄位的使用提供建議。 請洽詢您的隱私權法律團隊，使資料型別的結構與您的組織如何解譯及向您的客戶呈現這些同意和偏好設定選擇一致。

此 [!UICONTROL 同意和偏好設定] 資料型別提供數個用於擷取的欄位 **同意** 和 **偏好設定** 資訊。

同意是可讓客戶指定如何使用其資料的選項。 大部分的同意都有法律層面，因為某些司法管轄區會先要求取得許可，資料才能以特定方式使用，或是如果不需要肯定同意，則要求客戶可以選擇停止該使用（選擇退出）。

偏好設定是一個選項，可讓客戶指定如何處理其品牌體驗的不同方面。 這些屬於兩個類別：

* **個人化偏好設定**：有關品牌應如何個人化提供給客戶的體驗的偏好設定。
* **行銷偏好設定**：有關品牌是否獲准透過各種管道聯絡客戶的偏好設定。

下列熒幕擷圖顯示資料型別的結構在Platform UI中的呈現方式：

![](../images/data-types/consents.png)

>[!TIP]
>
>請參閱指南： [探索XDM資源](../ui/explore.md) ，以瞭解如何在Platform UI中查詢任何XDM資源及檢查其結構的步驟。

以下JSON範例說明 [!UICONTROL 同意和偏好設定] 資料型別可以處理。 以下各節將提供有關每個欄位特定用途的資訊。

```json
{
  "consents": {
    "collect": {
      "val": "VI",
    },
    "adID": {
      "idType": "IDFA",
      "val": "y"
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "u"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "metadata": {
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

>[!TIP]
>
>您可以為您在Experience Platform中定義的任何XDM結構描述產生範例JSON資料，以協助視覺化應如何對應客戶同意和偏好設定資料。 如需詳細資訊，請參閱下列檔案：
>
>* [在UI中產生範例資料](../ui/sample.md)
>* [在API中產生範例資料](../api/sample-data.md)


## `consents` {#choices}

`consents` 包含幾個說明客戶同意和偏好設定的欄位。 以下小節將更詳細地說明這些欄位。

```json
"consents": {
  "collect": {
    "val": "VI",
  },
  "adID": {
    "idType": "IDFA",
    "val": "y"
  },
  "share": {
    "val": "y",
  },
  "personalize": {
    "content": {
      "val": "y"
    }
  },
  "marketing": {
    "preferred": "email",
    "any": {
      "val": "u"
    },
    "email": {
      "val": "n",
      "reason": "Too Frequent",
      "time": "2019-01-01T15:52:25+00:00"
    }
  }
}
```

### `collect`

`collect` 代表客戶同意收集其資料。

```json
"collect": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客戶針對此使用案例提供的同意選擇。 請參閱 [附錄](#choice-values) 以取得接受的值和定義。 |

{style="table-layout:auto"}

### `adID`

`adID` 代表客戶同意是否可使用廣告商ID在此裝置上跨應用程式連結客戶。

```json
"adID": {
  "idType": "IDFA",
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `idType` | 廣告ID型別： `IDFA` 廣告商的Apple ID或 `GAID` Google (也稱為Android廣告商ID (AAID))的資訊。 |
| `val` | 客戶針對此使用案例提供的同意選擇。 請參閱 [附錄](#choice-values) 以取得接受的值和定義。 |

{style="table-layout:auto"}

### `share`

`share` 代表客戶同意其資料可與第二方或第三方共用（或賣給）的同意。

```json
"share": {
  "val": "y"
}
```

| 属性 | 描述 |
| --- | --- |
| `val` | 客戶針對此使用案例提供的同意選擇。 請參閱 [附錄](#choice-values) 以取得接受的值和定義。 |

{style="table-layout:auto"}

### `personalize` {#personalize}

`personalize` 擷取客戶對其資料個人化使用方式的偏好設定。 客戶可以選擇退出特定的個人化使用案例，或完全選擇退出個人化。

>[!IMPORTANT]
>
>`personalize` 不包含行銷使用案例。 例如，如果客戶選擇退出所有管道的個人化，他們不應停止透過這些管道接收通訊。 相反地，他們收到的訊息應該是通用的，而不是根據其設定檔。
>
>根據相同範例，如果客戶選擇退出所有頻道的直銷(透過 `marketing`，說明於 [下一節](#marketing))，則即使允許個人化，該客戶也不應收到任何訊息。

```json
"personalize": {
  "content": {
    "val": "y",
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `content` | 代表客戶對您網站或應用程式上的個人化內容的偏好設定。 |
| `val` | 客戶針對指定使用案例提供的個人化偏好設定。 如果不需要提示客戶提供同意，此欄位的值應指出進行個人化的基礎。 請參閱 [附錄](#choice-values) 以取得接受的值和定義。 |

{style="table-layout:auto"}

### `marketing` {#marketing}

`marketing` 擷取客戶對其資料可用於哪些行銷用途的偏好設定。 客戶可以選擇退出特定的行銷使用案例，或完全選擇退出直銷。

```json
"marketing": {
  "preferred": "email",
  "any": {
    "val": "u"
  },
  "email": {
    "val": "n",
    "reason": "Too Frequent"
  },
  "push": {
    "val": "y"
  },
  "sms": {
    "val": "y"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `preferred` | 表示客戶接收通訊的偏好管道。 請參閱 [附錄](#preferred-values) 以取得接受的值。 |
| `any` | 代表整體直銷的客戶偏好設定。 此欄位中提供的同意偏好設定會視為任何行銷管道的「預設」偏好設定，除非已由下提供的其他子欄位覆寫 `marketing`. 如果您打算使用更精細的同意選項，建議您排除此欄位。<br><br>如果值設定為 `n`，則應忽略所有更具體的個人化設定。 如果值設定為 `y`，則所有較精細的個人化選項也應視為 `y`，除非明確設定為 `n`. 如果值未設定，則每個個人化選項的值都應依照指定接受。 |
| `email` | 指出客戶是否同意接收電子郵件訊息。 |
| `push` | 指出客戶是否允許接收推播通知。 |
| `sms` | 指出客戶是否同意接收文字訊息。 |
| `val` | 客戶針對指定使用案例提供的偏好設定。 如果不需要提示客戶提供同意，此欄位的值應指出行銷使用案例發生的基礎。 請參閱 [附錄](#choice-values) 以取得接受的值和定義。 |
| `time` | 行銷偏好設定變更時間的ISO 8601時間戳記（如適用）。 請注意，如果任何個別偏好設定的時間戳記與下方提供的相同 `metadata`，則不會針對該偏好設定設定此欄位。 |
| `reason` | 當客戶選擇退出行銷使用案例時，此字串欄位代表客戶選擇退出的原因。 |

{style="table-layout:auto"}

### `metadata`

`metadata` 擷取有關客戶同意和偏好設定的一般中繼資料（只要上次更新）。

```json
"metadata": {
  "time": "2019-01-01T15:52:25+00:00",
}
```

| 属性 | 描述 |
| --- | --- |
| `time` | 上次更新任何客戶同意和偏好設定的ISO 8601時間戳記。 此欄位可用於取代將時間戳記套用至個別偏好設定，以減少負載和複雜性。 提供 `time` 個別偏好設定下的值會覆寫 `metadata` 該特定偏好設定的時間戳記。 |

{style="table-layout:auto"}

## 使用資料型別擷取資料 {#ingest}

為了使用 [!UICONTROL 同意和偏好設定] 資料型別若要從客戶擷取同意資料，您必須根據包含該資料型別的結構描述建立資料集。

請參閱教學課程，位置如下： [在UI中建立結構描述](https://www.adobe.com/go/xdm-schema-editor-tutorial-en) 有關如何將資料型別指派給欄位的步驟。 建立包含欄位的結構描述後，使用 [!UICONTROL 同意和偏好設定] 資料型別，請參閱 [建立資料集](../../catalog/datasets/user-guide.md#create) 在資料集使用手冊中，依照使用現有結構描述建立資料集的步驟操作。

>[!IMPORTANT]
>
>如果您想要將同意資料傳送至 [!DNL Real-Time Customer Profile]，您必須建立 [!DNL Profile] — 啟用的結構描述，根據 [!DNL XDM Individual Profile] 包含 [!UICONTROL 同意和偏好設定] 資料型別。 您根據該結構描述建立的資料集也必須啟用 [!DNL Profile]. 如需瞭解相關的具體步驟，請參閱上述教學課程 [!DNL Real-Time Customer Profile] 結構描述和資料集的需求。
>
>此外，您也必須確保合併原則已設定為優先處理包含最新同意和偏好設定資料的資料集，以便客戶設定檔能夠正確更新。 請參閱以下文章的概觀： [合併原則](../../rtcdp/profile/merge-policies.md) 以取得詳細資訊。

## 處理同意和偏好設定變更

當客戶在您的網站上變更其同意或偏好設定時，應使用 [Adobe Experience Platform Web SDK](../../edge/consent/supporting-consent.md). 如果客戶選擇退出資料收集，所有資料收集必須立即停止。 如果客戶選擇退出個人化，則他們造訪的下一個頁面上應該不會出現個人化。

## 附录 {#appendix}

以下各節提供有關以下專案的其他參考資訊： [!UICONTROL 同意和偏好設定] 資料型別。

### 接受的值 `val` {#choice-values}

下表概述下列專案的可接受值 `val`：

| 值 | 标题 | 描述 |
| --- | --- | --- |
| `y` | 是（選擇加入） | 客戶已選擇加入以獲得同意或偏好設定。 換言之，他們 **do** 同意使用相關同意或偏好設定所指示的資料。 |
| `n` | 否（選擇退出） | 客戶已選擇退出同意或偏好設定。 換言之，他們 **不要** 同意使用相關同意或偏好設定所指示的資料。 |
| `p` | 擱置中的驗證 | 系統尚未收到最終同意或偏好設定值。 這通常用於需要兩步驟驗證的同意中。 例如，如果客戶選擇接收電子郵件，該同意將設為 `p` 直到他們選取電子郵件中的連結，以確認他們提供了正確的電子郵件地址，同意才會更新為 `y`.<br><br>如果此同意或偏好設定未使用兩集驗證程式，則 `p` 選擇可用於指出客戶尚未回應同意提示。 例如，您可以自動將值設為 `p` 在網站首頁，客戶尚未回應同意提示時。 在不需要明確同意的管轄區中，您也可以使用它來表示客戶尚未明確選擇退出（換句話說，假設您同意）。 |
| `u` | 未知 | 客戶的同意或偏好設定資訊不明。 |
| `dy` | 是（選擇加入）的預設值 | 客戶本身並未提供同意值，且預設會被視為選擇加入（「是」）。 換言之，在客戶另外表示同意之前，一律假定客戶同意。<br><br>請注意，如果貴公司隱私權政策的法律或變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `dn` | 「否」（選擇退出）的預設值 | 客戶本身並未提供同意值，且預設會被視為選擇退出（「否」）。 換言之，客戶被假定已拒絕同意，直到他們指出不同意。<br><br>請注意，如果貴公司隱私權政策的法律或變更導致部分或所有使用者的預設值變更，您必須手動更新包含預設值的所有設定檔。 |
| `LI` | 合法利益 | 為特定目的收集和處理此資料的合法商業利益，超過其對個人的潛在傷害。 |
| `CT` | 合約 | 為特定目的收集資料是履行與個人的合約義務所必需的。 |
| `CP` | 遵守法律義務 | 為了符合企業的法律義務，必須針對特定目的收集資料。 |
| `VI` | 個人的重大利益 | 為了保護個人切身利益，需要為特定目的收集資料。 |
| `PI` | 公共利益 | 為了公眾利益或行使官方權力，需要為特定目的收集資料。 |

{style="table-layout:auto"}

### 接受的值 `preferred` {#preferred-values}

下表概述下列專案的可接受值 `preferred`：

| 值 | 描述 |
| --- | --- |
| `email` | 电子邮件 messages. |
| `push` | 推送通知. |
| `inApp` | 应用程序内消息. |
| `sms` | 短信消息. |
| `phone` | 電話通話互動。 |
| `phyMail` | 實體郵件。 |
| `inVehicle` | 車內訊息。 |
| `inHome` | 住家內訊息。 |
| `iot` | 物聯網(IoT)訊息。 |
| `social` | 社群媒體內容。 |
| `other` | 不符合標準類別的管道。 |
| `none` | 沒有偏好的管道。 |
| `unknown` | 偏好的管道不明。 |

{style="table-layout:auto"}

### 完整 [!UICONTROL 同意和偏好設定] 綱要 {#full-schema}

若要檢視的完整結構描述 [!UICONTROL 同意和偏好設定] 資料型別，請參閱 [官方XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-preferences.schema.json).
