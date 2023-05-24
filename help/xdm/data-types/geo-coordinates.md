---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；地理；座標；資料型別；資料型別；
solution: Experience Platform
title: 地理座標資料型別
description: 本檔案提供地理座標XDM資料型別的概觀。
exl-id: 3c80eb44-852f-4a95-bd13-b6197ffe62da
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 地理座標] 資料型別

[!UICONTROL 地理座標] 是標準XDM資料型別，可描述地標的地理座標。 此資料型別以記錄的公開規格為基礎 [schema.org](https://schema.org/GeoCoordinates).

<img src="../images/data-types/geo-coordinates.png" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_schema.description` | 字符串 | 座標識別內容的說明。 |
| `_schema.elevation` | 双精度 | 已定義座標的特定上升量。 值必須符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，並以公尺測量。 |
| `_schema.latitude` | 双精度 | 地理點的已簽署垂直座標。 |
| `_schema.longitude` | 双精度 | 地理點的已簽署水平座標。 |
| `_id` | 字符串 | 系統產生的唯一座標ID。 |
