---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；網頁互動；資料型別；資料型別；
solution: Experience Platform
title: Web互動資料型別
description: 本檔案提供網頁互動Experience Data Model (XDM)資料型別的概觀。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# [!UICONTROL 網路互動] 資料型別

[!UICONTROL 網路互動] 是標準的Experience Data Model (XDM)資料型別，可說明初始頁面載入完成後發生在網頁上的互動相關資訊。 它主要用於記錄豐富網頁應用程式(例如單頁網頁應用程式(SPA))中不會觸發新頁面載入的互動。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 測量]](./measure.md) | 追蹤網頁連結點選的測量。 |
| `URL` | 字符串 | 用於此網頁互動的實際連結或URL。 |
| `name` | 字符串 | 用於此網頁連結的規範名稱。 這是用於分類目的。 |
| `type` | 字符串 | 連結型別。 此屬性必須等於下列其中一個列舉值： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
