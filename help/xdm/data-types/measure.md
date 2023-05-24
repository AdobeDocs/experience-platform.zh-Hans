---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；測量；資料型別；資料型別；
solution: Experience Platform
title: 測量資料型別
description: 本檔案提供測量體驗資料模型(XDM)資料型別的概觀。
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 1%

---

# [!UICONTROL 測量] 資料型別

[!UICONTROL 測量] 是標準Experience Data Model (XDM)資料型別，包含特定量度的具體可量化資料點。 測量由唯一識別碼和值組成。

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `id` | 字符串 | 此測量值的唯一識別碼。 在使用有損通訊通道（例如無法確保傳輸測量之行動應用程式或具有離線功能的網站）進行資料收集時，此屬性會包含使用者端產生的所採取測量之唯一ID。 最佳實務是將此動作維持足夠長的時間來確保足夠的隨機性。 <br><br> 如果時間戳記、裝置ID、IP、MAC位址或其他潛在的使用者識別值等資訊已納入產生程式 `id`，則結果應進行雜湊處理。 這可確保值中不會編碼PII，因為目標不是識別使用者或裝置，而是及時識別特定測量。 |
| `value` | 双精度 | 此測量的可量化值。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
