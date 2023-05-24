---
title: 在UI中建立Marketo Engage來源連線和資料流
description: 本教學課程提供在UI中建立Marketo Engage來源連線和資料流的步驟，以便將B2B資料引進Adobe Experience Platform。
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: b271d28677543f773fe1ba471fc08574e7c5542b
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# 建立 [!DNL Marketo Engage] UI中的來源連線和資料流

>[!IMPORTANT]
>
>建立之前 [!DNL Marketo Engage] 來源連線和資料流，您必須先確定 [已對應您的Adobe組織ID](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html?lang=en) 在 [!DNL Marketo]. 此外，您也必須確保已完成 [自動填入 [!DNL Marketo] B2B名稱空間和結構描述](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) 建立來源連線和資料流之前。

本教學課程提供建立 [!DNL Marketo Engage] (以下稱&quot;[!DNL Marketo]&quot;) UI中的來源聯結器，可將B2B資料帶入Adobe Experience Platform。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [B2B名稱空間和結構描述自動產生公用程式](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md)：B2B名稱空間和結構描述自動產生公用程式可讓您使用 [!DNL Postman] 自動產生B2B名稱空間和結構描述的值。 您必須先完成B2B名稱空間和結構描述，才能建立 [!DNL Marketo] 來源連線和資料流。
* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [體驗資料模型(XDM)](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [在UI中建立和編輯結構描述](../../../../../xdm/ui/resources/schemas.md)：瞭解如何在UI中建立和編輯結構描述。
* [身分名稱空間](../../../../../identity-service/namespaces.md)：身分名稱空間是元件 [!DNL Identity Service] 做為身分識別相關內容的指示器。 完整身分包含ID值和名稱空間。
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

為了存取您的 [!DNL Marketo] account on Platform，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID是特定識別碼的唯一識別碼 [!DNL Marketo] 執行個體。 |
| `clientId` | 您的唯一使用者端ID [!DNL Marketo] 執行個體。 |
| `clientSecret` | 您專屬的唯一使用者端密碼 [!DNL Marketo] 執行個體。 |

如需取得這些值的詳細資訊，請參閱 [[!DNL Marketo] 驗證指南](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

收集完所需的認證後，您可以依照下一節中的步驟操作。

## 連線您的 [!DNL Marketo] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL Adobe應用程式] 類別，選取 **[!UICONTROL Marketo Engage]**. 然後，選取 **[!UICONTROL 新增資料]** 以建立新的 [!DNL Marketo] 資料流。

![目錄](../../../../images/tutorials/create/marketo/catalog.png)

此 **[!UICONTROL 連線Marketo Engage帳戶]** 頁面便會顯示。 您可以在此頁面使用新帳戶或存取現有帳戶。

### 現有帳戶

若要使用現有帳戶建立資料流，請選取「 」 **[!UICONTROL 現有帳戶]** 然後選取 [!DNL Marketo] 您要使用的帳戶。 選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/marketo/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供帳戶名稱、選擇性說明，以及 [!DNL Marketo] 驗證認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/marketo/new.png)

## 选择数据集

建立您的 [!DNL Marketo] 帳戶，下一個步驟會提供介面供您探索 [!DNL Marketo] 資料集。

介面的左半部分是目錄瀏覽器，顯示10 [!DNL Marketo] 資料集。 功能齊全的 [!DNL Marketo] 來源連線需要擷取9個不同的資料集。 如果您也使用 [!DNL Marketo] 帳戶型行銷(ABM)功能，則您還必須建立第10個資料流以擷取 [!UICONTROL 具名帳戶] 資料集。

>[!NOTE]
>
>為了簡單起見，下列教學課程使用 [!UICONTROL 機會] 例如，以下概述的步驟適用於下列10個步驟中的任一個 [!DNL Marketo] 資料集。

選取您要先擷取的資料集，然後選取「 」 **[!UICONTROL 下一個]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## 提供資料流詳細資料 {#provide-dataflow-details}

此 [!UICONTROL 資料流詳細資料] 頁面可讓您選取要使用現有資料集還是新資料集。 在此程式中，您也可以為以下專案進行設定： [!UICONTROL 設定檔資料集]， [!UICONTROL 錯誤診斷]， [!UICONTROL 部分擷取]、和 [!UICONTROL 警報].

![資料流 — 詳細資料](../../../../images/tutorials/create/marketo/dataflow-details.png)

>[!BEGINTABS]

>[!TAB 使用現有的資料集]

若要將資料內嵌至現有資料集，請選取「 」 **[!UICONTROL 現有資料集]**. 您可以使用來擷取現有的資料集 [!UICONTROL 進階搜尋] 選項，或是透過在下拉式選單中捲動現有資料集清單的方式。 選取資料集後，請為資料流提供名稱和說明。

![existing-data](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!TAB 使用新資料集]

若要內嵌至新資料集，請選取「 」 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選擇性說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項或透過捲動下拉式選單中的現有結構描述清單的方式。 選取結構描述後，請為資料流提供名稱和說明。

![新資料集](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!ENDTABS]

### 啟用 [!DNL Profile] 和錯誤診斷

接下來，選取 **[!UICONTROL 設定檔資料集]** 切換以啟用您的資料集 [!DNL Profile]. 這可讓您建立實體屬性和行為的整體檢視。 來自所有人的資料 [!DNL Profile] — 啟用的資料集將包含在 [!DNL Profile] 和變更會在您儲存資料流時套用。

[!UICONTROL 錯誤診斷] 針對資料流中發生的任何錯誤記錄，啟用詳細的錯誤訊息產生，同時 [!UICONTROL 部分擷取] 可讓您擷取包含錯誤的資料，最多可擷取您手動定義的特定臨界值。 請參閱 [部分批次擷取概觀](../../../../../ingestion/batch-ingestion/partial.md) 以取得詳細資訊。

>[!IMPORTANT]
>
>此 [!DNL Marketo] 來源會使用批次擷取來擷取所有歷史記錄，並使用串流擷取來即時更新。 這可讓來源在擷取任何錯誤記錄時繼續串流。 啟用 **[!UICONTROL 部分擷取]** 切換，然後設定 [!UICONTROL 錯誤臨界值%] 達到最大值，以防止資料流失敗。

![設定檔與錯誤](../../../../images/tutorials/create/marketo/profile-and-errors.png)

### 啟用警示

您可以啟用警報以接收有關資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱來源警報](../../alerts.md).

