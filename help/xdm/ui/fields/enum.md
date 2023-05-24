---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；列舉；欄位；
solution: Experience Platform
title: 在UI中定義列舉欄位和建議值
description: 瞭解如何在Experience Platform使用者介面中定義字串欄位的列舉和建議值。
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 8%

---

# 在UI中定義列舉和建議值 {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="枚举和建议值"
>abstract="**枚举**&#x200B;将字符串字段限制为仅允许提取与一组预定义值匹配的数据。可以为每个枚举限制分配一个&#x200B;**显示名称**，用于填充分段 UI 中的属性下拉列表。字段的&#x200B;**建议值**&#x200B;不限制提取，并且仅确定分段中显示的显示名称。如果您的多个架构共享一个属于公共类或字段组的字段，并且您在各个架构之间为该字段定义了不同的枚举或建议值，则这些值将合并和附加到联合架构中。"

在Experience Data Model (XDM)中，字串欄位可以獲得一組預先定義的接受或建議值，以更好地控制哪些值被擷取到該欄位中或它將在分段中如何表現。

**[!UICONTROL 列舉]** 將字串欄位可擷取的值限製為預先定義的集合。 如果您嘗試將資料內嵌至列舉欄位，但值不符合其設定中定義的任何值，則會拒絕內嵌。

相較於列舉， **[!UICONTROL 建議值]** 選項可讓您針對不限制其可內嵌值的字串欄位，表示一組建議值。 建議值反而會影響中可用的預先定義值 [區段UI](../../../segmentation/ui/overview.md) 將字串欄位納入為屬性時。

時間 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，並將型別設定為 [!UICONTROL 字串]，您可以選擇定義 [列舉](#enum) 或 [建議值](#suggested-values) 用於該欄位。

![此影像顯示UI中字串欄位已啟用列舉和建議值選項](../../images/ui/fields/enum/enum-options-selected.png)

本檔案說明如何在 [!UICONTROL 結構描述] UI工作區。 如需列舉和建議值的快速概覽（包括如何在UI中設定它們及其下游效果），請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## 定義列舉 {#enum}

選取 **[!UICONTROL 列舉值和建議值]**，然後選取 **[!UICONTROL 列舉]**. 會出現其他控制項，讓您指定列舉的值限制。 若要新增限制，請選取 **[!UICONTROL 新增列]**.

![顯示UI中選取的列舉選項的影像](../../images/ui/fields/enum/enum-add-row.png)

在 **[!UICONTROL 值]** 欄中，您必須提供想要強制欄位使用的確切值。 您可以選擇提供人性化的 **[!UICONTROL 顯示名稱]** 也會影響分段中值的呈現方式。

繼續使用 **[!UICONTROL 新增列]** 將所需的限制和選用標籤新增至列舉，或選取刪除圖示(![刪除圖示的影像](../../images/ui/fields/enum/remove-icon.png))來移除之前新增的列。 完成後，選取 **[!UICONTROL 套用]** 以將變更套用至結構描述。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/enum-confirm.png)

畫布會更新以反映變更。 當您日後探索此結構描述時，可以檢視並編輯右側邊欄中列舉欄位的限制。

## 定義建議值 {#suggested-values}

選取 **[!UICONTROL 列舉值和建議值]**，然後選取 **[!UICONTROL 建議值]** 讓其他控制項出現。 從此處選取 **[!UICONTROL 新增列]** 以開始新增建議值。

![顯示在UI中選取的建議值選項的影像](../../images/ui/fields/enum/suggested-add-row.png)

在 **[!UICONTROL 顯示名稱]** 欄中，為值提供您想在分段UI中顯示的好記名稱。 若要新增更多建議值，請選取 **[!UICONTROL 新增列]** 再次重複此程式，然後視需要重複此程式。 若要移除先前新增的列，請選取 ![刪除圖示](../../images/ui/fields/enum/remove-icon.png) 在相關列旁邊。

完成後，選取 **[!UICONTROL 套用]** 以將變更套用至結構描述。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>欄位更新的建議值大約會延遲5分鐘，才會反映在分段UI中。

### 管理標準欄位的建議值

標準XDM元件中的某些欄位包含自己的建議值，例如 `eventType` 從 [[!UICONTROL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 雖然您可以為標準欄位建立其他建議值，但無法修改或移除組織未定義的任何建議值。 在UI中檢視標準欄位時，其建議值會顯示，但為唯讀。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/suggested-standard.png)

若要為標準欄位新增建議值，請選取 **[!UICONTROL 新增列]**. 若要移除貴組織先前新增的建議值，請選取 ![刪除圖示](../../images/ui/fields/enum/remove-icon.png) 在相關列旁邊。

![此影像顯示UI中字串欄位填寫的列舉值和顯示名稱](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## 列舉和建議值的演化規則 {#evolution}

使用具有列舉欄位的結構描述將資料擷取到Platform後，對結構描述定義所做的任何進一步變更都必須符合系統中已存在的資料。 一般而言，對現有欄位進行的變更只能使該欄位生效 **更少** 限制性。 欄位的限制條件不能比現在嚴格。

如果是列舉和建議值，則下列規則適用於擷取後：

* 您 **可以** 使用現有的建議值為標準和自訂欄位新增建議值。
* 您 **可以** 從具有現有建議值的自訂欄位中移除建議值。
* 您 **可以** 為現有的自訂列舉欄位新增列舉值。
* 您 **可以** 將自訂欄位的列舉值切換為僅建議值，或將其轉換為沒有列舉或建議值的字串。 **此切換一旦套用即無法復原。**
* 您 **無法** 從標準欄位中移除列舉值或建議值。
* 您 **無法** 將列舉值新增至沒有現有列舉的欄位。
* 您 **無法** 移除自訂欄位的所有現有列舉值。
* 您 **無法** 從建議值切換為列舉。

## 合併列舉和建議值的規則 {#merging}

如果多個結構描述使用具有不同設定的相同列舉欄位，而這些結構描述包含在聯合中，則當談到如何協調列舉差異時，會套用某些規則。 確切的規則取決於參考相同標準欄位的結構描述(例如 `eventType`)或參照不同欄位群組中的相同自訂欄位路徑。

如果參考相同的標準欄位：

* 任何其他建議值包括 **已附加** 在聯合中。
* 對相同列舉索引鍵的建議值所做的更新如下 **已更新** 在聯合中。

如果參照不同欄位群組中的相同自訂欄位路徑：

* 任何其他建議值包括 **已附加** 在聯合中。
* 如果在多個結構描述中定義了相同的其他建議值，則這些值為 **已合併** 在聯合中。 換言之，相同的建議值在合併後不會出現兩次。

## 驗證限制

由於目前系統的限制，系統在內嵌期間未驗證列舉的情形有兩種：

1. 列舉定義於 [陣列欄位](./array.md).
1. 列舉在結構描述階層中定義了一個以上的層級。

## 后续步骤

本指南說明如何在UI中定義字串欄位的列舉和建議值。 有關如何使用Schema Registry API管理列舉和建議值的資訊，請參閱以下內容 [教學課程](../../tutorials/suggested-values.md).

若要瞭解如何在中定義其他XDM欄位型別 [!DNL Schema Editor]，請參閱概述，位於 [在UI中定義欄位](./overview.md#special).
