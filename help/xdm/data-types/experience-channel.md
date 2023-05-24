---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；網頁詳細資訊；資料型別；資料型別；資料型別；網頁
solution: Experience Platform
title: Experience Channel資料型別
description: 本檔案提供Experience Channel Experience Data Model (XDM)資料型別的概述。
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# [!UICONTROL 體驗管道] 資料型別

[!UICONTROL 體驗管道] 是描述體驗管道的標準Experience Data Model (XDM)資料型別。 體驗管道代表如何使用數位體驗的方法或路徑。

有多種體驗管道，每一種管道對於如何傳遞內容、如何觀察客戶互動以及如何收集資料都有不同的限制。 在管道內，可將體驗傳送至特定位置。 頻道中存在的位置和位置型別因頻道而異。

![](../images/data-types/experience-channel.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `_id` | 字符串 | 可唯一識別管道的ID。 每個特定體驗管道會定義一個常數 `@id`. |
| `_type` | 字符串 | 為具有類似屬性的管道提供粗略分類標籤。 |
| `contentTypes` | 字串陣列 | 此頻道可提供的內容型別。 |
| `locationTypes` | 字串陣列 | 此管道所包含且可傳送內容的目標位置型別（虛擬地點）。 |
| `mediaAction` | 字符串 | 說明Experience Event媒體動作（如適用）。 |
| `mediaType` | 字符串 | 說明媒體型別是付費、擁有還是贏得。 |
| `metricTypes` | 字串陣列 | 可在此管道中收集的量度。 |
| `mode` | 字符串 | 如何在此管道中提供體驗。 |
| `typeAtSource` | 字符串 | 管道的自訂名稱。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
