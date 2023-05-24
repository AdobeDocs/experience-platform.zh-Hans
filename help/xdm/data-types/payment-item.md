---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；付款專案；資料型別；資料型別；
solution: Experience Platform
title: 付款專案資料型態
description: 本檔案提供付款專案體驗資料模型(XDM)資料型別的概觀。
exl-id: d25a358b-73c1-468b-a9c5-808385689932
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 5%

---

# [!UICONTROL 付款專案] 資料型別

[!UICONTROL 付款專案] 是標準Experience Data Model (XDM)資料型別，可描述與訂單相關聯的付款，並定義付款型別、金額和相關聯的貨幣。

<img src="../images/data-types/payment-item.PNG" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `currencyCode` | 字符串 | 用於訂單總額的ISO 4217貨幣代碼。 所有例項都必須符合規則運算式 `^[A-Z]{3}$`. 示例包括 `USD` 和 `EUR`。 |
| `paymentAmount` | 双精度 | 付款的值。 |
| `paymentType` | 字符串 | 此訂單的付款方式。 接受的列舉值包括： <li> `cash` </li> <li> `credit_card` </li> <li> `debit_card` </li> <li> `gift_card` </li> <li> `check` </li> <li> `paypal` </li> <li> `wire_transfer` </li> <li> `credit_card_reference` </li> <li> `other` </li> |
| `transactionID` | 字符串 | 此付款專案的唯一交易識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/data/paymentitem.schema.json)
