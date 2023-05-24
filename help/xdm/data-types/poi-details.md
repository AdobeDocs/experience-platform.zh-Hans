---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；poi；poi詳細資訊；地標；興趣點詳細資訊；資料型別；資料型別；
solution: Experience Platform
title: 興趣點詳細資料資料型別
description: 本檔案提供Point Of Interest詳細資訊XDM資料型別的概觀。
exl-id: cab5463b-97a0-400d-a00c-0cd8bf9301a5
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 3%

---

# [!UICONTROL 興趣點細節] 資料型別

[!UICONTROL 興趣點細節] 是標準XDM資料型別，可描述觀察到事件的地理相關資料。

<img src="../images/data-types/poi-details.png" width="550" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `beaconInteractionDetails` | [[!UICONTROL Beacon]](./beacon.md) | 說明POI互動作用中的信標詳細資訊。 |
| `geoInteractionDetails` | [[!UICONTROL 地理互動細節]](./geo-interaction-details.md) | 說明進行POI互動的有效地理位置細節。 |
| `category` | 字符串 | 由POI定義的系統管理員指派來組織POI的一般類別。 |
| `distanceToPOICenter` | 双精度 | 與POI中心的預估距離（公尺）。 |
| `locatingType` | 字符串 | 用來判斷位置的機制。 接受的值包括： <ul><li>`beacon`</li><li>`gps`</li><li>`ip`</li><li>`ip+wifi`</li><li>`wifi-triangulation`</li></ul> |
| `name` | 字符串 | 指定給POI的名稱。 |
| `poiID` | 字符串 | POI的唯一識別碼。 |
| `type` | 字符串 | 使用POI定義的系統管理員所選取的輸入結構描述的POI一般型別。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json)
