---
keywords: 資料控管rtcdp；rtcdp資料控管；即時客戶資料設定檔資料控管
title: 資料控管概觀
description: 資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 3%

---

# Real-Time CDP中的資料控管

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)將來自多個企業系統的資料彙集在一起，讓行銷人員更能識別、瞭解客戶，並與客戶互動。 贵组织或法律法规可能会对此数据设置使用限制。因此，在處理您的資料時，請務必確保Real-Time CDP符合使用原則。

Adobe Experience Platform資料控管可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。 它在Real-Time CDP中起著關鍵作用，可讓您定義使用原則、根據這些原則將資料分類，以及在執行某些行銷動作時檢查原則違規。

Real-Time CDP是以Adobe Experience Platform為基礎所打造，因此，大多數資料控管功能都涵蓋在 [!DNL Experience Platform] 說明檔案。 本檔案旨在補充 [資料控管概觀](../../data-governance/home.md) 的 [!DNL Experience Platform]，並概述Real-Time CDP中可用的控管功能。 涵盖以下主题：

* [將使用標籤套用至您的資料](#labels)
* [管理資料使用原則](#policies)
* [強制執行資料使用規範](#enforce)

## 將使用標籤套用至您的資料 {#labels}

資料控管可讓您在資料集或資料集欄位層級，將使用標籤套用至您的資料。 資料使用標籤可讓您根據套用至該資料的使用原則來分類資料。

如需有關使用資料使用標籤的詳細資訊，請參閱 [資料使用標籤使用手冊](../../data-governance/labels/overview.md) 適用於Adobe Experience Platform。

## 設定目的地的行銷動作 {#destinations}

您可以定義目的地的行銷動作（也稱為行銷使用案例），以設定目的地的資料使用限制。 目的地的行銷動作會指出匯出至該目的地的資料意圖。

>[!NOTE]
>
>如需行銷動作及其在資料使用原則中之使用的詳細資訊，請參閱 [資料使用原則概觀](../../data-governance/policies/overview.md) 在 [!DNL Experience Platform] 說明檔案。

在目的地上定義行銷動作可讓您確保傳送至這些目的地的任何設定檔或區段都符合資料使用原則。 因此，您應該根據貴組織強制執行啟用原則限制的需求，將適當的行銷動作新增至目的地。

行銷動作只能在第一次設定目的地時選取。 根據您使用的目的地型別，設定行銷動作的機會將顯示在設定工作流程的不同時間點。 請參閱 [目的地檔案](../destinations/overview.md) 瞭解如何設定特定目的地的步驟。

## 管理資料使用原則 {#policies}

為了使資料使用標籤有效地支援資料合規性，必須定義並啟用資料使用原則。 資料使用原則是描述允許或限制您在Real-Time CDP中對資料執行的行銷動作型別的規則。 請參閱以下主題中的「資料使用原則」一節： [!DNL Experience Platform] [資料控管概觀](../../data-governance/home.md) 以取得詳細資訊。

Adobe Experience Platform為常見客戶體驗使用案例提供數個核心原則。 您可以導覽至「 」，在UI中檢視這些原則 **[!UICONTROL 原則]** 工作區並選取 **[!UICONTROL 瀏覽]** 標籤。 請參閱 [原則使用手冊](../../data-governance/policies/user-guide.md) 在 [!DNL Experience Platform] 說明檔案，以取得在UI中使用原則的更詳細步驟，包括如何建立自己的自訂原則。

## 強制執行資料使用規範 {#enforce}

標籤資料並定義使用原則後，您就可以強制資料使用符合原則。 在Real-Time CDP中將受眾區段啟用至目的地時，資料控管會在任何違規發生時自動強制執行使用原則。

檢視檔案： [自動原則執行](../../data-governance/enforcement/auto-enforcement.md) 以取得詳細資訊。

## 后续步骤

現在您已經瞭解Real-Time CDP上的重要資料控管功能，以及如何 [!DNL Experience Platform] 會啟用這些功能，請繼續瀏覽 [Adobe Experience Platform上的資料控管檔案](../../data-governance/home.md). 本檔案提供基本資料控管概念的概觀，以及管理資料使用標籤和原則的逐步工作流程。

以下影片提供Real-Time CDP中資料控管的概觀，包括在目的地使用行銷使用案例，以及不同案例的範例工作流程：

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
