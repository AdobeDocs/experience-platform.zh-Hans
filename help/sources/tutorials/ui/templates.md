---
description: 瞭解如何在Adobe Experience Platform UI中使用範本，以加速B2B資料的資料擷取程式。
title: 在UI中使用範本建立來源資料流
badge1: "Beta"
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: 91d6832231d75c9dd23e91a5f1152eac61558fc5
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 9%

---

# 在UI中使用範本建立來源資料流

>[!IMPORTANT]
>
>範本為測試版，並受到下列來源支援：
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>檔案和功能可能會有所變更。

Adobe Experience Platform提供預先設定的範本，可用來加速資料擷取程式。 範本包括自動產生的資產，例如結構描述、資料集、身分、對應規則、身分名稱空間和資料流程，您可以從來源將資料帶入Experience Platform時使用這些資產。

使用範本時，您可以：

* 透過加速範本化資產的建立，縮短內嵌的價值實現時間。
* 將手動資料擷取過程中可能發生的錯誤減到最少。
* 隨時更新自動產生的資產，以符合您的使用案例。

下列教學課程提供如何在Platform UI中使用範本的步驟。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 在Platform UI中使用範本 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="选择业务类型"
>abstract="为您的用例选择适当的业务类型。您的访问权限可能因 Real-Time Customer Data Platform 订阅帐户而异。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hans" text="Real-Time CDP 概述"

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 並檢視Experience Platform中可用的來源目錄。

使用 *[!UICONTROL 類別]* 功能表，依類別篩選來源。 或者，在搜尋列中輸入來源名稱，從目錄中尋找特定來源。

前往 [!UICONTROL Adobe應用程式] 類別以檢視 [!DNL Marketo Engage] 來源卡片，然後選取 [!UICONTROL 新增資料] 以開始。

![反白顯示Marketo Engage來源的來源工作區目錄。](../../images/tutorials/templates/catalog.png)

此時會出現一個快顯視窗，提供您瀏覽範本或使用現有結構描述和資料集的選項。

* **瀏覽範本**：來源範本會為您自動建立具有對應規則的結構描述、身分、資料集和資料流程。 您可以視需要自訂這些資產。
* **使用我現有的資產**：使用您建立的現有資料集和結構描述擷取您的資料。 您也可以視需要建立新的資料集和結構描述。

若要使用自動產生的資產，請選取 **[!UICONTROL 瀏覽範本]** 然後選取 **[!UICONTROL 選取]**.

![包含瀏覽範本或使用現有資產的選項的快顯視窗。](../../images/tutorials/templates/browse-templates.png)

### 身份验证

驗證步驟隨即顯示，提示您建立新帳戶或使用現有帳戶。

>[!BEGINTABS]

>[!TAB 使用現有帳戶]

若要使用現有帳戶，請選取 [!UICONTROL 現有帳戶] ，然後從顯示的清單中選取您要使用的帳戶。

![現有帳戶的選擇頁面，其中包含您可以存取的現有帳戶清單。](../../images/tutorials/templates/existing-account.png)

>[!TAB 建立新帳戶]

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供您的來源連線詳細資料和帳戶驗證認證。 完成後，選取 **[!UICONTROL 連線到來源]** 並留出時間建立新連線。

![具有來源連線詳細資料和帳戶驗證認證的新帳戶的驗證頁面。](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### 選取範本

根據您選取的企業型別，會出現範本清單。 選取預覽圖示 ![預覽圖示](../../images/tutorials/templates/preview-icon.png) 範本名稱旁邊，用來預覽範本中的範例資料。

![反白顯示預覽圖示的範本清單。](../../images/tutorials/templates/templates.png)

預覽視窗會出現，供您瀏覽及檢查範本中的範例資料。 完成後，選取 **[!UICONTROL 明白]**.

![預覽範例資料視窗。](../../images/tutorials/templates/preview-sample-data.png)

接下來，從清單中選取您要使用的範本。 您可以選取多個範本，一次建立多個資料流。 不過，每個帳戶只能使用一次範本。 選取範本後，請選取 **[!UICONTROL 完成]** 並稍候片刻讓資產產生。

如果您從可用範本清單中選取一個或部分專案，仍會產生所有B2B結構描述和身分識別名稱空間，以確保跨結構描述的B2B關係已正確設定。

>[!NOTE]
>
>已使用的範本將從選擇中停用。

![已選取商機連絡人角色範本的範本清單。](../../images/tutorials/templates/select-template.png)

### 設定排程

此 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce] 兩個來源都支援排程資料流程。

使用排程介面來設定資料流的擷取排程。 將您的擷取頻率設為 **一次** 以建立一次性內嵌。

![Dynamics和Salesforce範本的排程介面。](../../images/tutorials/templates/schedule.png)

或者，您也可以將擷取頻率設為 **分鐘**， **小時**， **日**，或 **周**. 如果排程資料流進行多次擷取，則必須設定間隔，以建立每次擷取之間的時間範圍。 例如，擷取頻率設為 **小時** 而間隔設定為 **15** 代表您的資料流已排程擷取資料間隔 **15小時**.

