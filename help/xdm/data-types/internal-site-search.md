---
title: 內部網站搜尋資料型別
description: 本檔案提供內部網站搜尋XDM資料型別的概觀。
exl-id: 3cab9445-f641-4a44-9699-cd8a62da8a61
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# [!UICONTROL 內部網站搜尋] 資料型別

[!UICONTROL 內部網站搜尋] 是標準的XDM資料型別，可描述內部網站搜尋，包括所有相關搜尋行為和詳細資訊。

![](../images/data-types/internal-site-search.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `autoCompleteClicked` | [!UICONTROL 布尔型] | 指出訪客是使用建議的或自動完成的搜尋值來執行搜尋。 |
| `autoCompleteTypedValue` | [!UICONTROL 字符串] | 若是自動完成的情況，使用者有時會捨棄其搜尋結果，並從下拉式選單中選取特定字詞。 此值會追蹤使用者開始輸入的內容，以產生一組特定的建議搜尋詞。 |
| `autoCompleteValue` | [!UICONTROL 字符串] | 若是自動完成的情況，使用者有時會捨棄其搜尋結果，並從下拉式選單中選取特定字詞。 此值用於追蹤所選的特定詞語。 |
| `instances` | [!UICONTROL 整数] | 內部網站搜尋發生的次數。 |
| `locationInPage` | [!UICONTROL 字符串] | 當頁面上有多個搜尋方塊時，這個值應該用於識別使用者用來搜尋的特定位置。 |
| `nullInstances` | [!UICONTROL 整数] | 提供零結果的內部網站搜尋發生次數。 |
| `numberOfResults` | [!UICONTROL 整数] | 傳回的搜尋結果總數。 |
| `postalCode` | [!UICONTROL 字符串] | 用於搜尋的郵遞區號（如適用）。 |
| `productFindingMethods` | [!UICONTROL 字符串] | 具有銷售繫結的內部網站搜尋字詞值。 此值表示在檢視產品之前立即搜尋的字詞。 |
| `radiusDistance` | [!UICONTROL 整数] | 結合方式 `radiusType`，表示搜尋半徑的選取距離。 |
| `radiusType` | [!UICONTROL 整数] | 選取的距離型別 `radiusDistance`，英里或公里。 |
| `refinementInstances` | [!UICONTROL 整数] | 完善內部網站搜尋的次數。 |
| `refinementType` | 字串陣列 | 列出套用至搜尋結果的細分型別。 範例包括部門、品牌、價格、店內、評論評等、顏色、材質等。 |
| `refinementValue` | [!UICONTROL 字符串] | 將搜尋調整為的值。 |
| `resultsPageNumber` | [!UICONTROL 整数] | 針對分頁搜尋結果，此值會追蹤訪客正在檢視的結果頁面。 |
| `resultsPerPage` | [!UICONTROL 整数] | 若為分頁搜尋結果，此值會追蹤每頁顯示的搜尋結果數目。 |
| `searchType` | [!UICONTROL 字符串] | 擷取正在執行的搜尋方法（如適用）。 範例可能包括預先輸入搜尋、直接輸入搜尋或網站可能有的任何其他型別的自訂搜尋功能。 |
| `sortOrder` | [!UICONTROL 字符串] | 結合方式 `sortType`，表示搜尋結果的排序順序（升序或降序）。 |
| `term` | [!UICONTROL 字符串] | 訪客輸入的內部網站搜尋字詞。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/internal-site-search.schema.json).
