---
keywords: Experience Platform；首頁；熱門主題；匯出；匯出
solution: Experience Platform
title: 在Privacy ServiceUI中管理隱私權工作
description: 瞭解如何使用Privacy Service使用者介面協調和監視各種Experience Cloud應用程式的隱私權請求。
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 14%

---

# 在Privacy ServiceUI中管理隱私權工作 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="遵守数据主体隐私请求"
>abstract="<h2>描述</h2><p>通过 Adobe Experience Platform Privacy Service，可代表要根据隐私法规访问或删除其个人数据的客户创建和管理隐私请求。</p>"

本檔案提供使用建立和管理隱私權請求的步驟。 [!DNL Privacy Service] 使用者介面。

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利請求。 不支援或不允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行負載測試，因為這是僅限生產的環境，且會建立有效隱私權請求的不必要待處理專案。
>
>現已設定每日硬性上傳限制，以防止服務被濫用。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與其舉行會議，討論其行動並討論可接受的Privacy Service用途。

## 瀏覽 [!DNL Privacy Service] UI儀表板

的儀表板 [!DNL Privacy Service] UI提供兩個Widget，可讓您檢視隱私權工作的狀態：「[!UICONTROL 狀態報告]「和」[!UICONTROL 工作請求]「。 控制面板也會針對顯示的作業顯示目前選取的規則。

![UI儀表板](../images/user-guide/dashboard.png)

### 法規型別

[!DNL Privacy Service] 支援數項隱私權法規的工作請求。 下表列出支援的法規及其在UI中表示的對應標籤：