在此步驟中，您也可以啟用 **回填** 和定義資料增量擷取的欄。 回填是用來擷取歷史資料，而您為增量擷取定義的欄則允許將新資料與現有資料區分開來。

完成擷取排程的設定後，請選取 **[!UICONTROL 完成]**.

![已啟用回填的Dynamics和Salesforce範本排程介面。](../../images/tutorials/templates/backfill.png)

### 檢閱資產 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="查看自动生成的资产"
>abstract="生成所有资产最多需要五分钟时间。如果您选择离开页面，在生成完资产后，将向您发送通知以返回页面。您可以在资产生成后查看资产，并随时对数据流进行其他配置。"

此 [!UICONTROL 檢閱範本資產] 頁面會顯示作為範本的一部分自動產生的資產。 您可以在此頁面檢視與來源連線相關聯的自動產生結構描述、資料集、身分名稱空間和資料流程。 生成所有资产最多需要五分钟时间。如果您选择离开页面，在生成完资产后，将向您发送通知以返回页面。您可以在资产生成后查看资产，并随时对数据流进行其他配置。

根據預設，自動產生的資料流會設定為草稿狀態，以允許進一步自訂設定，例如對應規則或排程頻率。 選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 預覽對應]** 檢視為草稿資料流建立的對應集。

![已選取預覽對應選項的下拉式視窗。](../../images/tutorials/templates/preview.png)

會出現預覽頁面，讓您檢查來源資料欄位和目標結構描述欄位之間的對應關係。 檢視資料流的對應後。 選取 **[!UICONTROL 知道了。]**

![對應預覽視窗。](../../images/tutorials/templates/preview-mappings.png)

您可在執行後隨時更新資料流程。 選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 更新資料流]**. 您會進入來源工作流程頁面，您可以在此頁面更新資料流詳細資訊，包括部分擷取、錯誤診斷和警報通知的設定，以及資料流的對應。

您可以使用結構描述編輯器檢視來更新自動產生的結構描述。 瀏覽指南： [使用結構描述編輯器](../../../xdm/tutorials/create-schema-ui.md) 以取得詳細資訊。

![已選取更新資料流選項的下拉式視窗。](../../images/tutorials/templates/update.png)

>[!TIP]
>
>您可以透過以下方式存取草稿資料流： [!UICONTROL 資料流] 「來源」工作區中的「目錄」頁面。 選取 **[!UICONTROL 資料流]** 從頂端標題中，然後從清單中選取您要更新的資料流。
>
>![來源工作區資料流目錄中的現有資料流清單。](../../images/tutorials/templates/dataflows.png)

### 發佈您的資料流

透過來源工作流程開始發佈程式。 在您選取之後 [!UICONTROL 更新資料流]，您會前往 *[!UICONTROL 新增資料]* 工作流程的步驟。 選取 **[!UICONTROL 下一個]** 以繼續進行。

![草稿資料流的新增資料步驟](../../images/tutorials/templates/continue-draft.png)

接下來，確認您的資料流詳細資料，並設定錯誤診斷、部分擷取和警報通知的設定。 完成後，選取 **[!UICONTROL 下一個]**.

![草稿資料流的資料流詳細資料步驟。](../../images/tutorials/templates/dataflow-detail.png)

>[!NOTE]
>
>您可以選取 **[!UICONTROL 另存為草稿]** 隨時停止並儲存您對資料流所做的變更。

對應步驟隨即出現。 在此步驟中，您可以重新設定資料流的對應設定。 如需用於對應的資料準備功能的完整指南，請造訪 [資料準備UI指南](../../../data-prep/ui/mapping.md).

![草稿資料流的對應步驟。](../../images/tutorials/templates/mapping.png)

最後，檢閱資料流的詳細資訊，然後選取 **[!UICONTROL 儲存並擷取]** 以發佈您的草稿。

![草稿資料流的稽核步驟。](../../images/tutorials/templates/review.png)

## 后续步骤

依照本教學課程所述，您現在已使用範本建立資料流，以及結構描述、資料集和身分識別名稱空間等資產。 如需來源的一般資訊，請瀏覽 [來源概觀](../../home.md).

## 警示和通知 {#alerts-and-notifications}

Adobe Experience Platform警報支援範本，您可以使用通知面板來接收資產狀態的更新，並導覽回檢閱頁面。

選取Platform UI頂端標題的通知圖示，然後選取狀態警報以檢視您要檢閱的資產。

![Platform UI中的通知面板，會醒目提示警示失敗資料流的通知。](../../images/tutorials/templates/notifications.png)

您可以更新範本的警報設定，以接收有關資料流狀態的電子郵件和平台內通知。 如需設定警示的詳細資訊，請閱讀以下指南： [如何訂閱來源資料流的警示](../ui/alerts.md).