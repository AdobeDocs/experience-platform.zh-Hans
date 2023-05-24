---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；裝置；資料型別；資料型別；貨幣；
solution: Experience Platform
title: 貨幣資料型別
description: 本檔案提供貨幣XDM資料型別的概觀。
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 3%

---

# [!UICONTROL 貨幣] 資料型別

[!UICONTROL 貨幣] 是標準的XDM資料型別，說明貨幣金額，包括貨幣型別和轉換日期。

![](../images/data-types/currency.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `amount` | 双精度 | 由定義的貨幣金額 `currencyCode`. |
| `conversionDate` | 日期時間 | 進行貨幣轉換的時間戳記。 |
| `currencyCode` | 字符串 | ISO 4217代碼，指示貨幣型別 `amount` 表示。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
