---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；順序；資料型別；資料型別；
solution: Experience Platform
title: 訂單資料型別
description: 本檔案提供訂單體驗資料模型(XDM)資料型別的概觀。
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 4%

---

# [!UICONTROL 訂購] 資料型別

[!UICONTROL 訂購] 是標準Experience Data Model (XDM)資料型別，可描述產品清單的訂單。

<img src="../images/data-types/order.PNG" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `payments` | 陣列 [[!UICONTROL 付款專案]](./payment-item.md) | 此訂單的付款清單。 |
| `currencyCode` | 字符串 | 用於訂單總額的ISO 4217貨幣代碼。 所有例項都必須符合規則運算式 `^[A-Z]{3}$`. 示例包括 `USD` 和 `EUR`。 |
| `priceTotal` | 双精度 | 此訂單套用所有折扣和稅金後的總價。 |
| `purchaseID` | 字符串 | 賣家為此購買或合約所指派的唯一識別碼。 由於這由賣家定義，無法保證ID是唯一的。 |
| `purchaseOrderNumber` | 字符串 | 購買者為此購買或合約所指派的唯一識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
