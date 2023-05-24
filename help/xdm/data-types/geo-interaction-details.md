---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；信標；互動細節；資料型別；資料型別；
solution: Experience Platform
title: 地理互動詳細資料資料型別
description: 本檔案提供地域互動詳細資訊XDM資料型別的概觀。
exl-id: c05b098b-3f12-4283-a6d5-5ebf96b9828d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---

# [!UICONTROL 地理互動細節] 資料型別

[!UICONTROL 地理互動細節] 是標準XDM資料型別，說明地理定義區域中目前的包含狀態。

<img src="../images/data-types/geo-interaction-details.png" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `geoShape` | [[!UICONTROL 地理形狀]](./geo-shape.md) | 說明互動區域的地理形狀。 此欄位可描述方塊、圓形或多邊形。 |
| `deviceGeoAccuracy` | 双精度 | 地理測量裝置或機制的精確度（以公尺衡量）。 |
| `distanceToCenter` | 双精度 | 在地理圓圈的情況下與地理中心的距離（以公尺測量）。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/geo-interaction-details.schema.json)
