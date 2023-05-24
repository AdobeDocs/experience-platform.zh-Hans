---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；必要；欄位；
title: 在UI中定義必填欄位
description: 瞭解如何在Experience Platform使用者介面中定義必要的XDM欄位。
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 在UI中定義必填欄位

在Experience Data Model (XDM)中，必填欄位表示必須提供有效值，才能在資料擷取期間接受特定記錄或時間序列事件。 必要欄位的常見使用案例包括使用者身分資訊和時間戳記。

>[!IMPORTANT]
>
>無論結構描述欄位是否為必填，平台都不會接受 `null` 或任何內嵌欄位的空白值。 如果記錄或事件中特定欄位沒有值，則應該從擷取裝載中排除該欄位的索引鍵。

時間 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，您可以選取 **[!UICONTROL 必填]** 核取方塊。 選取 **[!UICONTROL 套用]** 將變更套用至結構描述。

![必要核取方塊](../../images/ui/fields/required/root.png)

如果欄位是租使用者ID物件下的根層級屬性，則其路徑會立即出現在 **[!UICONTROL 必填欄位]** 在左側邊欄中。

![根層級必填欄位](../../images/ui/fields/required/applied.png)

不過，如果必要欄位巢狀內嵌在未標籤為必要本身的物件中，則巢狀欄位不會出現在 **[!UICONTROL 必填欄位]** 在左側邊欄中。

在以下範例中， `internalSKU` 欄位已設定為必要，但其父物件 `SKUs` 不是。 在此情況下，若發生以下情況，則不會發生驗證錯誤： `SKUs` 在內嵌資料時排除，即使子欄位亦然 `internalSKU` 標示為必要。 換言之，當 `SKUs` 是選用專案，它必須包含 `internalSKU` 欄位（在包含欄位的情況下）。

![巢狀必要欄位](../../images/ui/fields/required/nested.png)

如果您希望結構描述中一律需要巢狀欄位，您也必須視需要設定所有父欄位（租使用者ID物件除外）。

![父項和子項必填欄位](../../images/ui/fields/required/parent-and-child.png)

## 后续步骤

本指南說明如何在UI中定義必填欄位。 請參閱以下文章的概觀： [在UI中定義欄位](./overview.md#special) 瞭解如何在中定義其他XDM欄位型別 [!DNL Schema Editor].
