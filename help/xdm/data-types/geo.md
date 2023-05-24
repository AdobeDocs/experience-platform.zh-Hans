---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；地理；資料型別；資料型別；
solution: Experience Platform
title: 地理資料型別
description: 本檔案提供地理XDM資料型別的概觀。
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# [!UICONTROL 地理] 資料型別

[!UICONTROL 地理] 是標準XDM資料型別，可描述觀察事件的地理區域。

<img src="../images/data-types/geo.png" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 地理座標]](./geo-coordinates.md) | 說明地點的地理座標。 |
| `_id` | 字符串 | 系統產生的唯一座標ID。 |
| `city` | 字符串 | 城市名稱。 |
| `countryCode` | 字符串 | 兩個字元 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 國家/地區的代碼。 |
| `dmaID` | 整数 | Nielsen媒體研究指定的市場區域。 |
| `msaID` | 整数 | 進行觀察的美國大都會統計區域。 |
| `postalCode` | 字符串 | 地點的郵遞區號。 郵遞區號並非適用於所有國家/地區。 在某些國家/地區，這僅包含部分郵遞區號。 |
| `stateProvince` | 字符串 | 觀察的州或省的部分。 格式會遵循 [ISO 3166-2 （國家/地區和細分）](https://www.unece.org/cefact/locode/subdivisions.html) 標準。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
