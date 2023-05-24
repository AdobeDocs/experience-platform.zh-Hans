---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用情況
title: 編輯結構描述以建立自訂儀表板Widget
description: 本指南逐步說明如何選取屬性和設定您組織的架構，為Adobe Experience Platform儀表板建立自訂Widget。
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 編輯結構描述以建立自訂Widget

若要建立Adobe Experience Platform儀表板的自訂Widget，您必須先識別Widget所根據的即時客戶設定檔屬性。

本指南透過選取屬性以建立自訂儀表板Widget，提供編輯組織架構的逐步指示。

選取屬性並設定結構描述後，您可以繼續下列步驟： [為您的儀表板建立自訂Widget](custom-widgets.md).

>[!NOTE]
>
>必須授予使用者「管理標準儀表板」許可權，才能編輯結構。 如需授予控制面板存取許可權的詳細步驟，請參閱 [儀表板許可權指南](../permissions.md).

## Widget資料庫 {#widget-library}

本指南需要存取 [!UICONTROL Widget資料庫] 在Experience Platform內。 若要進一步瞭解Widget程式庫，以及如何在UI中存取它，請從閱讀 [Widget程式庫概觀](widget-library.md).

## 编辑架构

在Widget程式庫中， **[!UICONTROL 自訂]** 索引標籤可讓您建立Widget並與您組織中的其他使用者共用，以自訂儀表板的外觀。

建立自訂Widget之前，必須選取「即時客戶設定檔」屬性，以確保資料包含在每日快照中。

>[!IMPORTANT]
>
>您的組織最多可以選取20個屬性。

如果您的組織尚未選取任何設定檔屬性，請從選取 **[!UICONTROL 設定]** 在熒幕中央。

![突出顯示「設定」之Widget程式庫工作區的「自訂」標籤。](../images/customization/configure-schema.png)

建立至少一個自訂屬性後，選取 **[!UICONTROL 編輯結構描述]** 以檢視選取的屬性並新增更多屬性。

![反白顯示「編輯」結構描述之Widget程式庫工作區的「自訂」索引標籤。](../images/customization/edit-schema.png)

## 選取屬性

若要選取中的屬性 **[!UICONTROL 選取聯合結構描述欄位]** 對話方塊，導覽至聯合結構描述中的屬性（或使用搜尋），並選取屬性旁的核取方塊。 選取核取方塊也會將屬性新增至 **[!UICONTROL 選取的屬性]** 清單顯示在對話方塊的右側。

>[!NOTE]
>
>若要讓屬性在選取時可見，它必須是下列其中一項： String、Date、Date-Time、Boolean、Short、Long、Integer或Byte。 不支援Map和Double資料型別，且為灰色，因此無法選取。

選擇您要新增的屬性後，選取 **[!UICONTROL 儲存]** 以儲存屬性並返回自訂Widget標籤。

>[!WARNING]
>重新整理資料時，新選取的屬性可在下一個每日快照後使用。

![用來選取結構描述屬性（具有屬性）和「儲存」的對話方塊會反白顯示。](../images/customization/select-attribute.png)

## 后续步骤

閱讀本指南後，您可以導覽至Widget程式庫，並選取「即時客戶個人檔案」屬性以設定您的結構。 選取設定檔屬性後，您就可以開始 [為您的儀表板建立自訂Widget](custom-widgets.md).
