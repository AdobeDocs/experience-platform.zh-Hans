---
keywords: Experience Platform；首頁；熱門主題；對應csv；對應csv檔案；將csv檔案對應到xdm；將csv對應到xdm；ui指南；對應程式；對應；資料準備；資料準備；
solution: Experience Platform
title: 資料準備總覽
description: 本檔案介紹Adobe Experience Platform中的資料準備。
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# 計算欄位

計算欄位允許根據輸入結構描述中的屬性建立值。 然後可以將這些值指派給目標結構描述中的屬性，並提供名稱和說明，以便更輕鬆地參考。

若要建立計算欄位，請選取 **[!UICONTROL 新增計算欄位]**.

![](./images/calculated-fields/add-calculated-field.png)

此 **[!UICONTROL 建立計算欄位]** 面板隨即顯示。 左側對話方塊包含計算欄位支援的欄位、函式和運運算元。 選取其中一個標籤，以開始將函式、欄位或運運算元新增至運算式編輯器。

![](./images/calculated-fields/create-calculated-field.png)

| 选项卡 | 描述 |
| --- | ----------- |
| 函数 | 函式標籤會列出可用來轉換資料的函式。 若要進一步瞭解您可以在計算欄位中使用的函式，請閱讀以下指南： [使用資料準備（對應程式）函式](./functions.md). |
| 字段 | 欄位索引標籤會列出來源結構描述中可用的欄位和屬性。 |
| 操作员 | 運運算元索引標籤會列出可用於轉換資料的運運算元。 |

您可以使用中央的運算式編輯器，手動新增欄位、函式和運運算元。 選取編輯器以開始建立運算式。

![](./images/calculated-fields/write-calculated-field.png)

選取 **[!UICONTROL 儲存]** 以繼續進行。

對應畫面會重新出現，並顯示您新建立的來源欄位。 套用適當的對應目標欄位並選取 **[!UICONTROL 完成]** 以完成對應。

![](./images/calculated-fields/new-calculated-field.png)
