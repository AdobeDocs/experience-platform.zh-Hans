---
title: 中繼畫素延伸功能概述
description: 瞭解Adobe Experience Platform中的Meta Pixel標籤擴充功能。
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] 擴充功能概觀

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) 是以JavaScript為基礎的分析工具，可讓您追蹤網站上的訪客活動。 您追蹤的訪客動作（稱為轉換）會傳送至 [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) 可用於衡量廣告、行銷活動、轉換漏斗等專案的成效。

此 [!DNL Meta Pixel] 標籤擴充功能可讓您善用 [!DNL Pixel] 使用者端標籤程式庫中的功能。 本文介紹如何安裝擴充功能，以及在 [規則](../../../ui/managing-resources/rules.md).

## 先决条件

為了使用擴充功能，您必須具備有效的 [!DNL Meta] 有權存取的帳戶 [!DNL Ads Manager]. 具體而言，您必須 [建立新的 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) 並複製其 [!DNL Pixel ID] 以便讓擴充功能可設定至您的帳戶。 如果您已有 [!DNL Meta Pixel]，您可以改用其ID。

強烈建議使用 [!DNL Meta Pixel] 與 [!DNL Meta Conversions API] 分別從使用者端和伺服器端共用和傳送相同的事件，因為這有助於復原未擷取的事件 [!DNL Meta Pixel]. 請參閱 [[!DNL Meta Conversions API] 事件轉送的擴充功能](../../client/meta/overview.md) 瞭解如何在伺服器端實作中整合該軟體的步驟。 請注意，您的組織必須擁有下列專案的存取權： [事件轉送](../../../ui/event-forwarding/overview.md) 以使用伺服器端擴充功能。

## 安裝擴充功能

若要安裝 [!DNL Meta Pixel] 擴充功能，導覽至資料收集UI或Experience PlatformUI並選取 **[!UICONTROL 標籤]** 從左側導覽列中。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，選取 **[!UICONTROL 擴充功能]** 在左側導覽中，然後選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL 中繼畫素] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕已選取 [!UICONTROL 中繼畫素] 資料收集UI中的擴充功能。](../../../images/extensions/client/meta/install.png)

在出現的組態檢視中，您必須提供 [!DNL Pixel] 您先前複製的ID可將擴充功能連結至您的帳戶。 您可以直接將ID貼到輸入中，也可以改為選取現有的資料元素。

>[!TIP]
>
>使用資料元素可讓您選擇動態變更 [!DNL Pixel] 使用的ID取決於其他因素，例如組建環境。 請參閱附錄中關於 [使用不同的 [!DNL Pixel] 適用於不同環境的ID](#id-data-element) 以取得詳細資訊。

您也可以選擇提供事件ID以與擴充功能建立關聯。 此專案用於去除重複相同事件，介於 [!DNL Meta Pixel] 和 [!DNL Meta Conversions API]. 如需詳細資訊，請參閱以下小節： [事件重複資料刪除](../../server/meta/overview.md#event-deduplication) 在總覽中 [!DNL Conversions API] 副檔名。

完成後，選取 **[!UICONTROL 儲存]**

![此 [!DNL Pixel] 在擴充功能組態檢視中作為資料元素提供的ID。](../../../images/extensions/client/meta/configure.png)

擴充功能已安裝，您現在可以在標籤規則中運用其各種動作。

## 設定標籤規則 {#rule}

[!DNL Meta Pixel] 接受一組預先定義的 [標準事件](https://www.facebook.com/business/help/402791146561655)，每個檔案都有其專屬的內容和已接受的屬性。 規則動作由 [!DNL Pixel] 擴充功能與這些事件型別相關聯，可讓您輕鬆分類及設定要傳送至的事件 [!DNL Meta] 根據其型別而定。

為了示範，本節說明如何建立將頁面檢視事件傳送至的規則 [!DNL Meta].

開始建立新標籤規則，並視需要設定其條件。 選取規則的動作時，選取 **[!UICONTROL 中繼畫素]** 針對擴充功能，然後選取「 」 **[!UICONTROL 傳送頁面檢視]** （動作型別）。

![此 [!UICONTROL 傳送頁面檢視] 為資料收集UI中的規則選取的動作型別。](../../../images/extensions/client/meta/select-action.png)

不需要進一步設定 [!UICONTROL 傳送頁面檢視] 動作。 選取 **[!UICONTROL 保留變更]** 以將動作新增至規則設定。 如果您對規則滿意，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新標籤 [建置](../../../ui/publishing/builds.md) 以啟用程式庫的變更。

## 確認 [!DNL Meta] 正在接收資料

將更新的組建部署到您的網站後，您可以在瀏覽器上產生一些轉換事件，並檢查這些事件是否出現在中，以確認資料是否按預期傳送 [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## 后续步骤

本指南說明如何將資料傳送至 [!DNL Meta] 使用 [!DNL Meta Pixel] 標籤延伸。 如果您也打算將伺服器端事件傳送至 [!DNL Meta]，您現在可以繼續安裝並設定 [[!DNL Conversions API] 事件轉送擴充功能](../../server/meta/overview.md).

如需Experience Platform中標籤的詳細資訊，請參閱 [標籤總覽](../../../home.md).

## 附錄：使用不同的 [!DNL Pixel] 適用於不同環境的ID {#id-data-element}

如果您想在開發或預備環境中測試實施，同時保留您的生產環境 [!DNL Meta Pixel] analytics完整無缺，您可以使用資料元素來動態選擇適當的 [!DNL Pixel] ID取決於使用的環境。

您可以使用來達成此目的 [!UICONTROL 自訂程式碼] 資料元素(由 [[!UICONTROL 核心] 擴充功能](../core/overview.md))與 [`turbine` 自由變數](../../../extension-dev/turbine.md). 在資料元素的JavaScript程式碼中，使用 `turbine` 物件以尋找目前的環境階段，然後傳回適當的 [!DNL Pixel] 根據結果的ID。

以下範例會傳回假的生產ID `exampleProductionKey` 在生產環境中使用時，以及不同的ID `exampleTestKey` 使用任何其他環境時。 實作此程式碼時，請將每個值取代為您實際的生產和測試 [!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
