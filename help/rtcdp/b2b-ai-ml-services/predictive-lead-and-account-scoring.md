---
title: Real-Time CDP B2B中的預測性銷售線索和帳戶評分
type: Documentation
description: 有關Experience PlatformCDP B2B中預測性銷售線索和帳戶評分功能的概述和詳細資訊。
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Real-Time CDP B2B中的預測性銷售線索和帳戶評分

B2B行銷人員在行銷漏斗頂端面臨多項挑戰。 為了有效運作，B2B行銷人員需要自動化方式來確認大量人員的資格，以便他們能專注於高價值的目標。 資格應與最終銷售結果一致，而不僅僅是行銷轉換。

帳戶是購買B2B產品和服務的最終實體。 為了有效行銷和銷售，B2B行銷人員不僅需要知道個人的購買可能性，還需要知道帳戶購買的可能性。

以帳戶為基礎的行銷尤其會將帳戶策略化為行銷目標。 帳戶購買傾向分數可大幅協助B2B行銷人員排定帳戶優先順序，以實現投資報酬的最大化。

預測性銷售線索和帳戶評分服務可透過學習和預測機會階段轉換事件，並將個人活動彙總到帳戶層級以產生帳戶分數，從而解決上述挑戰。 這些分數可立即作為個人設定檔和帳戶設定檔的自訂欄位提供，並可輕鬆作為區段條件納入，以縮小您的受眾。 彙總和單位層級也提供主要影響因素，以協助B2B行銷人員更瞭解哪些元素驅動分數。

## 瞭解預測性銷售線索和帳戶評分 {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] 資料來源目前為必要專案，因為它是唯一可在人員設定檔層級提供轉換事件的資料來源。

預測性銷售線索和帳戶評分使用樹狀結構（隨機森林/漸層提升）機器學習方法，以建立預測性銷售線索評分模型。

管理員能夠設定多個設定檔評分目標（也稱為模型），每個設定的轉換事件各一個，從而為每個設定的目標產生個別的分數。

預測性銷售線索和帳戶評分支援下列轉換目標型別和欄位：

| 目標型別 | 字段 |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>範例： `opportunityEvent.dataValueChanges.attributeName` 等於 `Stage` 和 `opportunityEvent.dataValueChanges.newValue` 等於 `Contract`</ul> |

演演算法會考量下列屬性和輸入資料：

* 個人設定檔

| XDM欄位 | 必填/可选 |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | 必需 |
| `workAddress.country` | 可选 |
| `extSourceSystemAudit.createdDate` | 必需 |
| `extendedWorkDetails.jobTitle` | 可选 |

>[!NOTE]
> 
>演演算法只會檢查 `sourceAccountKey.sourceKey` 「Person：personComponents」欄位群組中的欄位。

* 帳戶設定檔

| XDM欄位 | 必填/可选 |
| --- | --- |
| `accountKey.sourceKey` | 必需 |
| `extSourceSystemAudit.createdDate` | 必需 |
| `accountOrganization.industry` | 可选 |
| `accountOrganization.numberOfEmployees` | 可选 |
| `accountOrganization.annualRevenue.amount` | 可选 |

* 體驗事件

| XDM欄位 | 必填/可选 |
| --- | --- |
| `_id` | 必需 |
| `personKey.sourceKey` | 必需 |
| `timestamp` | 必需 |
| `eventType` | 必需 |

支援多種機型，並設定下列硬性限制：

* 每個生產沙箱有權使用五個模型。
* 每個開發沙箱都有權使用一種模型。

資料品質要求如下：

* 理想情況下，應提供兩年的最新資料供訓練使用。
* 所需的最小資料長度為六個月加上預測期間。
* 對於每個預測目標，至少需要10個合格的轉換事件。

評分工作每天都會執行，且結果會儲存為設定檔屬性和帳戶屬性，然後可用於區段定義和個人化。 現成可用的分析深入分析也可在帳戶概述控制面板上取得。

請參閱檔案，深入瞭解如何 [管理預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) 服務。

## 檢視預測性銷售線索和帳戶評分結果 {#how-to-view}

工作執行後，結果會儲存在名稱下每個模型的新系統資料集中 `LeadsAI.Scores` - ***分數名稱***. 每個分數欄位群組都位於 `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| 属性 | 描述 |
| --- | --- |
| 得分 | 設定檔在定義的時間範圍內達到預測目標的相對可能性。 此值不被視為機率百分比，而是個人資料相較於整體母體的可能性。 此分數介於0到100之間。 |
| 百分位數 | 此值提供有關設定檔相對於其他類似評分的設定檔效能的資訊。 百分位數的範圍為1到100。 |
| 模型型別 | 選取的模型型別會指出這是否為人員或帳戶分數。 |
| 評分日期 | 評分發生的日期。 |
| 影響因素 | 個人資料可能轉換的預測原因。 因子由下列屬性組成：<ul><li>程式碼：對設定檔的預測分數產生正面影響的設定檔或行為屬性。</li><li>值：設定檔或行為屬性的值。</li><li>重要性：指出設定檔或行為屬性對預測分數（低、中、高）的權重。</li></ul> |

### 檢視客戶設定檔分數

若要檢視個人檔案的預測性分數，請選取「 」 **[!UICONTROL 設定檔]** 在左側面板的「客戶」區段下方，然後輸入身分名稱空間和身分值。 完成後，選取 **[!UICONTROL 檢視]**.

接下來，從清單中選取設定檔。

![客戶設定檔](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

此 **[!UICONTROL 詳細資訊]** 頁面現在包含預測性分數。 按一下預測分數旁的圖表圖示。

![客戶設定檔預測性分數](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

快顯對話方塊會顯示分數、整體分數分佈、此分數的主要影響因素，以及分數目標定義。

![客戶設定檔預測性分數詳細資訊](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## 監控預測性銷售線索和帳戶評分工作 {#monitoring-jobs}

您可以透過控制面板監控基本量度和每日工作執行狀態。 這些量度包括：

* 已評分的個人/帳戶設定檔總數
* 下一個評分工作（日期）
* 下一個訓練工作（日期）

如需詳細資訊，請參閱以下檔案： [監控預測性銷售線索和帳戶評分的工作](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
