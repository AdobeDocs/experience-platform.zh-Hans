---
keywords: Experience Platform；首頁；熱門主題；分段；區段比對；區段比對
solution: Experience Platform
title: 區段比對概觀
description: 「區段比對」是Adobe Experience Platform中的區段共用服務，可讓兩名或以上Platform使用者以安全、受管且隱私權友好的方式交換區段資料。
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1997'
ht-degree: 2%

---

# [!DNL Segment Match] 概述

Adobe Experience Platform區段比對是一項區段共用服務，可讓兩位或以上的Platform使用者以安全、受管且隱私權友好的方式交換區段資料。 [!DNL Segment Match] 會使用Platform隱私權標準和個人識別碼，例如雜湊電子郵件、雜湊電話號碼，以及裝置識別碼（例如IDFA和GAID）。

替換為 [!DNL Segment Match] 您可以：

* 管理身分重疊程式。
* 檢視預先共用預估值。
* 套用資料使用標籤以控制資料是否可與合作夥伴共用。
* 在發佈摘要後維護共用的對象生命週期管理，並透過新增、刪除和取消共用的功能繼續動態交換資料。

[!DNL Segment Match] 使用身分重疊程式，確保區段共用以安全和以隱私權為中心的方式進行。 一個 **重疊的身分** 是在您的區段和您選取的合作夥伴區段中都相符的身分。 在傳送者與接收者之間共用區段之前，身分重疊程式會檢查名稱空間中的重疊，並檢查傳送者與接收者之間的同意檢查。 必須傳遞兩個重疊檢查才能共用區段。

以下小節提供以下專案的詳細資訊： [!DNL Segment Match]，包括設定及其端對端工作流程的詳細資訊。

## 设置

以下各節概述如何設定和配置 [!DNL Segment Match]：

### 設定身分資料和名稱空間 {#namespaces}

開始使用的第一步 [!DNL Segment Match] 是確保您擷取的是支援的身分名稱空間資料。

身分名稱空間是的元件 [Adobe Experience Platform Identity Service](../../../identity-service/home.md). 每個客戶身分都包含一個關聯的名稱空間，可指出身分的上下文。 例如，名稱空間可以區分「name」的值<span>@email.com」作為電子郵件地址，或「443522」作為數值CRM ID。

完整身分包含ID值和名稱空間。 跨設定檔片段比對記錄資料時(例如 [!DNL Real-Time Customer Profile] 合併設定檔資料)，身分值和名稱空間必須相符。

在的內容中 [!DNL Segment Match]，共用資料時，名稱空間會用於重疊程式中。

支援的名稱空間清單如下：