當您完成提供詳細資訊給資料流時，請選取「 」 **[!UICONTROL 下一個]**.

![警報](../../../../images/tutorials/create/marketo/alerts.png)

### 擷取公司資料時略過無人認領的帳戶

建立資料流以從公司資料集中擷取資料時，您可以設定 [!UICONTROL 排除無人認領的帳戶] 從內嵌中排除或包含無人認領的帳戶。

當個人填寫表單時， [!DNL Marketo] 根據不含其他資料的公司名稱建立虛擬帳戶記錄。 對於新資料流，預設會啟用排除無人認領帳戶的切換。 對於現有資料流，您可以啟用或停用該功能，而變更會套用至新擷取的資料，而非現有資料。

![無人認領的帳戶](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## 對應您的 [!DNL Marketo] 資料集來源欄位至目標XDM欄位

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

每個 [!DNL Marketo] 資料集有其專屬的對應規則可遵循。 如需如何對應的詳細資訊，請參閱下列內容 [!DNL Marketo] 資料集至XDM：

* [活动](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [项目](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [計畫成員資格](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [公司](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [靜態清單](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [靜態清單成員資格](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [具名帳戶](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [機會](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [機會聯絡人角色](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [人員](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應介面的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

![對應](../../../../images/tutorials/create/marketo/mapping.png)

對應集準備就緒後，請選取 **[!UICONTROL 下一個]** 並留出一些時間，以便建立新的資料流。

## 檢閱您的資料流

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源實體的相關路徑，以及該來源實體中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取 **[!UICONTROL 儲存並擷取]** 並留出一些時間來建立資料流。

![檢閱](../../../../images/tutorials/create/marketo/review.png)

## 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視有關擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請參閱以下教學課程： [在UI中監控資料流](../../../../../dataflows/ui/monitor-sources.md).

## 刪除您的屬性

資料集中的自訂屬性無法回溯隱藏或移除。 如果您想要從現有資料集中隱藏或移除自訂屬性，則必須建立不含此自訂屬性的新資料集、新的XDM結構描述，並為您建立的新資料集設定新的資料流。 您也必須停用或刪除原始資料流，該資料流包含您要隱藏或移除自訂屬性的資料集。

## 刪除您的資料流

您可以刪除不再必要或已使用建立錯誤的資料流 **[!UICONTROL 刪除]** 函式位於 [!UICONTROL 資料流] 工作區。 如需如何刪除資料流的詳細資訊，請參閱以下教學課程： [在UI中刪除資料流](../../delete.md).

## 后续步骤

依照本教學課程所述，您已成功建立資料流以引入 [!DNL Marketo] 資料。 傳入資料現在可供下游平台服務使用，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概述](/help/profile/home.md)
* [[!DNL Data Science Workspace] 概述](/help/data-science-workspace/home.md)

## 附录 {#appendix}

以下小節提供您在使用時，可能會遵循的其他准則 [!DNL Marketo] 來源。

### UI中的錯誤訊息 {#error-messages}

當Platform偵測到您的設定發生問題時，UI中會顯示下列錯誤訊息：

#### [!DNL Munchkin ID] 未對應至適當的組織

如果您 [!DNL Munchkin ID] 未對應至您正在使用的平台組織。 設定以下專案之間的對應： [!DNL Munchkin ID] 以及您的組織使用 [[!DNL Marketo] 介面](https://app-sjint.marketo.com/#MM0A1).

![錯誤訊息顯示Marketo執行個體未正確對應至Adobe組織。](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### 缺少主要身分

如果缺少主要身分，資料流將無法儲存和擷取。 確定 [您的XDM結構描述中存在主要身分](../../../../../xdm/tutorials/create-schema-ui.md)，然後再嘗試設定資料流。

![錯誤訊息顯示XDM結構描述中缺少主要身分。](../../../../images/tutorials/create/marketo/no-primary-identity.png)

