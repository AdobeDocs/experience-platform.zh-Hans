---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；poi；互動；興趣點；興趣點；資料型別；資料型別；
solution: Experience Platform
title: 興趣點互動資料型別
description: 本檔案提供興趣點互動XDM資料型別的概觀。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# [!UICONTROL 興趣點互動] 資料型別

[!UICONTROL 興趣點互動] 是標準的XDM資料型別，說明在行動裝置進入範圍內時，將身分資訊傳遞給行動應用程式的無線裝置。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 興趣點細節]](./poi-details.md) | 說明導致事件的POI的詳細資料。 |
| `poiEntries` | 对象 | 說明個人已進入POI的次數。 包含兩個屬性： <ul><li>`id`：測量的唯一識別碼。</li><li>`value`：測量的可量化值。</li></ul> |
| `poiExits` | 对象 | 說明個人已退出POI的次數。 包含兩個屬性： <ul><li>`id`：測量的唯一識別碼。</li><li>`value`：測量的可量化值。</li></ul> |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