| 命名空间 | 描述 |
| --------- | ----------- |
| 電子郵件（SHA256，小寫） | 預先雜湊電子郵件地址的名稱空間。 使用SHA256雜湊之前，此名稱空間中提供的值會轉換為小寫。 在電子郵件地址標準化之前，需要修剪開頭和結尾的空格。 此設定無法回溯變更。 Platform提供兩種支援資料收集雜湊的方法，透過 [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) 和至 [資料準備](../../../data-prep/functions.md#hashing). |
| 電話(SHA256_E.164) | 代表需要使用SHA256和E.164格式雜湊的原始電話號碼的名稱空間。 |
| ECID | 代表Experience CloudID (ECID)值的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請參閱 [ECID概觀](../../../identity-service/ecid.md) 以取得詳細資訊。 |
| Apple IDFA （廣告商的ID） | 代表廣告商Apple ID的名稱空間。 請參閱以下檔案： [興趣型廣告](https://support.apple.com/en-us/HT202074) 以取得詳細資訊。 |
| Google Ad ID | 代表Google Advertising ID的名稱空間。 請參閱以下檔案： [Google廣告ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) 以取得詳細資訊。 |

### 設定同意設定

您必須提供同意設定，並將其預設值設為 `opt-in` 或 `opt-out` 進行同意檢查。

選擇加入和選擇退出同意檢查會決定您預設是否可以在同意的情況下操作以共用使用者資料。 如果同意設定預設值設為 `opt-out`，則使用者資料可以共用，除非使用者明確選擇退出。 如果預設值設為 `opt-in`，則無法共用使用者資料，除非使用者明確選擇加入。

預設同意設定 [!DNL Segment Match] 設為 `opt-out`. 若要對您的資料強制執行選擇加入模式，請傳送電子郵件要求給您的Adobe帳戶團隊。

如需詳細資訊，請參閱 `share` 用於設定資料共用同意值的屬性，請參閱以下檔案： [隱私權與同意欄位群組](../../../xdm/field-groups/profile/consents.md). 如需用於擷取消費者同意，以收集及使用與隱私權、個人化和行銷偏好設定相關之資料的特定欄位群組的相關資訊，請參閱下列內容 [隱私權、個人化和行銷偏好設定的同意GitHub範例](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### 設定資料使用標籤

您必須建立的最後一個先決條件是設定新的資料使用標籤，以防止資料共用。 透過資料使用標籤，您可以管理允許透過分享的資料 [!DNL Segment Match].

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 標籤可隨時套用，讓您靈活選擇控管資料的方式。 最佳實務建議在資料內嵌至Experience Platform後，或資料可在Platform中使用時，立即為資料加上標籤。

[!DNL Segment Match] 使用C11標籤，此合約標籤特定於 [!DNL Segment Match] 手動新增至任何資料集或屬性，以確保將其從 [!DNL Segment Match] 合作夥伴共用程式。 C11標籤表示不應在下列位置使用的資料： [!DNL Segment Match] 程式。 在您決定好要排除的資料集和/或欄位後 [!DNL Segment Match] 並據此新增C11標籤，而標籤會由 [!DNL Segment Match] 工作流程。 [!DNL Segment Match] 自動啟用 [!UICONTROL 限制資料共用] 核心原則。 如需如何將資料使用標籤套用至資料集的特定指示，請參閱以下教學課程： [在UI中管理資料使用標籤](../../../data-governance/labels/user-guide.md).

如需資料使用標籤及其定義的清單，請參閱 [資料使用標籤字彙表](../../../data-governance/labels/reference.md). 如需資料使用原則的相關資訊，請參閱 [資料使用原則概觀](../../../data-governance/policies/overview.md).

### 瞭解 [!DNL Segment Match] 許可權

有兩個相關許可權 [!DNL Segment Match]：

| 权限 | 描述 |
| --- | --- |
| 管理對象共用連線 | 此許可權可讓您完成合作夥伴交握程式，該程式會連線兩個要啟用的組織 [!DNL Segment Match] 流程。 |
| 管理對象共用 | 此許可權可讓您建立、編輯和發佈摘要（用於下列專案的資料套件）： [!DNL Segment Match])與作用中合作夥伴(由管理員使用者透過以下連結的合作夥伴： **[!UICONTROL 對象共用連線]** 存取)。 |

請參閱 [存取控制總覽](../../../access-control/home.md) 以取得存取控制和許可權的詳細資訊。

## [!DNL Segment Match] 端對端工作流程

設定好身分資料和名稱空間、同意設定和資料使用標籤後，您就可以開始使用 [!DNL Segment Match] 及其功能。

### 管理合作夥伴

在Platform UI中選取 **[!UICONTROL 區段]** 從左側導覽列中，然後選取 **[!UICONTROL 摘要]** 從頂端標題。

![segments-feed.png](./images/segments-feed.png)

此 [!UICONTROL 摘要] 頁面包含從合作夥伴收到的摘要清單，以及您共用的摘要。 若要檢視現有合作夥伴的清單或建立與新合作夥伴的連線，請選取 **[!UICONTROL 管理合作夥伴]**.

![manage-partners.png](./images/manage-partners.png)

兩個合作夥伴之間的連線是「雙向交握」，可作為使用者在沙箱層級將其Platform組織連結在一起的自助方法。 需要連線，才能通知Platform已建立合約，且Platform可協助您與合作夥伴共用服務。

>[!NOTE]
>
>您與合作夥伴之間的「雙向握手」純屬連線。 在此過程中不會交換任何資料。

您可以在的主要介面中檢視與現有合作夥伴的連線清單 [!UICONTROL 管理合作夥伴] 畫面。 右邊欄上是 [!UICONTROL 共用設定] 面板，可讓您選擇產生新的 [!UICONTROL 連線ID] 以及輸入方塊，您可以在其中輸入合作夥伴的 [!UICONTROL 連線ID].

![establish-connection.png](./images/establish-connection.png)

若要建立新的 [!UICONTROL 連線ID]，選取 **[!UICONTROL 重新產生]** 在 [!UICONTROL 共用設定] 然後選取新產生的ID旁邊的復製圖示。

![share-setting.png](./images/share-setting.png)

若要使用下列專案連線合作夥伴： [!UICONTROL 連線ID]，請在下的輸入方塊中輸入其唯一ID值 [!UICONTROL 連線合作夥伴] 然後選取 **[!UICONTROL 請求]**.

![connect-partner.png](./images/connect-partner.png)

### 建立摘要 {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="受限的营销用例"
>abstract="受限的营销用例有助于为您的合作伙伴提供指导，确保根据您的数据治理限制正确使用共享区段。"
>text="Learn more in documentation"

A **摘要** 是一組資料（區段）、如何公開或使用這些資料的規則，以及決定如何將您的資料與合作夥伴的資料進行比對的設定。 摘要可透過以下方式獨立管理，並與其他Platform使用者交換： [!DNL Segment Match].

若要建立新的摘要，請選取 **[!UICONTROL 建立摘要]** 從 [!UICONTROL 摘要] 儀表板。

![create-feed.png](./images/create-feed.png)

摘要的基本設定包括關於行銷使用案例和身分設定的名稱、說明和設定。 提供摘要的名稱和說明，然後套用您要排除其資料的行銷使用案例。 您可以從清單中選取多個使用案例，包括：

* [!UICONTROL Analytics]
* [!UICONTROL 與PII結合]
* [!UICONTROL 跨網站目標定位]
* [!UICONTROL 数据科学]
* [!UICONTROL 電子郵件目標定位]
* [!UICONTROL 匯出至第三方]
* [!UICONTROL 站上廣告]
* [!UICONTROL 站上個人化]
* [!UICONTROL 區段比對]
* [!UICONTROL 單一身分個人化]

最後，請為您的摘要選取適當的身分名稱空間。 有關支援的特定名稱空間的資訊 [!DNL Segment Match]，請參閱 [身分資料和名稱空間表格](#namespaces). 完成後，選取 **[!UICONTROL 下一個]**.

![audience-sharing.png](./images/audience-sharing.png)

建立摘要的設定後，請從第一方區段清單中選取要共用的區段。 您可以從清單中選取多個區段，也可以使用滑鼠右欄來管理所選區段的清單。 完成後，選取 **[!UICONTROL 下一個]**.

![select-segments.png](./images/select-segments.png)

此 [!UICONTROL 共用] 頁面隨即顯示，提供您選擇要與其共用摘要的合作夥伴介面。 在此步驟中，您也可以檢視預先共用重疊預估報表，並依名稱空間檢視您與合作夥伴之間的重疊身分數目，以及同意共用資料的重疊身分數目。

選取 **[!UICONTROL 依區段分析]** 檢視預估報表。

![analyze.png](./images/analyze.png)

重疊預估報表可讓您在共用摘要之前，管理每個合作夥伴和每個區段的重疊和同意檢查。

| 量度 | 描述 |
| ------- | ----------- |
| 經同意的預估身分 | 符合為貴組織設定的同意要求的重疊身分總數。 |
| 預估的重疊身分 | 符合所選區段資格且與所選合作夥伴相符的身分數量。 這些身分會依名稱空間顯示，不代表個別設定檔身分。 重疊的預估值是根據輪廓草圖。 |

完成後，選取 **[!UICONTROL 關閉]**.

![overlap-report.png](./images/overlap-report.png)

選取合作夥伴並檢視重疊預估報表後，請選取「 」 **[!UICONTROL 下一個]** 以繼續進行。

![share.png](./images/share.png)

此 [!UICONTROL 檢閱] 步驟隨即顯示，可讓您在共用和發佈新摘要之前先檢閱該摘要。 此步驟包含您套用的身分設定詳細資訊，以及您選取的行銷使用案例、區段和合作夥伴的相關資訊。

選取 **[!UICONTROL 完成]** 以繼續進行。

![review.png](./images/review.png)

### 更新摘要

若要新增或移除區段，請選取 **[!UICONTROL 建立摘要]** 從 [!UICONTROL 摘要] 頁面，然後選取 **[!UICONTROL 現有摘要]**. 在出現的現有摘要清單中，選取您要更新的摘要，然後選取 **[!UICONTROL 下一個]**.

![摘要 — 清單](./images/feed-list.png)

區段清單隨即顯示。 從這裡，您可以新增區段至摘要，並使用滑鼠右欄來移除您不再需要的任何區段。 管理完摘要中的區段後，請選取「 」 **[!UICONTROL 下一個]** 然後依照上述步驟完成更新的摘要。

![update](./images/update.png)

>[!NOTE]
>
>當您從共用摘要新增或移除區段時，接收合作夥伴必須透過重新啟用 [!DNL Profile] 切換其已接收摘要的清單。

### 接受傳入摘要

若要檢視傳入摘要，請選取 **[!UICONTROL 已接收]** 從「 」的標題 [!UICONTROL 摘要] 頁面，然後從清單中選取您要檢視的摘要。 若要接受摘要，請選取 **[!UICONTROL 為設定檔啟用]** 並留出片刻讓狀態從更新 [!UICONTROL 擱置中] 至 [!UICONTROL 已啟用].

![received.png](./images/received.png)

接受共用摘要後，您就可以開始使用共用資料來建立新區段。

## 后续步骤

閱讀本檔案後，您已瞭解 [!DNL Segment Match]、其功能及其端對端工作流程。 請參閱下列檔案，進一步瞭解其他Platform服務：

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-Time Customer Profile] 概述](../../../profile/home.md)
