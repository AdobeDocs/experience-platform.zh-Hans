---
title: 查詢服務稽核記錄整合
description: 查詢服務稽核記錄可維護各種使用者動作的記錄，以形成稽核軌跡，用於疑難排解問題或遵循公司資料管理政策和法規要求。 本教學課程提供查詢服務專屬的稽核記錄功能概觀。
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] 稽核記錄整合

Adobe Experience Platform [!DNL Query Service] 稽核記錄整合提供查詢相關使用者動作的記錄。 稽核記錄是進行疑難排解以及遵守公司資料管理政策和法規要求的重要工具。 此功能可讓您傳回許多事件型別的動作記錄，並篩選及匯出記錄。 可透過Platform UI或 [稽核查詢API](https://www.adobe.io/experience-platform-apis/references/audit-query/) 並下載為CSV或JSON檔案格式。

若要進一步瞭解稽核記錄使用者介面，請參閱 [稽核記錄概觀檔案](../../landing/governance-privacy-security/audit-logs/overview.md). 若要進一步瞭解如何呼叫Platform API，請參閱 [稽核記錄API指南](../../landing/api-guide.md).

## 先决条件

您必須擁有 [!DNL Data Governance] [!UICONTROL 檢視使用者活動記錄] 已啟用在Platform UI中檢視稽核記錄儀表板的許可權。 許可權會透過Adobe啟用 [Admin Console](https://adminconsole.adobe.com/). 如果您沒有啟用此許可權的管理員許可權，請聯絡貴組織的管理員。 請參閱存取控制檔案以瞭解 [透過Admin Console新增許可權的完整指示](../../access-control/home.md).

## [!DNL Query Service] 稽核記錄類別 {#audit-log-categories}

提供的稽核記錄類別 [!DNL Query Service] 如下所示。

| 类别 | 描述 |
|---|---|
| [!UICONTROL 查询] | 此類別可讓您稽核查詢執行。 |
| [!UICONTROL 查詢範本] | 此類別可讓您稽核對查詢範本採取的各種動作（建立、更新和刪除）。 |
| [!UICONTROL 排定的查詢] | 此類別可讓您稽核在中建立、更新或刪除的排程 [!DNL Query Service]. |

## 執行 [!DNL Query Service] 稽核記錄 {#perform-an-audit-log}

若要針對下列專案執行稽核： [!DNL Query Service] 活動，選取 **[!UICONTROL 稽核]** 從左側導覽，然後按一下漏斗圖示(![篩選圖示。](../images/audit-log/filter.png))來顯示篩選控制項清單，以協助縮小結果範圍。

![Platform UI稽核記錄儀表板，左側導覽中的「稽核」和篩選控制項會醒目提示。](../images/audit-log/filter-controls.png)

從 [!UICONTROL 稽核] 儀表板 [!UICONTROL 活動記錄] 索引標籤上，您可以透過以下任何專案篩選所有錄製的平台動作： [!DNL Query Service] 類別。 可根據記錄結果執行的時間段、採取的動作/功能或執行查詢的使用者，進一步篩選記錄結果。 請參閱稽核記錄檔案以瞭解 [有關如何根據類別、動作、使用者和狀態篩選記錄的完整指示](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

傳回的稽核記錄檔資料包含符合您所選篩選條件之所有查詢的下列資訊。

| 列名称 | 描述 |
|---|---|
| [!UICONTROL 时间戳] | 在中執行動作的確切日期和時間 `month/day/year hour:minute AM/PM` 格式。 |
| [!UICONTROL 資產名稱] | 的值 [!UICONTROL 資產名稱] 欄位取決於選擇作為篩選器的類別。 使用時 [!UICONTROL 排定的查詢] 類別這是 **排程名稱**. 使用時 [!UICONTROL 查詢範本] 類別，這是 **範本名稱**. 使用時 [!UICONTROL 查詢] 類別，這是 **工作階段ID** |
| [!UICONTROL 类别] | 此欄位符合您在篩選下拉式清單中選取的類別。 |
| [!UICONTROL 操作] | 這可以是建立、刪除、更新或執行。 可用的動作取決於選擇作為篩選器的類別。 |
| [!UICONTROL 用户] | 此欄位提供執行查詢的使用者ID。 |

![反白顯示篩選活動記錄檔的「稽核」控制面板。](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>透過下載CSV或JSON檔案格式的記錄結果，提供的查詢詳細資料會多於稽核記錄儀表板中預設顯示的資料。

## 詳細資訊面板

選取稽核記錄結果的任何一列，即可開啟畫面右側的詳細資訊面板。

![稽核控制面板「活動記錄」索引標籤，並反白顯示詳細資訊面板。](../images/audit-log/details-panel.png)

詳細資訊面板可用來尋找 [!UICONTROL 資產ID] 和 [!UICONTROL 事件狀態].

的值 [!UICONTROL 資產ID] 會隨著稽核中使用的類別而改變。

* 使用時 [!UICONTROL 查詢] 類別， [!UICONTROL 資產ID] 是  **工作階段ID**.
* 使用時 [!UICONTROL 查詢範本] 類別， [!UICONTROL 資產ID] 是 **範本ID** 前置詞為 `[!UICONTROL templateID:]`.
* 使用時 [!UICONTROL 排定的查詢] 類別， [!UICONTROL 資產ID] 是  **排程ID** 前置詞為 `[!UICONTROL scheduleID:]`.

的值 [!UICONTROL 事件狀態] 會隨著稽核中使用的類別而改變。

* 使用時 [!UICONTROL 查詢] 類別， [!UICONTROL 事件狀態] 欄位提供所有欄位的清單 **查詢ID** 由使用者在該工作階段中執行。
* 使用時 [!UICONTROL 查詢範本] 類別， [!UICONTROL 事件狀態] 欄位提供 **範本名稱** 作為事件狀態的前置詞。
* 使用時 [!UICONTROL 查詢排程] 類別， [!UICONTROL 事件狀態] 欄位提供 **排程名稱** 作為事件狀態的前置詞。

## 可用的篩選器 [!DNL Query Service] 稽核記錄類別 {#available-filters}

可用的篩選器會因下拉式清單中所選的類別而異。 下表詳細說明以下專案可用的篩選器 [[!DNL Query Service] 稽核記錄類別](#audit-log-categories).

| 过滤器 | 描述 |
|---|---|
| 类别 | 請參閱 [[!DNL Query Service] 稽核記錄類別](#audit-log-categories) 區段，以取得可用類別的完整清單。 |
| 操作 | 當引用時 [!DNL Query Service] 稽核類別，更新為 **修改現有表單**，刪除為 **移除排程或範本**，建立為 **建立新排程或範本**，而執行為 **執行查詢**. |
| 用户 | 輸入完整的使用者ID (例如johndoe@acme.com)以依使用者篩選。 |
| 状态 | 此 [!UICONTROL 允許]， [!UICONTROL 成功]、和 [!UICONTROL 失敗] 選項會根據「狀態」或「事件狀態」來篩選記錄，而 [!UICONTROL 拒絕] 選項將會篩選掉 **全部** 記錄。 |
| 日期 | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 |

## 后续步骤

閱讀本檔案可讓您更瞭解 [!DNL Query Service] 稽核記錄功能，以及如何用來篩選您的 [!DNL Query Service] 使用者動作。

如果您使用 [!DNL Query Service] 稽核記錄功能如需疑難排解，建議您閱讀 [疑難排解指南](../troubleshooting-guide.md).
