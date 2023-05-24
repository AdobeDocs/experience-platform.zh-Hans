---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；位址；xdm：位址；資料型別；資料型別；
solution: Experience Platform
title: 產品清單專案資料型別
description: 本檔案提供產品清單專案XDM資料型別的概觀。
exl-id: 056fdb5b-6782-4e29-9d62-90b270c05795
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# [!UICONTROL 產品清單專案] 資料型別

[!UICONTROL 產品清單專案] 是標準XDM資料型別，說明客戶所選產品的特定時間點，包含特定選項、定價和使用內容。

此資料型別中擷取的值可能與產品記錄不同。 例如，產品記錄包含來自產品資訊系統的細節，這些細節對所有客戶都是一致的，其中產品清單專案具有在購買時提供給客戶的實際價格，這可能因銷售活動或季節性定價而有所不同。

![](../images/data-types/product-list-item.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `selectedOptions` | 物件陣列 | 包含為可設定產品選擇的自訂選項。 每個清單專案都是一個物件，具有下列屬性：<ul><li>`attribute`：可設定屬性的名稱。</li><li>`value`：屬性的值。</li></ul> |
| `SKU` | [!UICONTROL 字符串] | 庫存單位(SKU)，供應商所定義之產品的唯一識別碼。 |
| `_id` | [!UICONTROL 字符串] | 此產品專案的明細專案識別碼。 產品本身的識別方式 `product`. |
| `currencyCode` | [!UICONTROL 字符串] | 此 [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) 用於為產品定價的字母貨幣代碼。 |
| `discountAmount` | [!UICONTROL 双精度] | 如果產品已貼現，這表示產品的一般價格與特殊價格之間的差額。 |
| `name` | [!UICONTROL 字符串] | 針對此產品檢視向使用者展示的產品顯示名稱。 |
| `priceTotal` | [!UICONTROL 双精度] | 產品明細專案的總價。 |
| `product` | [!UICONTROL 字串] (URI) | URI `$id` 擷取產品本身的XDM結構描述。 |
| `productAddMethod` | [!UICONTROL 字符串] | 訪客用來將產品專案新增至清單的方法。 |
| `productImageUrl` | [!UICONTROL 字符串] | 產品主要影像的URL。 |
| `quantity` | [!UICONTROL 整数] | 客戶表示所需的產品單位數。 |
| `unitOfMeasureCode` | [!UICONTROL 字符串] | 標準 [單位代碼](https://ucum.org/ucum) 與相關的產品 `quantity` 屬性。 |

{style="table-layout:auto"}

如需郵寄地址資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json)
