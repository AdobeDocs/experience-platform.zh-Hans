---
solution: Experience Platform
title: 下載Experience Platform儀表板以PDF
type: Documentation
description: 使用Experience PlatformUI中提供的下載至PDF功能儲存控制面板視覺效果的副本。
exl-id: 838e98a0-ce2e-4dcd-8c8f-d28ef2cb8315
source-git-commit: 5d9428c4323e65c2605fd116160e160af7d9086d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 下載儀表板以PDF

Adobe Experience Platform中的儀表板可從Platform使用者介面下載為PDF，以促進與組織成員共用資訊。

本檔案摘要說明如何使用Platform UI下載儀表板，以及使用預設瀏覽器列印選單將儀表板儲存為PDF。

>[!WARNING]
>
>儀表板中包含的資料可能包括關於您的客戶的個人識別資訊(PII)，或與您的組織相關的敏感資料。 任何儲存至PDF的儀表板資料都應根據貴組織的資料隱私權准則進行適當處理。

## 下載儀表板

若要開始下載控制面板，請導覽至您要下載的控制面板(例如， [!UICONTROL 設定檔] 控制面板)，然後選取更多選項功能表(**`...`**)。 接下來，選取 **[!UICONTROL 下載]**.

![反白顯示省略符號和下載下拉式清單的「Experience Platform設定檔」控制面板。](images/download/download-button.png)

## 預覽PDF

選取後 **[!UICONTROL 下載]**，即會開啟瀏覽器的預設列印功能表。 在此範例中，顯示Google Chrome列印功能表。

列印功能表可讓您預覽要儲存的PDF。 PDF是儀表板Widget在Platform UI中出現的真實表示方式，PDF大小會自動調整，以便在單一頁面上顯示所有目前可見的儀表板Widget。

![「設定檔概述」會以單頁格式顯示，而「列印選項」面板則位於右側。](images/download/download-chrome-print.png)

PDF包括自動產生的標頭，其中包含Experience Platform標誌、控制面板名稱、您的名稱以及下載控制面板的日期和時間。 此資訊是唯讀的，無法在PDF中編輯。

![反白顯示自動產生標頭的列印預覽特寫。](images/download/download-pdf.png)

## 另存為PDF

預覽PDF後，選取 **儲存** 以選擇要儲存PDF的位置。

>[!NOTE]
>
>如有需要，您可以使用 **目的地** 要選取的下拉式清單 **另存為PDF** 如果未自動為您選取該選項。

![「設定檔概述」會顯示在單頁格式上，而「目的地」下拉式清單中的「另存為PDF」列印選項會反白顯示。](images/download/download-chrome-print-destination.png)

## 自訂儀表板PDF

產生的PDF會符合您在UI中看到的儀表板，並僅包含目前顯示在儀表板上的Widget。 可以自訂某些儀表板，以變更Widget的大小和位置，或從檢視中新增和移除Widget。 在Platform UI中自訂控制面板的外觀也會變更所產生PDF的外觀。

例如，您可以修改設定檔控制面板的外觀，加入數個棧疊在三個標準Widget上方的全寬度Widget。

![「設定檔」儀表板會顯示延伸的Widget。](images/download/download-modify.png)

選取以下載更新的儀表板會導致新的PDF預覽，符合自訂設定檔儀表板的外觀。 它也會自動調整PDF的大小，以確保所有可見的Widget都包含在單頁PDF中。

![「設定檔概述」會以單頁格式顯示，而「列印選項」面板則位於右側。](images/download/download-chrome-print-modified.png)

若要進一步瞭解自訂儀表板，請先閱讀 [儀表板自訂概觀](customize/overview.md).

## 后续步骤

現在您已下載儀表板並將其儲存為PDF，您可以重複這些步驟以下載其他儀表板或與您組織的成員共用PDF。
