---
title: 曝光數資料型別
description: 本檔案提供「曝光數」XDM資料型別的概觀。
exl-id: 1e758043-a41e-45f7-ae8b-514990d0649e
source-git-commit: afdac5ce2ed967b4688d456a586c946bc2cf4179
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# [!UICONTROL 曝光次數] 資料型別

[!UICONTROL 曝光次數] 是描述行銷印象的標準XDM資料型別，這是用於量化一段內容（例如廣告、數位貼文或網頁）的數位檢視或參與次數的量度。

![](../images/data-types/impressions.png)

| 属性 | 資料型別 | 描述 |
| --- | --- | --- |
| `ID` | 字符串 | 閱聽的唯一ID。 |
| `displays` | 整数 | 閱聽專案已向客戶顯示的次數。 |
| `selected` | 整数 | 已選取或點按曝光專案的次數。 |
| `type` | 字符串 | 曝光型別。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/impressions.schema.json)
