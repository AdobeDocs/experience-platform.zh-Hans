---
keywords: Experience Platform；首頁；熱門主題；
title: （測試版）在UI中建立Adobe Workfront來源連線
description: 本教學課程提供建立Adobe Workfront來源連線的步驟，以使用使用者介面將Workfront資料帶入Adobe Experience Platform。
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# （測試版）在UI中建立Adobe Workfront來源連線

>[!NOTE]
>
>Adobe Workfront來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供建立Adobe Workfront來源連線的步驟，以使用使用者介面將Workfront資料帶入Adobe Experience Platform。

## 快速入门

>[!IMPORTANT]
>
>您必須在Adobe Admin Console中設定為管理員，才能存取Workfront來源。

本教學課程需要您實際瞭解下列Experience Platform元件：

* [Experience Data Model (XDM)系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [即時客戶個人檔案](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 在使用者介面中建立Workfront來源連線

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示可用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的來源。

在 **[!UICONTROL Adobe應用程式]** 類別，選取 **[!UICONTROL Adobe Workfront]** 然後選取 **[!UICONTROL 新增資料]**.

![反白顯示Adobe Workfront來源的來源目錄。](../../../../images/tutorials/create/workfront/catalog.png)

## 选择数据

此 [!UICONTROL 選取資料] 步驟隨即顯示。 在這裡，您必須提供Workfront子網域和Datalane的值。 舉例來說，您的Workfront子網域與您用來存取Workfront執行個體的URL相同 `https://acme.workfront.com/`，而您的datalane代表您要使用的workfront環境。

新增子網域和Datalane後，請選取 **[!UICONTROL 下一個]**.

![具有子網域和datalane預留位置值的選取資料頁面。](../../../../images/tutorials/create/workfront/select-data.png)

## 提供資料流詳細資料

資料流詳細資料步驟可讓您為資料流提供名稱和可選描述。 在此步驟中，您也可以訂閱警報以接收有關資料流狀態的通知。 如需關於警報的詳細資訊，請瀏覽下列主題的教學課程： [訂閱來源UI中的警報](../../alerts.md).

提供資料流詳細資料並設定所需的警報設定後，請選取 **[!UICONTROL 下一個]**.

![包含資料流名稱、說明和警示通知之資訊的資料流詳細資訊頁面](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## 请查看

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![摘要連線資訊的檢閱頁面。](../../../../images/tutorials/create/workfront/review.png)

## 附录

以下小節提供有關Workfront來源的其他資訊。

### Workfront變更事件結構描述

Platform中的Workfront資料以時間序列記錄資料表示，資料中的每一列都有時間戳記，顯示事件發生的時間及與該事件相關的屬性。

在設定期間，會建立名為「來自流程的Workfront變更事件」的結構描述。

| 結構描述欄位 | 描述 |
| --- | --- |
| `timestamp` | 所選事件發生的時間。 時間戳記以GTM時區表示。 |
| `_workfront.objectType` | 物件型別。 可用的值包括 `project`， `task`， `portfolio`和其他專案，視變更或建立的物件而定。 |
| `_workfront.objectID` | 對應至物件型別的ID。 |
| `_workfront.created` | 此值已設為 `1` 如果事件代表物件建立。 |
| `_workfront.deleted` | 此值已設為 `1` 如果物件已刪除。 |
| `_worfkront.updated` | 此值已設為 `1` 如果物件已更新。 |
| `_workfront.completed` | 此值已設為 `1` 如果物件標示為已完成。 |
| `_workfront.parentObjectType` | （選用）對應至物件父項的物件型別。 |
| `_workfront.parentID` | 父物件的ID。 |
| `_workfront.customData` | 事件期間填入的所有自訂表單欄位和值的對應。 |

>[!IMPORTANT]
>
>系統只會填入已變更或已建立為事件一部分的屬性。 例如，如果您只變更物件的名稱，則只會填入下列欄位：<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## 后续步骤

依照本教學課程所述，您現在已建立資料流，將資料從Workfront帶入Experience Platform。 您現在可以使用以下服務 [查詢服務](../../../../../query-service/home.md) 以進一步分析您的資料。 如需Workfront的詳細資訊，請閱讀 [Workfront概觀](../../../../connectors/adobe-applications/workfront.md).
