---
description: 使用 [!UICONTROL 設定檔擴充] 儀表板以瞭解設定檔擴充工作是否成功執行並完成，並檢視基本量度以評估擴充的成效。
solution: Experience Platform
title: 監視設定檔擴充工作
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# 在UI中監視設定檔擴充工作 {#monitor-profile-enrichment}

使用 [!UICONTROL 設定檔擴充] 儀表板以瞭解設定檔擴充工作是否成功執行並完成，並檢視基本量度以評估擴充的成效。

在 [平台UI](https://platform.adobe.com)，選取 **[!UICONTROL 監視]** 從左側導覽存取 [!UICONTROL 監視] 儀表板。 在檢視選擇器中，選取 **B2B流量** 若要檢視特定的儀表板元素 [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  此 [!UICONTROL 監視] 控制面板包含最近一次成功執行的基本量度，以及過去90天內的每日工作狀態。

## 相關帳戶設定檔擴充 {#related-accounts}

此 [!UICONTROL 相關帳戶] 控制面板顯示基本量度，以及特定每日工作的狀態。 [相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) 設定檔擴充。

![如何前往Experience PlatformUI中設定檔擴充工作監控畫面的視覺指示。](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

中的資料 **[!UICONTROL 量度]** 卡片包含最近成功執行「相關帳戶」作業的基本量度。

相關帳戶設定檔擴充工作可使用下列量度：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL 帳戶設定檔總數]** | 表示您的組織有權存取的帳戶設定檔總數。 |
| **[!UICONTROL 帳戶群組]** | 表示相關帳戶機器學習工作所叢集的帳戶群組數目。 |
| **[!UICONTROL 單一帳戶群組]** | 指示未與其他帳戶一起分組的帳戶數目。 |
| **[!UICONTROL 最大群組大小]** | 指示最大相關帳戶群組的大小。 允許的群組大小上限為30。 |
| **[!UICONTROL 群組大小中位數]** | 表示組織中相關帳戶群組的大小中位數。 |
| **[!UICONTROL 上次成功執行]** | 指示上次成功執行相關帳戶工作的日期和時間。 |
| **[!UICONTROL 状态]** | 指出相關帳戶工作的狀態（成功、失敗或處理）。 |
| **[!UICONTROL 消息]** | 表示特定工作執行的錯誤或警告訊息。 |

## 銷售線索與帳戶比對設定檔擴充 {#lead-to-account-matching}

此 [!UICONTROL 銷售線索與帳戶的比對] 儀表板顯示的基本量度和特定於的每日工作執行狀態 [銷售線索與帳戶的比對](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) 設定檔擴充。

![銷售線索與帳戶比對設定檔擴充](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

下列量度可用於銷售線索與帳戶比對設定檔擴充工作：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL 擁有帳戶的人員總數]** | 表示與帳戶相關聯的總人數。 |
| **[!UICONTROL 帳戶總數]** | 表示帳戶總數。 |
| **[!UICONTROL 具有帳戶的現有人員]** | 表示已與來自資料來源的帳戶相關聯的人數。 |
| **[!UICONTROL 相符的人員]** | 指出符合帳戶的人員數量。 |
| **[!UICONTROL 不相符的人員]** | 表示不符合帳戶的人員數量。 |
| **[!UICONTROL 上次成功執行]** | 表示上次成功銷售線索與帳戶相符工作執行的日期和時間。 |
| **[!UICONTROL 状态]** | 指出銷售機會與帳戶比對工作的狀態（成功、失敗或正在處理）。 |

## 預測性銷售線索和帳戶評分設定檔擴充 {#predictive-lead-to-account-scoring}

此 [!UICONTROL 預測性銷售線索和帳戶評分] 儀表板顯示的基本量度和特定於的每日工作執行狀態 [預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) 設定檔擴充。

![預測性銷售線索和帳戶評分設定檔擴充](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

預測性銷售線索與帳戶評分設定檔擴充工作可使用下列量度：

| 量度 | 描述 |
| --------- | ---------- |
| **[!UICONTROL 工作開始]** | 表示預測性銷售線索和帳戶評分工作執行的開始日期和時間。 |
| **[!UICONTROL 处理时间]** | 完成工作所花費的總時間。 |
| **[!UICONTROL 分數名稱]** | 工作的分數名稱。 |
| **[!UICONTROL 設定檔型別]** | 分數型別： <ul><li>人员</li><li>帐户</li></ul>。 |
| **[!UICONTROL 工作型別]** | 工作的型別：<ul><li>評分</li><li>培训</li>。 |
| **[!UICONTROL 状态]** | 表示預測性銷售線索和帳戶評分工作的狀態（成功、失敗或處理）。 |

## UI控制項 {#ui-controls}

本節說明監督介面中的各種使用者介面(UI)選項，這些選項可讓您篩選頁面上顯示的測量結果。

使用箭頭圖示(![箭頭圖示](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))以展開或關閉畫面頂端的卡片，卡片會顯示設定檔擴充工作的相關快速資訊。

![顯示箭頭圖示UI控制項的熒幕錄製。](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

使用 **[!UICONTROL 度量和圖表]** 切換即可關閉顯示最新量度的檢視。

![顯示度量和圖形切換的熒幕錄製。](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

使用 **[!UICONTROL 僅顯示失敗]** 切換為僅顯示失敗的設定檔擴充工作。

![熒幕錄製：顯示「僅顯示失敗」切換按鈕。](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## 后续步骤 {#next-steps}

依照本教學課程，您現在可以成功監控和瞭解設定檔擴充工作的量度。 如需更多詳細資訊，請參閱下列檔案：

* [Real-Time CDP B2B中的相關帳戶](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [帳戶設定檔UI指南中的相關帳戶標籤](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Real-Time CDP B2B中的銷售機會帳戶比對](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Real-Time CDP B2B中的預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
