---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 如何設定計算屬性欄位
type: Documentation
description: 計算屬性是用來將事件層級資料彙總到設定檔層級屬性的函式。 若要設定計算屬性，您必須先識別將儲存計算屬性值的欄位。 您可以使用結構描述欄位群組來建立此欄位，以將欄位新增至現有結構描述，或選取您已在結構描述中定義的欄位。
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alpha)在UI中設定計算屬性欄位

>[!IMPORTANT]
>
>計算屬性功能目前為Alpha版，並非所有使用者都可使用。 文档和功能可能会发生变化。

若要設定計算屬性，您必須先識別將儲存計算屬性值的欄位。 您可以使用結構描述欄位群組來建立此欄位，以將欄位新增至現有結構描述，或選取您已在結構描述中定義的欄位。

>[!NOTE]
>
>運算屬性無法新增至Adobe定義的欄位群組中的欄位。 欄位必須位於 `tenant` 名稱空間，這表示它必須是您定義並新增到結構描述的欄位。

為了成功定義計算屬性欄位，結構描述必須啟用 [!DNL Profile] 和會作為結構描述所依據之類別的聯合結構描述的一部分出現。 如需詳細資訊，請參閱 [!DNL Profile] — 啟用的結構描述和聯合，請檢閱 [!DNL Schema Registry] 開發人員指南章節於 [為設定檔啟用結構描述並檢視聯合結構描述](../../xdm/api/getting-started.md). 也建議檢閱 [關於聯合的區段](../../xdm/schema/composition.md) 結構描述組合基本資料檔案中。

本教學課程中的工作流程使用 [!DNL Profile]-enabled結構描述，並遵循定義包含計算屬性欄位的新欄位群組，以及確保它是正確名稱空間的步驟。 如果您的欄位在啟用設定檔的結構描述中位於正確的名稱空間，您可以直接進入的步驟 [建立計算屬性](#create-a-computed-attribute).

## 檢視結構描述

後續步驟使用Adobe Experience Platform使用者介面來尋找結構、新增欄位群組和定義欄位。 如果您偏好使用 [!DNL Schema Registry] API，請參閱 [Schema Registry開發人員指南](../../xdm/api/getting-started.md) 如需如何建立欄位群組的步驟，請將欄位群組新增至結構描述，並啟用結構描述以用於 [!DNL Real-Time Customer Profile].

在使用者介面中，按一下 **[!UICONTROL 結構描述]** 左側邊欄中使用「 」搜尋列 **[!UICONTROL 瀏覽]** 索引標籤來快速尋找您要更新的結構描述。

![](../images/computed-attributes/Schemas-Browse.png)

找到結構描述後，按一下其名稱以開啟 [!DNL Schema Editor] 您可以在其中編輯結構描述。

![](../images/computed-attributes/Schema-Editor.png)

## 创建字段组

若要建立新的欄位群組，請按一下 **[!UICONTROL 新增]** 旁邊 **[!UICONTROL 欄位群組]** 在 **[!UICONTROL 組合]** 區段。 如此將可開啟 **[!UICONTROL 新增欄位群組]** 對話方塊，您可在其中檢視現有的欄位群組。 按一下選項按鈕 **[!UICONTROL 建立新欄位群組]** 以定義您的新欄位群組。

為欄位群組提供名稱和說明，然後按一下 **[!UICONTROL 新增欄位群組]** 完成時。

![](../images/computed-attributes/Add-field-group.png)

## 將計算屬性欄位新增至結構描述

您的新欄位群組現在應會顯示在「[!UICONTROL 欄位群組]「 」下的「 」區段[!UICONTROL 組合]「。 按一下欄位群組的名稱，然後按多個 **[!UICONTROL 新增欄位]** 按鈕將顯示在 **[!UICONTROL 結構]** 區段。

選取 **[!UICONTROL 新增欄位]** 在結構描述名稱旁邊，以新增頂層欄位，或者您可以選取將欄位新增到您偏好的結構描述內的任何位置。

按一下 **[!UICONTROL 新增欄位]** 新物件隨即開啟，以您的租使用者ID命名，表示欄位位於正確的名稱空間。 在該物件中， **[!UICONTROL 新欄位]** 出現。 如果您要在其中定義計算屬性的欄位，就會執行此動作。

![](../images/computed-attributes/New-field.png)

## 設定欄位

使用 **[!UICONTROL 欄位屬性]** 區段，提供新欄位的必要資訊，包括其名稱、顯示名稱和型別。

>[!NOTE]
>
>欄位的型別必須與計算屬性值相同。 例如，如果計算的屬性值是一個字串，則結構描述中定義的欄位必須是字串。

完成後，按一下 **[!UICONTROL 套用]** 和欄位的名稱及其型別將顯示在 **[!UICONTROL 結構]** 區段。

![](../images/computed-attributes/Apply.png)

## 為以下專案啟用結構描述 [!DNL Profile]

在繼續之前，請確定結構描述已啟用 [!DNL Profile]. 按一下以下位置中的結構描述名稱： **[!UICONTROL 結構]** 區段，以便 **[!UICONTROL 結構描述屬性]** 標籤隨即顯示。 如果 **[!UICONTROL 設定檔]** 滑桿為藍色，表示結構描述已啟用 [!DNL Profile].

>[!NOTE]
>
>啟用結構描述 [!DNL Profile] 無法復原，因此如果您在啟用後按一下滑桿，就不必冒險停用它。

![](../images/computed-attributes/Profile.png)

您現在可以按一下 **[!UICONTROL 儲存]** 以儲存更新的結構描述，並使用API繼續本教學課程的其餘部分。

## 后续步骤

現在您已建立要儲存計算屬性值的欄位，您可以使用 `/computedattributes` api端點。 如需在API中建立計算屬性的詳細步驟，請依照以下提供的步驟操作： [計算屬性API端點指南](ca-api.md).