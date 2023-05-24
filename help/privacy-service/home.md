---
keywords: Experience Platform；首頁；熱門主題；GDPR；gdpr；ccpa：CCPA；PDPA；PDPA_that；PDPA_THA；lgpd；LGPD；lgpd_bra；LGPD_BRA；
solution: Experience Platform
title: Privacy Service概觀
description: Privacy Service可讓您在Experience Cloud資料作業中促進自動遵守法律隱私權法規。
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 3296209a15a5f88ab14e16de25d554b9df712445
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 5%

---

# [!DNL Privacy Service] 概述

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service的許可權已得到改善，以提高其精細度等級。 這些變更可讓組織管理員以所需的角色和許可權層級，授予更多使用者存取權。 技術帳戶使用者必須更新其Privacy Service許可權，因為此即將進行的更新對他們而言是重大變更。 此許可權變更的強制實施將發生在 **2023年4月13日**. 請參閱以下說明檔案： [移轉舊版API認證](./permissions.md#migrate-tech-accounts) 以取得解決此問題的指引。
>
>企業客戶可使用技術帳戶，這些帳戶是透過Adobe開發人員控制檯建立的。 技術帳戶持有人的Adobe ID結尾為 `@techacct.adobe.com`. 如果您不確定您是否為技術帳戶擁有者，請聯絡您的組織管理員。

為了提供更好的客戶體驗，您需要收集和儲存客戶的個人資料。 使用此資料時，請務必瞭解並尊重客戶的隱私權。 新的法律和组织规定正在用户提供相应的权利，允许他们请求访问或删除您的数据存储中的用户个人数据。

Adobe Experience Platform [!DNL Privacy Service] 因應企業管理客戶個人資料的方式發生根本性轉變而開發。 的核心目的 [!DNL Privacy Service] 是自動化資料隱私權法規合規性，一旦違規，可能導致重大罰款並中斷貴企業的資料營運。

[!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶資料請求。 替換為 [!DNL Privacy Service]，您可以提交存取和刪除Adobe Experience Cloud應用程式中個人客戶資料的請求，協助實現法律和組織隱私法規的自動合規性。

>[!IMPORTANT]
>
>Privacy Service僅適用於資料主體和消費者權利請求。 不支援或不允許將Privacy Service用於資料清理或維護的任何其他用途。 Adobe有法定義務須及時履行。 因此，不允許在Privacy Service上進行負載測試，因為這是僅限生產的環境，且會建立有效隱私權請求的不必要待處理專案。
>
>現已設定每日硬性上傳限制，以防止服務被濫用。 發現濫用系統的使用者將會停用其服務的存取權。 隨後將與其舉行會議，討論其行動並討論可接受的Privacy Service用途。

## 開始使用 [!DNL Privacy Service] {#getting-started}

為了使用 [!DNL Privacy Service]，您需根據貴組織的隱私權要求、您從客戶那裡收集的身分資料型別，以及將CRM系統與服務介面的最佳方式，來做出幾項重要決定。

這些決定可透過下列問題加以摘要：

1. **我從客戶那裡收集哪些資訊？**
   * 善加利用 [!DNL Privacy Service]，您必須詳細瞭解您從客戶那裡收集的資料型別，以及哪些資料受到隱私權法規的約束。 請參閱以下小節： [判斷隱私權需求](#requirements) 以取得詳細資訊。
1. **我是否正確標示我的資料？**
   * 資料必須正確加上標籤，服務才能在隱私權工作期間決定要存取或刪除哪些欄位。 請參閱以下小節： [標籤資料](#label) 以取得詳細資訊。
1. **我是否知道要將哪些ID傳送至 [!DNL Privacy Service]？**
   * 傳送隱私權請求時，必須提供特定Adobe應用程式專用的個別客戶ID。 請參閱以下小節： [提供身分資料](#identity)  和 [提出隱私權請求](#requests) 以取得詳細資訊。
1. **如何追蹤我的隱私權工作？**
   * 提出隱私權請求後，您可使用數個選項來追蹤其狀態和結果。 請參閱以下小節： [監控隱私權工作](#monitor) 以取得詳細資訊。

以下各節提供這些重要先決條件步驟的一般指引，也提供進一步連結 [!DNL Privacy Service] 說明檔案以取得更多詳細資料。

### 判斷貴組織的隱私權要求 {#requirements}

根据您的业务性质及运营所在的司法管辖区，您的数据运营可能会受到隐私法规的约束。这些法规通常赋予您的客户请求访问您从他们那里收集的数据的权利，并且这些客户有权请求删除所存储的数据。客戶對其個人資料的請求，在本檔案稱為「隱私權請求」。

如需不同法律隱私權法規的詳細資訊，請參閱 [!DNL Privacy Service] 管理請求，包括關鍵術語和常見問題的解答，請參閱 [隱私權法規檔案](./regulations/overview.md).

如果您的資料作業屬於任何受支援法規的管轄範圍，請檢閱其檔案以取得重要資訊，例如他們提供給客戶的特定隱私權，以及遵循隱私權要求的合規視窗。 在決定如何整合時，應將此資訊列入考量 [!DNL Privacy Service] 以及客戶應如何與您的網站互動以提出隱私權請求。

除了法律規範外，在做出這些決定時，也應考慮適用於您組織的任何組織或行業標準。

### 隱私權請求的標籤資料 {#label}

根據 [!DNL Experience Cloud] 您正在使用的應用程式，必須標示回應隱私權請求時應存取或刪除的特定資料欄位。 標籤資料的程式因應用程式而異。 若要瞭解如何為每個支援的Adobe應用程式加上資料標籤，請參閱以下檔案： [Experience Cloud應用程式](./experience-cloud-apps.md).

### 決定要傳送至的身分資料型別 [!DNL Privacy Service] {#identity}

為了 [!DNL Privacy Service] 若要處理來自客戶的隱私權請求，該請求本身必須提供至少一個唯一身分值。 唯一身分值是可用於識別個人及其在您網站中儲存之個人資料的任何資訊， [!DNL Experience Cloud] 資料存放區。 [!DNL Privacy Service] 根據請求的性質（存取、刪除或選擇退出），使用此身分資訊來尋找和處理客戶的個人資料。

根據 [!DNL Experience Cloud] 您的CRM系統所使用的應用程式，您必須為每個客戶提供的身分值型別和數量會有所不同。 有些應用程式會使用自己的內部客戶ID值(例如Adobe Target ID)，而其他解決方案則需仰賴Adobe的全域識別碼 [!DNL Experience Cloud Identity Service] (ECID)追蹤所有客戶活動 [!DNL Experience Cloud] 應用程式。 此外，電子郵件地址或電話號碼等一般個人資訊也可以作為有效的身分資料。

上的檔案 [隱私權請求的身分資料](./identity-data.md) 提供接受的身分資訊型別的詳細資訊 [!DNL Privacy Service]. 本檔案也提供相關指引，說明如何運用Adobe技術，在客戶與您的網站互動時，有效從客戶擷取適當的身分資訊，並將資料傳送至 [!DNL Privacy Service] （在API要求中）。

### 開始提出隱私權請求 {#requests}

在您決定企業的隱私權需求，並決定要傳送至哪些身分值後， [!DNL Privacy Service]，您就可以開始提出隱私權請求。 [!DNL Privacy Service] 可讓您透過API或UI傳送隱私權請求。

>[!IMPORTANT]
>
>以下各節提供檔案連結，說明如何在API或UI中提出一般隱私權請求。 然而，取決於 [!DNL Experience Cloud] 若您正在使用的應用程式，您在要求裝載中必須傳送的欄位可能會與這些指南中顯示的範例不同。
>
>當您遵循API或UI指南，請參閱以下檔案： [Privacy Service和Experience Cloud應用程式](./experience-cloud-apps.md) 如需進一步檔案，瞭解如何針對您的特定設定隱私權請求的格式 [!DNL Experience Cloud] 應用程式。
>
>同時請務必注意，隱私權請求會跨Experience Cloud應用程式以非同步方式處理。 當Privacy Service收到要求後，每個應用程式可能需要幾分鐘到數週的時間才能完成要求。 完成每個請求所花的時間取決於您所使用的應用程式，以及需要處理的資料量。

#### 使用 API

此 [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) 提供幾個端點，可讓您使用RESTful API呼叫來建立和管理隱私權工作，讓您以程式設計方式處理隱私權法規遵循。 [!DNL Experience Cloud] 應用程式。 如需如何使用API的詳細步驟，請參閱 [Privacy Service API指南](api/overview.md).

#### 使用UI

>[!NOTE]
>
>此 [!DNL Privacy Service] UI目前僅支援存取和刪除請求。 所有選擇退出請求必須改透過API提出。

此 [!DNL Privacy Service] UI可讓您使用圖形介面建立及監控隱私權工作。 UI包含 **[!UICONTROL 狀態報告]** widget，以視覺化方式呈現所有作用中請求的狀態，並允許您使用內建來建立新請求 **[!UICONTROL 請求產生器]** 或上傳JSON檔案。 如需使用UI的詳細資訊，請參閱 [Privacy Service使用手冊](ui/overview.md).

### 監視隱私權工作 {#monitor}

完成隱私權工作後，您有數個選項可監控其狀態和結果：

| 監視方法 | 描述 |
| --- | --- |
| [!DNL Privacy Service] UI | 此 [!DNL Privacy Service] UI提供監視儀表板，可讓您檢視所有作用中請求狀態的視覺化表示。 請參閱 [Privacy Service使用手冊](ui/overview.md) 以取得詳細資訊。 |
| [!DNL Privacy Service] API | 您可以使用提供的查詢端點，以程式設計方式監控隱私權工作的狀態。 [!DNL Privacy Service] API。 請參閱 [Privacy Service API指南](./api/overview.md) 瞭解如何使用API的詳細步驟。 |
| [!DNL Privacy Events] | [!DNL Privacy Events] 善用傳送至已設定webhook的Adobe I/O事件，以促進有效的工作請求自動化。 如此一來，您就不需要輪詢 [!DNL Privacy Service] API，以檢查工作是否已完成，或工作流程中是否已達到特定里程碑。 請參閱教學課程，位置如下： [訂閱隱私權事件](./privacy-events.md) 以取得詳細資訊。 |

## 后续步骤

本檔案提供以下專案的概觀： [!DNL Privacy Service] 以及開始使用服務功能所需的主要步驟。 如需有關使用的各個方面的更深入資訊，請參閱整份概觀中所連結的檔案 [!DNL Privacy Service].
