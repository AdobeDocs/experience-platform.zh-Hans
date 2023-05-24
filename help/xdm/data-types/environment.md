---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；環境；資料型別；資料型別；
solution: Experience Platform
title: 環境資料型別
description: 本檔案提供環境XDM資料型別的概觀。
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 4%

---

# [!UICONTROL 環境] 資料型別

[!UICONTROL 環境] 是標準的XDM資料型別，可描述觀察到的事件周圍環境，尤其會詳細說明網路和軟體版本之類的臨時資訊。

>[!IMPORTANT]
>
>所有值都應與 [DeviceAtlas](https://deviceatlas.com) 資料庫，依Adobe授權。

<img src="../images/data-types/environment.png" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_dc` | 对象 | 包含單一欄位的物件， `language`，代表環境語言，可代表使用者對於資料表示的語言、地理或文化偏好設定。 語言是依照中定義的語言代碼指定的 [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [瀏覽器詳細資料](./browser-details.md) | 說明環境的瀏覽器特定詳細資訊，例如瀏覽器名稱、版本、JavaScript版本、使用者代理字串以及接受語言。 |
| `ISP` | 字符串 | 使用者的網際網路服務提供者的名稱。 |
| `carrier` | 字符串 | 向使用者銷售並提供通訊服務的行動網路電信業者或MNO （也稱為無線服務提供者、無線電信業者、行動電話公司或行動網路電信業者）的名稱。 |
| `colorDepth` | 整数 | 用於單一畫素的每個顏色分量的位元數。 |
| `connectionType` | 字符串 | 網際網路連線型別。 接受的值包括： <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | 字符串 | 使用者ISP的網域。 |
| `ipV4` | 字符串 | 指定給參與使用網際網路通訊協定進行通訊（32位元）的電腦網路之裝置的數字標籤。 |
| `ipV6` | 字符串 | 指定給參與使用網際網路通訊協定進行通訊的電腦網路（128位元）之裝置的數字標籤。 |
| `operatingSystem` | 字符串 | 完成觀察時所使用的作業系統名稱。 屬性不應包含任何版本資訊，例如 `10.5.3`，而是包含「版本」標示，例如 `Ultimate` 或 `Professional`. |
| `operatingSystemVendor` | 字符串 | 完成觀察時所使用的作業系統供應商名稱。 |
| `operatingSystemVersion` | 字符串 | 完成觀察時所用作業系統的完整版本識別碼。 版本通常由數字組成，但可能採用廠商定義的格式。 |
| `type` | 字符串 | 應用程式環境的型別。 請參閱 [附錄](#type) 以取得接受的值。 |
| `viewportHeight` | 整数 | 內部顯示體驗的視窗垂直大小（畫素）。 若為網頁檢視事件，此為瀏覽器檢視區高度。 |
| `viewPortWidth` | 整数 | 顯示體驗的視窗水準大小（畫素）。 若為網頁檢視事件，此為瀏覽器檢視區寬度。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## 附录

以下小節包含更多關於 [!UICONTROL 裝置] 資料型別。

## 接受的型別值 {#type}

下表概述下列專案的可接受值 `type` 及其相關涵義：

| 值 | 描述 |
| --- | --- |
| `browser` | 浏览器 |
| `application` | 应用程序 |
| `iot` | 物聯網 |
| `external` | 外部系統 |
| `widget` | 應用程式延伸模組 |
