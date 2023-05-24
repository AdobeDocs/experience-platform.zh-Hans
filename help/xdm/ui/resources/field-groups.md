---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；欄位群組；欄位群組；
solution: Experience Platform
title: 在UI中建立和編輯結構描述欄位群組
description: 瞭解如何在Experience Platform使用者介面中建立和編輯結構描述欄位群組。
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 542ad49f475ac9586da506a8afa5408e83262121
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 在UI中建立和編輯結構描述欄位群組

在Experience Data Model (XDM)中，結構描述欄位群組是可重複使用的元件，可定義一或多個實作特定功能的欄位，例如個人詳細資料、飯店偏好設定或地址。 欄位群組旨在包含在實作相容類別的結構描述中。

欄位群組會根據欄位群組所代表的資料行為（記錄或時間序列），定義其相容的類別。 這表示並非所有欄位群組都可用於所有類別。

Adobe Experience Platform提供許多標準欄位群組，涵蓋廣泛的行銷使用案例。 不過，您也可以建立和編輯自己的自訂欄位群組，以在XDM結構描述中定義與您的業務相關的其他概念。 本指南概述如何在Platform UI中建立、編輯及管理貴組織的自訂欄位群組。

## 先决条件

本指南需要實際瞭解XDM系統。 請參閱 [XDM概觀](../../home.md) 介紹XDM在Experience Platform生態系統內的角色，以及 [結構描述組合基本概念](../../schema/composition.md) 瞭解欄位群組對XDM結構描述的貢獻。

雖然本指南不需要，但建議您也參閱以下主題的相關教學課程： [在UI中構成結構描述](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 建立新的欄位群組 {#create}

若要建立新的欄位群組，您必須先選取要新增該欄位群組的結構描述。 您可以選擇 [建立新結構描述](./schemas.md#create) 或 [選取要編輯的現有結構描述](./schemas.md#edit).

一旦您在中開啟結構描述後 [!DNL Schema Editor]，選取 **[!UICONTROL 新增]** 旁邊 [!UICONTROL 欄位群組] 區段。

![](../../images/ui/resources/field-groups/add-field-group.png)

在出現的對話方塊中，選取 **[!UICONTROL 建立新欄位群組]**. 您可以在此處提供 **[!UICONTROL 顯示名稱]** 和 **[!UICONTROL 說明]** （欄位群組）。 完成後，選取 **[!UICONTROL 新增欄位群組]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

此 [!DNL Schema Editor] 會重新出現，而新欄位群組會列在左側邊欄中。 由於這是全新的欄位群組，目前未提供任何欄位給結構描述，因此畫布保持不變。 您現在可以開始 [新增欄位至欄位群組](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## 編輯現有欄位群組 {#edit}

>[!NOTE]
>
>只有貴組織定義的自訂欄位群組才能完全編輯和自訂。 對於由Adobe定義的核心欄位群組，只能在個別結構描述的內容中編輯其欄位的顯示名稱。 請參閱以下小節： [編輯結構描述欄位的顯示名稱](./schemas.md#display-names) 以取得詳細資訊。
>
>儲存自訂欄位群組並在結構描述中使用以進行資料擷取後，之後只能對欄位群組進行附加變更。 請參閱 [結構描述演化規則](../../schema/composition.md#evolution) 以取得詳細資訊。

若要編輯現有的欄位群組，您必須先開啟採用下列欄位群組的結構描述： [!DNL Schema Editor]. 您可以 [選取要編輯的現有結構描述](./schemas.md#edit)，或您可以 [建立新結構描述](./schemas.md#create) 並新增相關欄位群組。

在編輯器中開啟結構描述後，您就可以開始 [新增欄位至欄位群組](#add-fields).

## 新增欄位至欄位群組 {#add-fields}

>[!NOTE]
>
>本節著重於新增欄位至自訂欄位群組。 有關如何將自訂欄位新增到標準欄位群組的資訊，請參閱 [結構描述UI指南](./schemas.md#custom-fields-for-standard-groups).

若要新增欄位至自訂欄位群組，請從選取 **加(+)** 圖示加以識別（位於畫布中的方案名稱旁）。

![](../../images/ui/resources/field-groups/add-field.png)

一個 **[!UICONTROL 未命名的欄位]** 預留位置會顯示在畫布中，而右邊欄會更新以顯示控制項來設定欄位的屬性。 請參閱指南： [在UI中定義欄位](../fields/overview.md#define) ，以瞭解如何設定不同欄位型別的具體步驟。

下 **[!UICONTROL 指派給]**，選取 **[!UICONTROL 欄位群組]** 選項，然後使用下拉式清單，從清單中選取所需的欄位群組。 您可以開始輸入欄位群組的名稱來縮小結果範圍。

![](../../images/ui/resources/field-groups/select-field-group.png)

下 **[!UICONTROL 指派給]**，選取 **[!UICONTROL 欄位群組]** 選項，然後使用下拉式清單，從清單中選取所需的欄位群組。 您可以開始輸入欄位群組的名稱來縮小結果範圍。

![](../../images/ui/resources/field-groups/select-field-group.png)

將欄位新增到結構描述後，就會將其指派給所選的欄位群組。 繼續將所需數量的欄位新增至欄位群組。 完成後，選取 **[!UICONTROL 儲存]** 以儲存結構描述和欄位群組。

![](../../images/ui/resources/field-groups/complete-field-group.png)

如果其他結構描述中已經使用了相同的欄位群組，則新新增的欄位會自動出現在這些結構描述中。

## 后续步骤

本指南說明如何使用Platform UI建立和編輯欄位群組。 如需功能的詳細資訊， [!UICONTROL 結構描述] 工作區，請參閱 [[!UICONTROL 結構描述] 工作區概觀](../overview.md).

若要瞭解如何使用管理欄位群組 [!DNL Schema Registry] API，請參閱 [欄位群組端點指南](../../api/field-groups.md).
