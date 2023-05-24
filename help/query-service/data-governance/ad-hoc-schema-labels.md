---
title: Ad Hoc結構描述的屬性式存取控制支援
description: 限制存取透過Adobe Experience Platform查詢服務產生的臨時結構描述中資料欄位的指南。
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: 91f318596bf268aa93e8b2df9c13774aab76d13a
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---

# 針對臨時結構描述的屬性型存取控制支援

任何帶入Adobe Experience Platform的資料都會由Experience Data Model (XDM)結構描述封裝，並可能會受到貴組織或法規定義的使用限制所規範。

當未指定結構描述時，透過查詢服務執行CTAS查詢，便會自動產生臨時結構描述。 通常需要限制使用特定結構描述的特定欄位或資料集，以控制對敏感個人資料和個人識別資訊的存取。 Adobe Experience Platform可讓您使用以屬性為基礎的存取控制功能，透過Platform UI標籤結構描述欄位，以協助進行此存取控制。

標籤可隨時套用，讓您靈活選擇控管資料的方式。 不過，最佳實務是在資料內嵌至Platform時，或資料可在Platform中使用時，立即加上標籤。

結構描述型標籤是以屬性為基礎的存取控制的重要元件，可更好地管理使用者或使用者群組的存取許可權。 Adobe Experience Platform可讓您透過建立和套用標籤，限制對臨時結構描述的任何欄位的存取。

本檔案提供教學課程，說明如何透過將標籤套用至透過查詢服務產生的臨時結構描述的資料欄位，以管理對敏感資料的存取。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [Experience Data Model (XDM)系統](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [[!DNL Schema Editor]](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=zh-Hans)：瞭解如何在Platform UI中建立和管理結構描述和其他資源。
* [[!DNL Data Governance]](../../data-governance/home.md)：瞭解如何 [!DNL Data Governance] 可讓您管理客戶資料，並確保遵守適用於資料使用的法規、限制和原則。
* [以屬性為基礎的存取控制](../../access-control/abac/overview.md)：以屬性為基礎的存取控制是Adobe Experience Platform的一項功能，可讓管理員根據屬性控制對特定物件和/或權能的存取。 屬性可以是新增至物件的中繼資料，例如新增至臨時或一般結構描述欄位的標籤。 管理員定義包含管理使用者存取許可權的屬性的存取原則。

## 建立臨時結構描述

執行查詢並產生結果後，就會自動產生臨時結構描述，並將其新增至結構描述詳細目錄。

若要新增資料標籤，請導覽至 [!UICONTROL 結構描述] 控制面板瀏覽標籤，方法是選取 [!UICONTROL 結構描述] （在Platform UI的左側邊欄中）。 此時會顯示結構描述詳細目錄。

>[!NOTE]
>
>依預設，臨時結構描述不會顯示在結構描述詳細目錄中。

## 探索Platform UI結構描述詳細目錄中的臨時結構描述 {#discover-ad-hoc-schemas}

若要在Platform UI中啟用臨時結構描述的顯示，請選取篩選圖示(![篩選圖示。](../images/data-governance/filter.png))，然後選取「 ** 」[!UICONTROL 顯示臨時結構描述] （在出現的左側邊欄中）。

![「結構描述」控制面板篩選選項左側邊欄的「顯示臨機結構描述」切換功能已啟用。](../images/data-governance/adhoc-schema-toggle.png)

從可用清單中選取最近建立的臨時結構描述的名稱。 隨即顯示臨機架構結構的視覺效果。

![臨時結構描述結構圖範例。](../images/data-governance/adhoc-schema-structure-diagram.png)

## 编辑治理标签

若要編輯臨機操作結構描述的資料標籤，請選取 [!UICONTROL 標籤] 標籤。 標籤工作區可讓您對臨時結構描述欄位套用、建立和編輯標籤，並透過UI控制存取許可權。 此處顯示臨時結構描述中的所有欄位。

## 編輯結構描述或欄位的標籤

若要編輯整個結構描述的標籤，請選取鉛筆圖示(![鉛筆圖示。](../images/data-governance/edit-icon.png))至結構描述名稱旁邊 [!UICONTROL 標籤] 標籤。

![標籤會在結構描述工作區中檢視，並反白顯示鉛筆圖示。](../images/data-governance/edit-entire-schema-labels.png)

若要將標籤套用至現有欄位，請從清單中選取一個或多個欄位，然後選取 [!UICONTROL 編輯治理標籤] 在右側邊欄中。

![在右側邊欄中反白顯示「編輯治理標籤」選項的結構描述工作區中的標籤檢視。](../images/data-governance/edit-governance-labels.png)

## 編輯標籤彈出視窗

此 [!UICONTROL 編輯標籤] 彈出視窗隨即顯示。 從這個檢視，您可以透過UI建立或編輯現有的治理標籤。

![編輯標籤彈出視窗。](../images/data-governance/edit-labels-popover.png)

請參閱檔案，取得以下操作的指引： [建立或編輯所選結構描述或欄位的標籤](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/labels.html#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>建立新標籤或編輯現有標籤需要您組織的管理員許可權。 如果您沒有管理員許可權，請聯絡您的系統管理員以安排存取權。

您也可以使用許可權工作區來建立標籤。 請參閱 [在許可權工作區中建立標籤指南](../../access-control/abac/ui/labels.md) 以取得指示。

套用以屬性為基礎的適當層級存取控制後，當使用者嘗試存取無法存取的資料時，以下系統行為適用於透過「查詢服務」執行的任何查詢：

1. 如果拒絕使用者存取結構描述中的其中一個欄位，使用者將無法讀取或寫入受限制的欄位。 這種情況適用於下列常見案例：

   * 當使用者嘗試執行僅具有受限欄的查詢時，系統將擲回該欄不存在的錯誤。
   * 當使用者嘗試執行具有多個包含受限欄的查詢時，系統將只為所有非受限欄傳回輸出。

1. 如果使用者請求存取計算欄位，該使用者需要存取構成中使用的所有欄位，或者系統將拒絕存取計算欄位。

如果在臨時結構描述上設定了身分或主要身分，則系統會自動執行任何關聯的資料衛生請求，並清除與身分欄繫結的資料集中的資料。

## 后续步骤

閱讀本檔案後，您對如何透過查詢服務CTAS查詢建立的臨時結構描述新增資料使用標籤有了更深入的瞭解。 如果您尚未這麼做，下列檔案有助於您進一步瞭解Query Service中的資料控管：

* [臨時結構描述身分](./ad-hoc-schema-identities.md)
* [資料控管](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hans)
