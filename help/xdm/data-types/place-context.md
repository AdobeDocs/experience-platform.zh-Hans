---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；位置上下文；placeContext；資料型別；資料型別；
solution: Experience Platform
title: 地標內容資料型別
description: 本檔案提供地標內容XDM資料型別的概觀。
exl-id: d7cf7366-0136-49ee-84d2-ec663db66eb4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 4%

---

# [!UICONTROL 地標內容] 資料型別

[!UICONTROL 地標內容] 是標準的XDM資料型別，可描述觀察到的事件位置，包括興趣點資訊和地理座標。

<img src="../images/data-types/place-context.png" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `POIinteraction` | [[!UICONTROL 興趣點互動]](./poi-interaction.md) | 說明興趣點(POI)互動的詳細資訊。 |
| `activePOIs` | 陣列 [[!UICONTROL 興趣點細節]](./poi-details.md) | 說明導致事件的POI。 |
| `geo` | [[!UICONTROL 地域]](./geo.md) | 說明提供體驗的地理位置。 |
| `localTime` | 日期時間 | 中的時間戳記 [RFC 3339](https://tools.ietf.org/html/rfc3339) 格式，表示當地時間，並加上指定的時區位移。 格式模式為 `yyyy-MM-dd'T'HH:mm:ssXXX` (例如， `2001-07-04T12:08:56-07:00`)。 |
| `localTimezoneOffset` | 整数 | 目前本地時區與UTC的偏移量（分鐘） `localTime` 值。 這應該包括目前的DST位移（如果適用）。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/placecontext.schema.json)
