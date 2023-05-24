---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；地理；地理形狀；資料型別；資料型別；資料型別；
solution: Experience Platform
title: 地理形狀資料型別
description: 本檔案提供地理形狀XDM資料型別的概觀。
exl-id: 50b9d783-a555-45eb-b154-7dc71389e224
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# [!UICONTROL 地理形狀] 資料型別

[!UICONTROL 地理形狀] 是描述地理區域形狀的標準XDM資料型別。 此資料型別以記錄的公開規格為基礎 [schema.org](https://schema.org/GeoShape).

<img src="../images/data-types/geo-shape.png" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_schema.box` | 陣列 [[!UICONTROL 地理座標]](./geo-coordinates.md) | 描述由兩個座標形成的矩形所圍起來的地理區域。 第一個座標是矩形的下角，第二個座標是上角。 |
| `_schema.circle` | 陣列 [[!UICONTROL 地理座標]](./geo-coordinates.md) | 描述以地理座標為中心的特定半徑圓形區域。 |
| `_schema.polygon` | [[!UICONTROL 地理圈]](./geo-circle.md) | 一系列四個或更多座標，其中第一個和最後一個座標完全相同。 |
| `_schema.description` | 字符串 | 形狀定義內容的說明。 |
| `_schema.elevation` | 双精度 | 形狀的特定或最小仰角。 此值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，並以公尺測量。 搭配 `ceiling`，此屬性可用來表示位置的三維邊界方框。 |
| `_id` | 字符串 | 形狀的系統產生的唯一識別碼。 |
| `ceiling` | 双精度 | 形狀的最大上升量。 此屬性只有在搭配使用時才有效 `elevation`. 該值符合 [WGS84](https://gisgeography.com/wgs84-world-geodetic-system/) 基準，並以公尺測量。 搭配 `elevation`，此屬性可用來表示位置的三維邊界方框。 |