| UI標籤 | 法規 |
| --- | --- |
| [!UICONTROL CCPA] | [!DNL California Consumer Privacy Act] |
| [!UICONTROL GDPR] | 歐盟的 [!DNL General Data Protection Regulation] |
| [!UICONTROL PDPA_THA] | 泰國的 [!DNL Personal Data Protection Act] |
| [!UICONTROL LGPD_BRA] | 巴西的 [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | 紐西蘭 [!DNL Privacy Act] |
| [!UICONTROL VCDPA_USA] | [!DNL Virginia Consumer Data Protection Act] |
| [!UICONTROL CPRA_USA] | [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL APA_AUS] | [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL HIPAA_AUS] | [!DNL Health Insurance Portability and Accountability Act] |

{style="table-layout:auto"}

>[!NOTE]
>
>請參閱以下文章的概觀： [支援的隱私權法規](../regulations/overview.md) 以取得每項法規之法律內容的詳細資訊。

系統會分別追蹤每種規則型態的工單。 若要切換規則型別，請選取 **[!UICONTROL 法規型別]** 下拉式功能表，並從清單中選取所需的規則。

![規則型別下拉式清單](../images/user-guide/regulation.png)

變更法規型別後，儀表板會更新以顯示適用於所選法規的所有操作、篩選器、Widget和工作建立對話方塊。

![已更新儀表板](../images/user-guide/dashboard-update.png)

### 狀態報告

「狀態報告」Widget左側的圖形，可追蹤已提交工作，以及任何可能已回報但有錯誤的工作。 右側的圖表會追蹤接近30天規定期間結束的工作。

選取圖表上方的兩個切換按鈕之一，以顯示或隱藏其各自的量度。

![](../images/user-guide/hide-errors.png)

您可以將滑鼠停留在有問題的資料點上，以檢視與圖表上任何資料點相關聯的確切工作數目。

![將滑鼠移到資料點上](../images/user-guide/mouse-over.png)

若要檢視指定資料點的進一步詳細資訊，請選取相關資料點，以在「工作請求」Widget中顯示相關工作。 記下套用至工作清單正上方的篩選器。

![從Widget套用的篩選器](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>將篩選器套用至工作請求Widget後，您可以選取 **X** 在篩選藥丸上。 然後，工作請求會返回預設追蹤清單。

### 工作請求

工作請求Widget會列出組織中所有可用的工作請求，包括請求型別、目前狀態、到期日及請求者電子郵件等詳細資訊。

>[!NOTE]
>
>僅可在完成日期後的30天記憶體取先前建立之工作的資料。

您可以在「工作請求」標題下方的搜尋列中鍵入關鍵字，以篩選清單。 清單會在您輸入時自動篩選，顯示包含符合搜尋字詞之值的請求。 您也可以使用 **[!UICONTROL 申請日期]** 下拉式選單來選取所列工作的時間範圍。

![工作請求搜尋選項](../images/user-guide/job-search.png)

若要檢視特定工作請求的詳細資訊，請從清單中選取請求的工作ID以開啟 **[!UICONTROL 工作詳細資訊]** 頁面。

![GDPR UI工作詳細資料](../images/user-guide/job-details.png)

此對話方塊包含每個專案的狀態資訊 [!DNL Experience Cloud] 解決方案及其相對於整體工作的目前狀態。 由於每個隱私權工作非同步，頁面會顯示每個解決方案的最新通訊日期和時間(GMT)，因為有些解決方案比有些解決方案需要更多的時間來處理請求。

如果解決方案已提供任何額外資料，可在此對話方塊中檢視。 您可以選取個別產品列來檢視此資料。

若要將完整的工作資料下載為CSV檔案，請選取 **[!UICONTROL 匯出至CSV]** 位於對話方塊的右上方。

## 建立新的隱私權工作請求 {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="说明"
>abstract="<ul><li>在左侧导航中选择<a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html#logging-in-from-experience-platform">请求</a>以打开 Privacy Ul，然后选择<b>创建请求</b>。</li><li>从这里可使用请求生成器或上传数据主体的 JSON 文件。</li><li>如果使用请求生成器，则选择作业类型（访问和/或删除），然后选择您提供的身份类型（电子邮件、ECID 或 AAID）或输入自定义身份命名空间。输入适合客户的身份值，并在完成后选择<b>创建</b>。</li><li>如果上传 JSON 文件，则选择“创建请求”旁边的箭头。从选项列表中，选择<b>上传 JSON</b> 并上传您的文件。如果您没有要上传的 JSON 文件，则选择<b>下载 Adobe-GDPR-Request.json</b> 以下载可填写的模板。上传 JSON，并在完成后选择<b>创建</b>。</li><li>有关此功能的更多帮助，请参阅 Experience League 上的 <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=zh-Hans">Privacy Service 用户指南</a>。</li></ul>"

>[!NOTE]
>
>為了建立隱私權工作請求，您必須提供存取或刪除其資料之特定客戶的身分資訊。 請在以下位置檢閱檔案： [隱私權請求的身分資料](../identity-data.md) 然後再繼續本節。

此 [!DNL Privacy Service] UI提供兩種建立新工作請求的方法：

* [使用請求產生器](#request-builder)
* [上傳JSON檔案](#json)

以下各節提供使用上述各種方法的步驟。

### 使用請求產生器 {#request-builder}

使用「請求產生器」，您可以在使用者介面中手動建立新的隱私權工作請求。 請求產生器最適合用於較簡單且較小的請求集，因為請求產生器限制每個使用者的請求只有ID型別。 若是更複雜的請求，最好 [上傳JSON檔案](#json) 而非。

若要開始使用請求產生器，請選取「 」 **[!UICONTROL 建立請求]** 位於畫面右側的「狀態報表」Widget下方。

![選取建立請求](../images/user-guide/create-request.png)

此 **[!UICONTROL 建立請求]** 對話方塊隨即開啟，顯示可用於針對目前所選規則型別提交隱私權工作請求的選項。

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

選取 **[!UICONTROL 工作型別]** 請求（「刪除」或「存取」）以及清單中一個或多個可用產品的完整清單。

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

下 **[!UICONTROL 名稱空間型別]**，請為要傳送至的客戶ID選取適當的名稱空間型別 [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

使用標準名稱空間型別時，請從下拉式選單（電子郵件、ECID或AAID）中選取名稱空間，然後在右側的文字方塊中輸入ID值，然後按 **\&lt;enter>** ，以將每個ID新增至清單。

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

使用自訂名稱空間型別時，您必須手動輸入名稱空間，才能在下方提供ID值。

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

完成後，選取 **[!UICONTROL 建立]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

對話方塊會消失，而新工作（或多個工作）會與其目前的處理狀態一起列在工作請求Widget中。

### 上傳JSON檔案 {#json}

建立更複雜的請求時（例如針對每個處理中的資料主體使用多個ID型別的請求），您可以透過上傳JSON檔案來建立請求。

選取旁的箭頭 **[!UICONTROL 建立請求]**，位於畫面右側的「狀態報表」Widget下方。 從出現的選項清單中，選取 **[!UICONTROL 上傳JSON]**.

![請求建立選項](../images/user-guide/create-options.png)

此 **[!UICONTROL 上傳JSON]** 對話方塊隨即出現，為您提供可將JSON檔案拖放到的視窗。

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

如果您沒有要上傳的JSON檔案，請選取「 」 **[!UICONTROL 下載Adobe-GDPR-Request.json]** 以下載範本，您可依據從資料主體收集的值填入。


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


在您的電腦上找到JSON檔案，並將其拖曳至對話方塊視窗中。 如果上傳成功，檔案名稱會顯示在對話方塊中。 您可以視需要繼續新增更多JSON檔案，方法是將其拖放至對話方塊中。

完成後，選取 **[!UICONTROL 建立]**. 對話方塊會消失，而新工作（或多個工作）會與其目前的處理狀態一起列在工作請求Widget中。

### 后续步骤

閱讀本檔案後，您已瞭解如何使用 [!DNL Privacy Service] UI可建立隱私權工作、檢視工作的詳細資訊和監控其處理狀態，並在完成後下載結果。

如需如何以程式設計方式執行這些操作的步驟，請使用 [!DNL Privacy Service] API，請參閱 [API指南](../api/overview.md).
