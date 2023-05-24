---
title: 產品類別
description: 本檔案提供Experience Data Model (XDM)中產品類別的概觀。
exl-id: 911680ae-b761-4945-9ad3-0233eaea89b0
source-git-commit: fdd68e5a94d841992a6f8abe10f3cffe0ebb6794
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 6%

---

# [!UICONTROL 產品] 類別

在Experience Data Model (XDM)中， [!UICONTROL 產品] class會擷取定義零售產品的最小屬性集。

![](../images/classes/product.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `productListPrice` | [货币](../data-types/currency.md) | 說明產品在銷售和折扣前的預設價格。 |
| `_id` | 字符串 | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會向其提供明確值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。 |
| `productDescription` | 字符串 | 產品的說明。 |
| `productID` | 字符串 | 產品的唯一識別碼。 |
| `productLastModifiedDate` | 日期時間 | 一個 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 上次修改此產品以進行任何更新的時間戳記。 |
| `productManufacturedDate` | 日期時間 | 一個 [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) 建立此產品時的時間戳記。 |
| `productName` | 字符串 | 产品的名称。 |
| `productRating` | 字符串 | 產品的客戶評論評分。 |

{style="table-layout:auto"}

## 相容的欄位群組 {#field-groups}

Adobe提供數個標準欄位群組，可搭配使用 [!UICONTROL 產品] 類別。 以下是類別的一些常用欄位群組清單：

* [[!UICONTROL 產品目錄]](../field-groups/product/product-catalog.md)
* [[!UICONTROL 產品類別]](../field-groups/product/product-category.md)
