---
title: 管理結構描述的資料使用標籤
description: 瞭解如何在Adobe Experience Platform UI中新增資料使用標籤至Experience Data Model (XDM)結構描述欄位。
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 6%

---

# 管理結構描述的資料使用標籤

>[!IMPORTANT]
>
>以結構描述為基礎的標籤是的一部分 [基於屬性的存取控制](../../access-control/abac/overview.md)，目前提供限量版給美國的醫療保健客戶。 此功能在完全發行後，將可供所有Adobe Real-time Customer Data Platform客戶使用。

所有帶入Adobe Experience Platform的資料都受到Experience Data Model (XDM)結構描述的限制。 贵组织或法律法规可能会对此数据设置使用限制。為了解決這個問題，Platform可讓您透過使用來限制特定資料集和欄位的使用 [資料使用標籤](../../data-governance/labels/overview.md).

套用至結構描述欄位的標籤會指出套用至該特定欄位中所包含資料的使用原則。

標籤可套用至個別資料集（以及這些資料集中的欄位），但您也可以在結構描述層級套用標籤。 標籤直接套用至結構描述時，這些標籤會傳播至以該結構描述為基礎的所有現有和未來資料集。

此外，您在某個結構描述中新增的任何欄位標籤，都會傳播至使用共用類別或欄位群組中相同欄位的所有其他結構描述。 這有助於確保類似欄位的使用規則在整個資料模型中保持一致。

本教學課程涵蓋在Platform UI中使用「結構描述編輯器」將標籤新增到結構描述的步驟。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述編輯器](../ui/overview.md)：瞭解如何在Platform UI中建立和管理結構描述和其他資源。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md)：提供基礎結構，以強制對Platform作業執行資料使用限制，使用定義哪些行銷動作可以（或無法）對標籤資料執行的原則。

## 選取要新增標籤的結構描述或欄位 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="编辑治理标签"
>abstract="将标签应用于架构字段可指示适用于该特定字段中包含的数据的使用策略。"

若要開始新增標籤，您必須先 [選取要編輯的現有結構描述](../ui/resources/schemas.md#edit) 或 [建立新結構描述](../ui/resources/schemas.md#create) 以在「架構編輯器」中檢視其結構。

若要編輯個別欄位的標籤，您可以在畫布中選取欄位，然後選取 **[!UICONTROL 管理存取權]** 在右側邊欄中。

![從結構編輯器畫布選取欄位](../images/tutorials/labels/manage-access.png)

您也可以選取 **[!UICONTROL 標籤]** 索引標籤中，從清單中選擇所需的欄位，然後選取 **[!UICONTROL 編輯治理標籤]** 在右側邊欄中。

![從「 」中選取欄位 [!UICONTROL 標籤] 標籤](../images/tutorials/labels/select-field-on-labels-tab.png)

若要編輯整個結構描述的標籤，請選取鉛筆圖示(![](../images/tutorials/labels/pencil-icon.png))的資料夾中，資料夾位於資料夾的 **[!UICONTROL 標籤]** 標籤。

![從以下專案選取結構描述名稱： [!UICONTROL 標籤] 標籤](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>當您首次嘗試編輯結構描述或欄位的標籤時，會出現免責宣告訊息，說明標籤使用方式如何根據您組織的原則影響下游作業。 選取 **[!UICONTROL 繼續]** 以繼續編輯。
>
>![標籤使用免責宣告](../images/tutorials/labels/disclaimer.png)

## 編輯結構描述或欄位的標籤

會出現一個對話方塊，可讓您編輯所選欄位的標籤。 如果您選取了個別的物件型別欄位，右側欄會列出套用標籤將傳播到的子欄位。

![已選取的欄位已顯示](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>如果您正在編輯整個結構描述的欄位，右側邊欄不會列出適用的欄位，而是顯示結構描述名稱。

使用顯示的清單來選取您要新增到結構描述或欄位的標籤。 選擇標籤後， **[!UICONTROL 套用的標籤]** 區段更新以顯示目前為止已選取的標籤。

![顯示套用的標籤](../images/tutorials/labels/applied-labels.png)

若要依型別篩選顯示的標籤，請在左側邊欄中選取所需的類別。 若要建立新的自訂標籤，請選取 **[!UICONTROL 建立標籤]**.

![篩選顯示的標籤或建立新標籤](../images/tutorials/labels/filter-and-create-custom.png)

在您對所選標籤滿意後，請選取 **[!UICONTROL 儲存]** 以將其套用至欄位或結構描述。

![儲存選取的標籤](../images/tutorials/labels/save-labels.png)

此 **[!UICONTROL 標籤]** 標籤會重新出現，顯示結構描述已套用的標籤。

![已套用欄位標籤](../images/tutorials/labels/field-labels-added.png)

## 后续步骤

本指南說明如何管理結構描述和欄位的資料使用標籤。 如需有關管理資料使用標籤的資訊，包括如何將其新增到特定資料集而不是結構描述層級，請參閱 [資料使用標籤UI指南](../../data-governance/labels/user-guide.md).
