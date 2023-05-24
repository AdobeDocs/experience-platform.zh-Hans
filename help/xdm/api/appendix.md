---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；相容性；相容性；相容性模式；相容性模式；欄位型別；欄位型別；
solution: Experience Platform
title: 結構描述登入API指南附錄
description: 本檔案提供與使用結構描述登入API相關的補充資訊。
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# 結構描述登入API指南附錄

本檔案提供與使用相關的補充資訊 [!DNL Schema Registry] API。

## 使用查詢引數 {#query}

此 [!DNL Schema Registry] 支援在列出資源時使用查詢引數來頁面和篩選結果。

>[!NOTE]
>
>合併多個查詢引數時，必須以&amp;符號(`&`)。

### 分页 {#paging}

分頁最常見的查詢引數包括：

| 参数 | 描述 |
| --- | --- |
| `orderby` | 依特定屬性排序結果。 範例： `orderby=title` 會依標題以遞增順序(A-Z)排序結果。 新增 `-` 在引數值之前(`orderby=-title`)會依標題以遞減順序(Z-A)排序專案。 |
| `limit` | 當與 `orderby` 引數， `limit` 限制指定請求應傳回的專案數上限。 若無此引數，就無法使用 `orderby` 引數存在。<br><br>此 `limit` 引數指定正整數(介於 `0` 和 `500`)作為 *提示* 應傳回的專案數上限。 例如， `limit=5` 只傳回清單中的五個資源。 不過，此值並非嚴格遵循。 實際的回應大小可能會小於或大於此值，因為需要提供 `start` 引數（若有）。 |
| `start` | 當與 `orderby` 引數， `start` 指定專案子集清單的開始位置。 若無此引數，就無法使用 `orderby` 引數存在。 此值可從下列位置取得： `_page.next` 清單回應的屬性，並用來存取結果的下一頁。 如果 `_page.next` 值為null，則沒有其他可用頁面。<br><br>通常省略此引數是為了取得結果的第一頁。 之後， `start` 應設定為以下專案的主要排序屬性最大值： `orderby` 在上一頁收到的欄位。 API回應接著會傳回開頭為具有主要排序屬性的專案 `orderby` 嚴格大於（遞增）或嚴格小於（遞減）指定值。<br><br>例如，如果 `orderby` 引數已設為 `orderby=name,firstname`，則 `start` 引數會包含 `name` 屬性。 在這種情況下，如果您想在名稱「Miller」之後立即顯示資源的接下來的20個專案，您可以使用： `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### 正在筛选 {#filtering}

您可以使用以下專案來篩選結果： `property` 引數，用於針對擷取資源內的指定JSON屬性套用特定運運算元。 支援的運運算元包括：

| 操作员 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 依據屬性是否等於提供的值來篩選。 | `property=title==test` |
| `!=` | 依據屬性是否不等於提供的值來篩選。 | `property=title!=test` |
| `<` | 依據屬性是否小於提供的值來篩選。 | `property=version<5` |
| `>` | 依據屬性是否大於提供的值來篩選。 | `property=version>5` |
| `<=` | 依據屬性是否小於或等於提供的值來篩選。 | `property=version<=5` |
| `>=` | 依據屬性是否大於或等於提供的值來篩選。 | `property=version>=5` |
| `~` | 依據屬性是否符合提供的規則運算式進行篩選。 | `property=title~test$` |
| (None) | 若僅指出屬性名稱，則只會傳回屬性存在的專案。 | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>您可以使用 `property` 用於依結構描述欄位群組的相容類別來篩選結構描述欄位群組的引數。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 只傳回與相容的欄位群組 [!DNL XDM Individual Profile] 類別。

## 相容性模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是公開記錄的規格，由Adobe驅動，以改善數位體驗的互用性、表現力和效能。 Adobe會在中維護原始程式碼和正式XDM定義 [GitHub上的開放原始碼專案](https://github.com/adobe/xdm/). 這些定義是以XDM標準標籤法編寫，使用JSON-LD （連結資料的JavaScript物件標籤法）和JSON結構描述作為定義XDM結構描述的文法。

在公開存放庫中檢視正式XDM定義時，您可以看到標準XDM與您在Adobe Experience Platform中看到的不同。 您在中看到的內容 [!DNL Experience Platform] 這稱為相容性模式，它提供標準XDM與其使用方式之間的簡單對應 [!DNL Platform].

### 相容性模式的運作方式

相容性模式可讓XDM JSON-LD模型透過變更標準XDM中的值同時保持相同的語意來搭配現有資料基礎結構運作。 它使用巢狀JSON結構，以樹狀格式顯示結構描述。

您在標準XDM和相容性模式之間會注意到的主要差異，是移除欄位名稱的「xdm：」首碼。

以下並排比較會顯示標準XDM和相容性模式中與生日相關的欄位（已移除「說明」屬性）。 請注意，相容性模式欄位包括對XDM欄位的引用，以及其「meta：xdmField」和「meta：xdmType」屬性中的資料型別。

<table style="table-layout:auto">
  <th>標準XDM</th>
  <th>相容性模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm：birthDate"： { "title"： "Birth Date"， "type"： "string"， "format"： "date" }， "xdm：birthDayAndMonth"： { "title"： "Birth Date"， "type"： "string"， "pattern"： "[0-1][0-9]-[0-9][0-9]" }， "xdm：birthYear"： { "title"： "Birth year"， "type"： "integer"： 1， "maximimum"： 32767 } } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate"： { "title"： "Birth Date"， "type"： "string"， "format"： "date"， "meta：xdmField"： "xdm：birthDate"， "meta：xdmType"： "date" }， "birthDayAndMonth"： { "title"： "Birth Date"， "type"： "string"， "pattern"： "[0-1][0-9]-[0-9]"， "meta：xdmField"： "xdm：birthDayAnd"， meta：xdmType"： "string" }， "birthYear"： { "title"： "Birth year"， "type"： "integer"， "minimum"： 1， "maximum"： 32767， "meta：xdmField"： "xdm：birthYear"， "meta：xdmType"： "short" }
      </pre>
  </td>
  </tr>
</table>

### 為何需要相容性模式？

Adobe Experience Platform設計為可與多種解決方案和服務搭配使用，而每一種解決方案和服務都有各自的技術挑戰和限制（例如，某些技術如何處理特殊字元）。 為了克服這些限制，我們開發了相容性模式。

最多 [!DNL Experience Platform] 服務包括 [!DNL Catalog]， [!DNL Data Lake]、和 [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] 以取代標準XDM。 此 [!DNL Schema Registry] API也使用 [!DNL Compatibility Mode]，而本檔案中的範例全部使用以下專案顯示 [!DNL Compatibility Mode].

值得一提的是，對應會發生在標準XDM與其操作方式之間 [!DNL Experience Platform]，但應該不會影響您的使用 [!DNL Platform] 服務。

開放原始碼專案可供您使用，但當您透過與資源互動時， [!DNL Schema Registry]，本檔案中的API範例提供您應知道並遵循的最佳實務。
