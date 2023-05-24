---
title: 監控批次查詢授權使用情況
description: Adobe Experience Platform UI提供控制面板，讓您檢視有關貴組織Data Distiller授權使用情況的重要資訊。
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
hide: true
hidefromtoc: true
recommendations: noCatalog, display
source-git-commit: fa573dcf03eb711e946afe40d107871f5166ff58
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# (Alpha)監控批次查詢授權使用情況 {#monitor-license-usage}

>[!IMPORTANT]
>
>並非所有使用者都能透過UI監控批次查詢授權使用情況。 此功能目前處於Alpha測試階段，仍在測試中。 此檔案可能會有變動。

Adobe Experience Platform使用者介面(UI)提供了一個儀表板，您可以通過該儀表板檢視有關您組織的Query Service授權使用情況的重要資訊。

如需如何在UI中存取授權使用儀表板並與之互動的詳細指示，以及深入瞭解儀表板中顯示的可用量度，請造訪 [授權使用儀表板指南](../../dashboards/guides/license-usage.md).

請閱讀 [儀表板概觀](../../dashboards/home.md) 以取得Experience Platform中所有儀表板功能的摘要。

## Widget {#widgets}

授權使用儀表板是由Widget組成，這些介面會以唯讀方式顯示度量，提供關於您組織授權使用的重要資訊。 可見的量度取決於您組織的特定授權。

選取選項按鈕以選擇要分析的沙箱，並使用下拉式選單來選取分析的時間段。 可用的選項包括30天、90天、12個月期間、去年、完整合約期間或自訂日期。

## 計算時數 {#compute-hours}

此 [!UICONTROL 計算時數] Widget會使用線圖，以視覺效果呈現貴組織每天的批次查詢處理時間。 Widget會在Widget左上角顯示三個以數字表示的量度。 這些是

- [!UICONTROL 實際]：在概覽下拉式清單中選擇的時段的總運算時數。 此量度也會在圖形中以實線表示。
- [!UICONTROL 已授權]：貴組織的授權合約所允許的運算時數總計。 此量度也會在圖表中以虛線表示。
- [!UICONTROL 使用狀況]：這是您的使用量相對於授權所同意的最大運算時數的百分比。

>[!IMPORTANT]
>
>此 [!UICONTROL 計算時數] widget僅適用於擁有Data Distiller授權進行批次查詢的客戶。

![已反白顯示計算時數Widget的授權使用儀表板。](../images/data-distiller/compute-hours.png)

