---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；陣列；欄位；
solution: Experience Platform
title: 在UI中定義陣列欄位
description: 瞭解如何在Experience Platform使用者介面中定義陣列欄位。
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 在UI中定義陣列欄位

在Adobe Experience Platform使用者介面中定義Experience Data Model (XDM)欄位時，您可以將該欄位指定為陣列。

陣列的內容取決於 [!UICONTROL 型別] 已為該欄位選取。 例如，如果欄位的 [!UICONTROL 型別] 設為&quot;[!UICONTROL 字串]&quot;，將該欄位設定為陣列會將欄位指定為字串陣列。 如果欄位的 [!UICONTROL 型別] 設為多欄位資料型別，例如&quot;[!UICONTROL 郵寄地址]&quot;，則它會變成符合資料型別的一系列郵寄地址物件。

在您擁有 [在UI中定義新欄位](./overview.md#define)，您可以選取 **[!UICONTROL 陣列]** 核取方塊。

![](../../images/ui/fields/special/array.png)

選取核取方塊後，右側欄中會出現其他控制項，可讓您選擇進一步限制陣列。 如果您不想強制執行特定限制，請將此欄位留空。

陣列的其他設定控制項如下：

| 欄位屬性 | 描述 |
| --- | --- |
| [!UICONTROL 最小長度] | 陣列必須包含的專案數下限才能成功內嵌。 |
| [!UICONTROL 最大长度] | 陣列必須包含的專案數上限，才能成功內嵌。 |
| [!UICONTROL 僅限唯一專案] | 若設為&quot;[!UICONTROL True]&quot;，陣列中的每個專案都必須是唯一的，才能成功擷取。 |

{style="table-layout:auto"}

完成欄位設定後，選取 **[!UICONTROL 套用]** 將變更套用至結構描述。

![](../../images/ui/fields/special/array-config.png)

畫布會更新以反映對欄位所做的變更。 請注意，畫布中欄位名稱旁邊顯示的資料型別會附加一對方括弧(`[]`)，指出欄位代表該資料型別的陣列。

![](../../images/ui/fields/special/array-applied.png)

## 后续步骤

本指南說明如何在UI中定義陣列欄位。 請參閱以下文章的概觀： [在UI中定義欄位](./overview.md#special) 瞭解如何在中定義其他XDM欄位型別 [!DNL Schema Editor].
