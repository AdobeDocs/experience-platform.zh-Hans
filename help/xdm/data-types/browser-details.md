---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；瀏覽器；瀏覽器詳細資訊；資料型別；資料型別；
solution: Experience Platform
title: 瀏覽器詳細資料資料型別
description: 本檔案提供瀏覽器詳細資訊XDM資料型別的概觀。
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 11%

---

# [!UICONTROL 瀏覽器詳細資料] 資料型別

[!UICONTROL 瀏覽器詳細資料] 是標準XDM資料型別，說明與瀏覽器或應用程式相關的詳細資訊。

<img src="../images/data-types/browser-details.png" width="450" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `acceptLanguage` | 字符串 | IETF語言標籤([RFC 5646](https://tools.ietf.org/html/rfc5646))。 |
| `cookiesEnabled` | 布尔值 | 指出使用者的設定是否允許寫入Cookie。 |
| `javaEnabled` | 布尔值 | 指出進行觀察的裝置是否已啟用Java。 |
| `javaScriptEnabled` | 布尔值 | 指出進行觀察的裝置是否已啟用JavaScript。 |
| `javaScriptVersion` | 字符串 | 在觀察期間受支援的JavaScript版本。 |
| `javaVersion` | 字符串 | 觀察期間支援的Java版本。 |
| `name` | 字符串 | 應用程式或瀏覽器名稱。 |
| `quicktimeVersion` | 字符串 | 在觀察期間受支援的Apple Quicktime版本。 |
| `thirdPartyCookiesEnabled` | 布尔值 | 指出進行觀察的裝置是否啟用第三方Cookie。 |
| `userAgent` | 字符串 | 來自使用者端請求的HTTP使用者代理字串。 |
| `vendor` | 字符串 | 應用程式或瀏覽器廠商。 |
| `version` | 字符串 | 應用程式或瀏覽器版本。 |
| `viewportHeight` | 整数 | 顯示事件之視窗的垂直大小（畫素）。 若為網頁檢視事件，此為瀏覽器檢視區高度。 |
| `viewportWidth` | 整数 | 顯示事件之視窗的水準大小（畫素）。 若為網頁檢視事件，此為瀏覽器檢視區寬度。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
