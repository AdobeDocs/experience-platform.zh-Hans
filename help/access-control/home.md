---
keywords: Experience Platform；首頁；熱門主題；存取控制；adobe admin console
solution: Experience Platform
title: 访问控制概述
description: Adobe Experience Platform的存取控制需透過Adobe Admin Console提供。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 88bfcdef65b4a938d573b1beb1952c7e030ebc13
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 2%

---

# 访问控制概述

Adobe Experience Platform的存取控制需透過 **[!UICONTROL 許可權]** 在 [Adobe Experience Cloud](https://experience.adobe.com/). 此功能利用角色和原則，將使用者與許可權和沙箱連結。

## 存取控制階層與工作流程

若要設定Experience Platform的存取控制，您必須擁有擁有Experience Platform產品的組織的系統或產品管理員許可權。 可授予或撤銷許可權的最小角色為產品管理員。 可以管理許可權的其他管理員角色是系統管理員（無限制）。 請參閱以下文章中的Adobe Help Center： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以取得詳細資訊。

>[!NOTE]
>
>從此刻起，本檔案提及的「管理員」一律指產品管理員或以上人員（如上所述）。

取得和指派存取許可權的高層級工作流程可概述如下：

- 在授權Adobe Experience Platform或使用Experience Platform的應用程式/應用程式服務後，系統會傳送電子郵件給授權期間指定的管理員。
- 管理員登入 [Adobe Admin Console](#adobe-admin-console) 並選取 **Adobe Experience Platform** 從總覽頁面上的產品清單。
- 若要授與Experience Platform的存取權，管理員需要將使用者新增至預設產品設定檔： `AEP-Default-All-Users`.
- 在「Experience Platform許可權」中，管理員可以建立新角色，或編輯任何現有角色的許可權和使用者。
- 建立或編輯角色時，管理員會使用 **[!UICONTROL 使用者]** 標籤，並授予這些使用者許可權(例如&quot;[!UICONTROL 讀取資料集]「或」[!UICONTROL 管理結構描述]「)，方式是編輯角色的許可權。 同樣地，管理員可以使用相同的編輯選項指派沙箱的存取權。
- 當使用者登入Experience Platform使用者介面時，他們對Experience Platform功能的存取權是由上一步授予他們的許可權所驅動。 例如，如果使用者沒有 [!UICONTROL 檢視資料集] 許可權， **[!UICONTROL 資料集]** 該使用者看不到側邊功能表中的索引標籤。

如需如何在Experience Platform中管理存取控制的詳細步驟，請參閱 [存取控制使用手冊](./ui/overview.md).

對Experience Platform API的所有呼叫都會驗證許可權，如果在目前使用者內容中找不到適當的許可權，則會傳回錯誤。 在UI中，將根據授予目前使用者的許可權，隱藏或更改元素。

## 权限 {#platform-permissions}

[!UICONTROL 許可權] 提供管理組織Experience Platform存取的中央位置。 到 [!UICONTROL 許可權]，您可以授予使用者群組各種Experience Platform功能的存取許可權，例如 [!UICONTROL 管理資料集]， [!UICONTROL 檢視資料集]，或 [!UICONTROL 管理設定檔].

### 角色

在 [!UICONTROL 角色] 區段，許可權會透過使用角色指派給使用者。 角色可讓您向一個或多個使用者授予許可權，並且還包含他們透過角色指派給他們的沙箱範圍的存取權。 您可以將使用者指派給屬於您組織的一或多個角色。

### 預設角色

Experience Platform隨附兩個預先設定的預設角色。 下表概述每個預設設定檔中提供的內容，包括他們授予存取許可權的沙箱，以及他們在該沙箱範圍內授予的許可權。

| 角色 | 沙箱存取 | 权限 |
| --- | --- | --- |
| 預設的生產所有存取權 | 生产 | 所有適用於Experience Platform的許可權，「沙箱管理」許可權除外。 |
| 沙箱管理員 | 不适用 | 僅提供對沙箱管理許可權的存取。 |

## 沙箱和許可權

非生產沙箱是資料虛擬化的一種形式，可讓您將資料與其他沙箱隔離，通常用於開發實驗、測試或試用。 角色的許可權可讓角色的使用者存取他們有權存取的沙箱環境中的Experience Platform功能。 預設Experience Platform授權會授予您5個沙箱（一個生產環境和4個非生產環境）。 您可以新增10個非生產沙箱的套件，最多總共75個沙箱。 如需詳細資訊，請聯絡貴組織的管理員或您的Adobe銷售代表。

如需Experience Platform沙箱的詳細資訊，請參閱 [沙箱總覽](../sandboxes/home.md).

### 沙箱的存取權

沙箱的存取權透過角色進行管理。 如需如何為角色啟用沙箱存取權的詳細步驟，請參閱 [屬性型存取控制角色指南](./abac/ui/roles.md).

可授予使用者角色中一或多個沙箱的存取權。 如果一位使用者包含在兩個或多個角色中，則該使用者將可存取這些角色中包含的所有沙箱。

「沙箱管理」許可權可讓使用者管理、檢視或重設沙箱。

### 資源許可權 {#permissions}

資源 [!UICONTROL 許可權] 角色中的標籤會顯示該角色的有效沙箱和許可權：

![許可權 — 概觀](./images/permissions.png)

透過資源許可權授與的許可權會依類別排序，有些許可權會授與對多個低階功能的存取權。

下表概述角色中Experience Platform的可用許可權，以及使用者授予存取權的特定Experience Platform功能說明。 如需有關如何將許可權新增至角色的詳細步驟，請參閱 [屬性型存取控制角色指南](./abac/ui/roles.md).

| 类别 | 权限 | 描述 |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL 檢視警示歷史記錄] | 警示歷程記錄的唯讀存取權。 |
| [!DNL Alerts] | [!UICONTROL 解決警示] | 讀取、編輯和刪除警示的存取權。 |
| [!DNL Alerts] | [!UICONTROL 檢視警示] | 警示的唯讀存取權。 |
| [!DNL Alerts] | [!UICONTROL 管理警報] | 讀取、建立、編輯和刪除警示歷程記錄的存取權。 |
| [!DNL Data Hygiene] | [!UICONTROL 檢視資料衛生] | 資料檢疫的唯讀存取。 |
| [!DNL Data Hygiene] | [!UICONTROL 管理資料衛生] | 讀取、建立、編輯和刪除資料檢疫的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理架构] | 讀取、建立、編輯和刪除結構描述和相關資源的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 查看架构] | 對結構描述和相關資源的唯讀存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理關係] | 讀取、建立、編輯和刪除綱要關係的存取權。 |
| [!DNL Data Modeling] | [!UICONTROL 管理身分中繼資料] | 讀取、建立、編輯和刪除結構描述身分中繼資料的存取權。 |
| [!DNL Data Management] | [!UICONTROL 管理資料集] | 讀取、建立、編輯和刪除資料集的存取權。 結構描述的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 查看数据集] | 資料集和結構描述的唯讀存取權。 |
| [!DNL Data Management] | [!UICONTROL 資料監視] | 以唯讀方式存取監督資料集和資料流。 |
| [!DNL Profile Management] | [!UICONTROL 管理設定檔] | 存取讀取、建立、編輯和刪除用於客戶設定檔的資料集。 對可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視設定檔] | 對可用設定檔的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理区段] | 讀取、建立、編輯和刪除區段的存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視區段] | 可用區段的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 管理合併原則] | 讀取、建立、編輯和刪除合併原則的存取權。 |
| [!DNL Profile Management] | [!UICONTROL 檢視合併原則] | 對可用合併原則的唯讀存取權。 |
| [!DNL Profile Management] | [!UICONTROL 匯出區段的對象] | 能夠將評估的對象區段匯出至資料集。 |
| [!DNL Profile Management] | [!UICONTROL 評估區段給對象] | 可透過評估區段定義來為對象產生設定檔。 |
| [!DNL Identity Management] | [!UICONTROL 管理身份命名空间] | 讀取、建立、編輯和刪除身分名稱空間的存取權。 |
| [!DNL Identity Management] | [!UICONTROL 查看标识命名空间] | 身分識別名稱空間的唯讀存取。 |
| [!DNL Identity Management] | [!UICONTROL 檢視身分圖表] | 身分圖的唯讀存取。 |
| [!DNL Sandbox Administration] | [!UICONTROL 管理沙箱] | 讀取、建立、編輯和刪除沙箱的存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 查看沙盒] | 屬於您組織的沙箱的唯讀存取權。 |
| [!DNL Sandbox Administration] | [!UICONTROL 重設沙箱] | 可重設沙箱。 |
| [!DNL Destinations] | [!UICONTROL 管理目的地] | 讀取、建立和刪除目的地啟用流程和目的地帳戶的存取權。 |
| [!DNL Destinations] | [!UICONTROL 檢視目的地] | 以唯讀方式存取中的可用目的地 **[!UICONTROL 目錄]** 索引標籤和已驗證的目標 **[!UICONTROL 瀏覽]** 標籤。 |
| [!DNL Destinations] | [!UICONTROL 啟用目的地] | 讓使用者能啟用現有目的地的區段。 在啟動工作流程中啟用對應步驟。 此許可權需要 [!UICONTROL 檢視目的地] 或 [!UICONTROL 管理目的地] 將授與將對目的地啟用資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 啟用區段而不進行對應] | 讓使用者能在不顯示 [對應步驟](../destinations/ui/activate-batch-profile-destinations.md#mapping). 使用者可以在啟動工作流程中新增和移除區段，但無法新增或移除對應的屬性或身分。 此許可權需要 [!UICONTROL 啟用目的地] 將許可權授與將啟用目的地資料的使用者。 |
| [!DNL Destinations] | [!UICONTROL 管理和啟用資料集目的地] | 能夠讀取、建立、編輯和停用資料集匯出流程。 還能對已建立的作用中資料集啟用資料。 |
| [!DNL Destinations] | [!UICONTROL 目的地製作] | 能夠使用編寫目的地 [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL 管理來源] | 讀取、建立、編輯和停用來源的存取權。 |
| [!DNL Data Ingestion] | [!UICONTROL 檢視來源] | 對中的可用來源具有唯讀存取權 **[!UICONTROL 目錄]** 索引標籤和已驗證的來源 **[!UICONTROL 瀏覽]** 標籤。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | 存取建立、接受和拒絕合作夥伴握手以連線兩個組織並啟用 [!DNL Segment Match] 流程。 |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | 讀取、建立、編輯和發佈的存取權 [!DNL Segment Match] 使用中合作夥伴的摘要。 |
| [!DNL Data Science Workspace] | [!UICONTROL 管理資料科學工作區] | 在中讀取、建立、編輯和刪除的存取權 [!DNL Data Science Workspace]. |
| 数据治理 | [!UICONTROL 套用資料使用標籤] | 讀取、建立和刪除使用標籤的存取權。 |
| 数据治理 | [!UICONTROL 管理資料使用原則] | 讀取、建立、編輯和刪除資料使用原則的存取權。 |
| 数据治理 | [!UICONTROL 檢視資料使用原則] | 屬於您組織的資料使用原則的唯讀存取權。 |
| 数据治理 | [!UICONTROL 檢視使用者活動記錄] | 唯讀存取權，可檢視錄製的影像 [稽核記錄](../landing/governance-privacy-security/audit-logs/overview.md) 平台活動的URL編號。 |
| [!DNL Dashboards] | [!UICONTROL 檢視授權使用量儀表板] | 唯讀存取權，可檢視授權使用情況儀表板。 |
| [!DNL Dashboards] | [!UICONTROL 管理標準儀表板] | 新增尚未在Data Warehouse中的自訂屬性。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢] | 存取Platform資料的讀取、建立、編輯和刪除結構化SQL查詢。 |
| [!DNL Query Service] | [!UICONTROL 管理查詢服務整合] | 存取以建立、更新和刪除不會到期的認證以進行查詢服務存取。 |

## 后续步骤

閱讀本指南後，您已瞭解Experience Platform中存取控制的主要原則。 您現在可以繼續前往 [屬性型存取控制使用手冊](./abac/overview.md) 有關如何使用Experience Cloud建立Experience Platform和指派角色的許可權的詳細步驟。
