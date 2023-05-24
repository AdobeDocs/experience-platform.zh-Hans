---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp；XDM圖形
title: Platform的一般協助工具功能
type: Documentation
description: 進一步瞭解Adobe Experience Platform支援的一般協助工具功能，包括鍵盤導覽、調色盤和對比以及輔助技術支援。
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# Experience Platform中的協助工具功能

Adobe Experience Platform致力為所有個人提供無障礙和包容的功能，包括使用語音辨識軟體和熒幕閱讀器等輔助裝置的使用者。 本檔案概述Platform支援的一般協助工具功能，包括鍵盤導覽、語意結構、前景元素和背景元素之間的充分對比，以及對輔助技術的支援。

## 輔助技術

殘障使用者經常依賴軟硬體（稱為輔助技術）來存取數位內容和使用軟體產品。 Adobe Experience Platform透過遵循協助工具最佳實務（如使用語意代碼、對等文字、標籤和在需要時使用ARIA），支援多種型別的輔助技術(AT)，例如熒幕閱讀器、縮放和語音辨識軟體。 Experience Platform使用者介面(UI)中的互動式元素會使用對應的標籤、可存取的名稱以及可識別其用途和目前狀態的角色。 這可確保輔助技術（例如熒幕閱讀程式）可朗讀標籤和其他資訊給使用者，以便他們能夠輕鬆與應用程式控制項互動。

## 键盘辅助功能

Experience Platform致力於支援完整的鍵盤協助功能。

以下导航元素有助于促进无障碍功能：
* Tab鍵可在UI元素、區段和功能表群組之間移動。
* 箭頭鍵可在選單群組中移動，以將焦點設定為個別活動元素。
* Shift + Tab鍵會向後移動並經過Tab鍵順序。
* Return (Enter)和空白鍵會啟動選取的專案。
* 逸出索引鍵(ESC)可作為取消按鈕，在出現時關閉對話方塊。
* Experience Platform會在選取的元素周圍顯示藍色邊框，以清楚指出目前取得焦點的UI元素。

![所選元素周圍出現藍色邊框，表示已套用焦點。](images/profile-overview-tab.png)

## 调色板和对比度

Experience Platform努力爭取 [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/) 符合性，包括色彩對比的要求。 Experience PlatformUI在應用程式中提供足夠的對比功能，以確保為視力不足或色彩缺乏的使用者提供可存取的檢視體驗。

![Experience PlatformUI首頁上顯示的調色盤和對比。](images/homepage.png)

## 必要欄位驗證

新增資料、建立結構描述或定義區段時，必填欄位會以視覺化方式並以程式設計方式標示（在欄位的文字標籤旁使用星號）。 當您在欄位中輸入無效資料並儲存時，這些欄位會觸發驗證。 如果必要欄位未通過驗證，則會以紅色列出，並出現錯誤圖示，以及需要修正的問題的書面說明。

![尚未通過驗證的必要欄位的特寫。 欄位會以紅色顯示，並顯示錯誤圖示。](images/field-validation.png)
