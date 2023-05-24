---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；網頁詳細資訊；資料型別；資料型別；資料型別；網頁
solution: Experience Platform
title: 網頁詳細資料資料型別
description: 本檔案提供網頁詳細資訊Experience Data Model (XDM)資料型別的概觀。
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# [!UICONTROL 網頁詳細資料] 資料型別

[!UICONTROL 網頁詳細資料] 是標準的Experience Data Model (XDM)資料型別，可描述剛載入及檢視之網頁的詳細資訊，如ExperienceEvent所記錄。

此資料型別適用於單頁網頁應用程式(SPA)的完整頁面詳細資料和初始頁面載入。 若為發生在載入頁面上的互動並未觸發新頁面載入，請參閱 [網路互動](./web-interaction.md) 資料型別。

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 測量]](./measure.md) | 網頁上的檢視次數。 |
| `URL` | 字符串 | 網頁的規範或一般URL。 這可能是也可能不是用來存取頁面的實際URL。 若要記錄用來存取頁面的URL，請使用 `webLink`. URI格式應遵循 [RFC 3986](https://tools.ietf.org/html/rfc3986) 標準。 |
| `isErrorPage` | 布尔值 | 此屬性會使用標幟來指出頁面是否為錯誤頁面。 此標幟可用來將網頁互動廣泛分類。 錯誤由應用程式定義，並可對應至提供HTTP錯誤碼的頁面。 |
| `isHomePage` | 布尔值 | 此屬性會使用標幟來指出頁面是否為首頁。 此標幟可用來將網頁互動廣泛分類。 首頁的定義由應用程式決定。 |
| `name` | 字符串 | 網頁的規範名稱。 此名稱不一定是頁面標題或直接與頁面內容相關聯，但用於組織網站頁面以進行分類。 |
| `server` | 字符串 | 託管網頁的規範或常用伺服器。 這可能是也可能不是實際提供頁面互動的主機或伺服器。 |
| `siteSection` | 字符串 | 此網頁所在的網站區段的規範名稱。 這可用來分類或分類互動。 |
| `viewName` | 字符串 | 頁面中檢視的名稱。 此屬性常用於具有變更大部分頁面版面的索引標籤或控制項的單頁應用程式或頁面。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)
