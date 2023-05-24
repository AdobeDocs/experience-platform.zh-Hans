---
title: Adobe Experience Platform Web SDK擴充功能中的資料元素型別
description: 瞭解Adobe Experience Platform Web SDK標籤擴充功能所提供的各種資料元素型別。
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# 数据元素类型

在您設定您的 [動作型別](action-types.md) 在 [Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md)，您必須設定資料元素型別。 此頁面說明可用的資料元素型別。

## 事件合併ID {#event-merge-id}

此数据元素在使用时提供事件合并 ID。此数据元素无需配置。在訪客離開頁面或 **[!UICONTROL 重設事件合併ID]** 動作型別已使用。

## 身分對應 {#identity-map}

身分對應可讓您為網頁的訪客建立身分識別。 身分對應由名稱空間組成，例如 _電話_ 或 _電子郵件_，每個名稱空間都包含一或多個識別碼。 例如，若您網站上的個人已提供兩個電話號碼，則您的電話名稱空間應包含兩個識別碼。

在 [!UICONTROL 身分對應] 資料元素中，您會針對每個識別碼提供下列資訊：

* **[!UICONTROL ID]**：識別訪客的值。 例如，如果識別碼屬於 _電話_ 名稱空間， [!UICONTROL ID] 可以是 _555-555-5555_. 此值通常衍生自頁面上的JavaScript變數或一些其他資料片段，因此最好建立參照頁面資料的資料元素，然後參照中的資料元素 [!UICONTROL ID] 內的欄位 [!UICONTROL 身分對應] 資料元素。 如果您在頁面上執行時，ID值不是填入的字串，則識別碼會自動從身分對應中移除。
* **[!UICONTROL 已驗證狀態]**：指出訪客是否已驗證的選取範圍。
* **[!UICONTROL 主要]**：指出識別碼是否應作為個人的主要識別碼的選擇。 如果沒有識別碼標示為主要，系統會使用ECID作為主要識別碼。

![顯示「編輯資料元素」畫面的UI影像。](./assets/identity-map-data-element.png)

您不應提供 [!DNL ECID] 建置身分對應時。 使用SDK時， [!DNL ECID] 會在伺服器上自動產生，並包含在身分對應中。

身分對應資料元素通常會與 [[!UICONTROL XDM物件] 資料元素型別](#xdm-object) 和 [[!UICONTROL 設定同意] 動作型別](action-types.md#set-consent).

深入瞭解 [Adobe Experience Platform Identity Service](../../identity-service/home.md).

## XDM物件 {#xdm-object}

使用XDM物件資料元素將資料格式化為XDM會更容易。 首次打开此数据元素时，请选择正确的 Adobe Experience Platform 沙箱和架构。選取結構描述後，您會看到結構描述的結構，您可輕鬆填寫。

![顯示XDM物件結構的UI影像。](assets/XDM-object.png)

請注意，當您開啟結構描述的特定欄位時，例如 `web.webPageDetails.URL`，則會自動收集某些專案。 即使自動收集了數個專案，您仍可視需要覆寫任何專案。 所有值都可以手动填写或使用其他数据元素进行填写。

>[!NOTE]
>
>僅填入您想收集的資訊片段。 將資料傳送至解決方案時，會忽略未填寫的專案。

## （測試版）變數 {#variable}

>[!IMPORTANT]
>
>此為目前的Beta版功能，可能會有變動。 未來版本可能包含重大變更。

建立XDM物件的另一種方法是使用 **[!UICONTROL 變數]** 資料元素。 而XDM物件資料元素是在參考時建立的，例如在 `sendEvent` 命令， **[!UICONTROL 變數]** 資料元素可以透過以下方式更新： [!UICONTROL 更新變數] 動作。 若要使用資料元素，請選取正確的Adobe Experience Platform沙箱和結構描述。

![UI影像顯示「建立資料元素」畫面。](assets/variable-data-element.png)

建立此資料元素後，您就可以使用 [更新變數](./action-types.md#update-variable) 修改資料元素的動作。 然後在「傳送事件」動作中，對XDM選項使用變數資料元素。

## 后续步骤 {#next-steps}

瞭解特定使用案例，例如 [存取ECID](accessing-the-ecid.md).
