---
keywords: Experience Platform；首頁；熱門主題；分段；區段產生器；區段產生器
solution: Experience Platform
title: 重構分段時間限制UI指南
description: 區段產生器提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供直覺式控制項來建置和編輯規則，例如用來表示資料屬性的拖放圖磚。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 時間限制重構

2020年10月發行的Adobe Experience Platform已對Adobe Experience Platform Segmentation Service進行效能變更，新增了使用OR和AND邏輯運運算元的限制。 這些變更將會影響使用區段產生器UI新建或編輯的區段。 本指南說明如何減輕這些變更。

在2020年10月版本之前，所有規則層級、群組層級和事件層級時間限制都以重複方式參考相同的時間戳記。 為了釐清時間限制的使用方式，已移除規則層級和群組層級的時間限制。 為了配合此變更，所有時間限制都必須重寫為事件層級時間限制。

過去，個別事件可以附加多個時間限制規則。

![「區段產生器」會反白顯示前一個時間限制樣式。](../images/ui/segment-refactoring/former-time-constraint.png)

如您所見，此區段在規則層級上有兩個限制：一個適用於&quot;[!UICONTROL 今天]」和另一個「[!UICONTROL 昨天]「。

前一個區段等同於以下區段 — 兩個事件層級時間限制都使用AND運運算元連線。 第一個事件層級時間限制會參考名稱等於「Training」且發生在今天的點選事件，第二個事件層級時間限制會參考名稱等於「Pets」且發生在昨天的點選事件。

![新的時間限制樣式會在「區段產生器」中反白顯示。](../images/ui/segment-refactoring/time-constraint-1.png) ![新的時間限制樣式會在「區段產生器」中反白顯示。](../images/ui/segment-refactoring/time-constraint-2.png)

這種時間限制重構也會影響使用OR運運算元連線的時間限制。
