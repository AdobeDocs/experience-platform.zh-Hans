---
title: 查詢範本
description: 查詢範本是可重複使用的已儲存SQL查詢，其他使用者可重複使用以節省時間和精力。 它們可以使用查詢編輯器或查詢服務API建立，並可用於所有Experience Platform資料集。
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: d5d69134627b1a162691bda95732d989bd6e3469
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# 查詢範本

Adobe Experience Platform查詢服務可讓您以查詢範本的形式儲存和重複使用SQL程式碼。 範本可避免重複執行常見的工作，從而節省精力。 您可以在組織內共用範本，輕鬆地變更查詢值，而不需要存取或瞭解底層SQL。

本檔案提供在「查詢服務」中建立查詢範本所需的資訊。

## 先决条件

您必須擁有 [!UICONTROL 管理查詢] 已啟用存取「查詢編輯器」的許可權，並在Platform UI中檢視查詢控制面板。 許可權會透過Adobe啟用 [Admin Console](https://adminconsole.adobe.com/). 如果您沒有啟用此許可權的管理員許可權，請聯絡貴組織的管理員。 請參閱存取控制檔案以瞭解 [透過Admin Console新增許可權的完整指示](../../access-control/home.md).

## 建立查詢範本

您可以透過兩種方法建立查詢範本，其中一種方法是向查詢服務API發出POST請求 `query-templates` 端點，或是透過查詢編輯器寫入、命名和儲存查詢。

### 使用查詢編輯器來編寫查詢並將其另存為範本

請參閱檔案，瞭解如何使用查詢編輯器 [寫入](./user-guide.md#query-authoring) 和 [儲存查詢](./user-guide.md#saving-queries). 命名並儲存查詢後，即可將其當做查詢範本重複使用。 [!UICONTROL 範本] 標籤。

## 瀏覽查詢範本 {#browse}

從Platform UI的查詢工作區中，選取 **[!UICONTROL 範本]** 以顯示可用已儲存查詢的清單。

![會反白顯示「範本」標籤的查詢工作區。](../images/ui/query-templates/query-templates.png)

若要尋找相關範本資訊，請從可用清單中選取任何查詢範本，以開啟詳細資訊面板。

![查詢ID為反白的查詢工作區中的詳細資訊面板。](../images/ui/query-templates/details-panel.png)

從詳細資訊面板中，您可以執行四個不同的動作：

* 選取 **[!UICONTROL 輸出資料集]** 以編輯所選範本的輸出資料集。
* 選取 **[!UICONTROL 檢視排程]** 導覽至 [!UICONTROL 時程表] 標籤。 此檢視包含與查詢相關聯的任何排程資訊。
* 選取 **[!UICONTROL 刪除查詢]** 以刪除範本。
* 選取範本名稱以瀏覽至查詢編輯器，其中會預先填入SQL以進行編輯。

### 使用查詢服務API建立範本

如需相關指示，請參閱檔案 [如何建立查詢範本](../api/query-templates.md#create-a-query-template) 使用查詢服務API。 新建立的查詢範本的詳細資料包含在回應本文中。

>[!NOTE]
>
>使用API建立的範本也可在Platform UI查詢服務範本索引標籤中看到。

## 后续步骤

閱讀本檔案後，您現在已能更清楚瞭解如何在「查詢服務」中建立查詢範本。 請參閱 [UI總覽](./overview.md)，或 [查詢服務API指南](../api/getting-started.md) 以進一步瞭解查詢服務功能。

請參閱 [排程查詢端點指南](../api/scheduled-queries.md) 瞭解如何使用API排程查詢，或 [查詢編輯器指南](./user-guide.md#scheduled-queries) 適用於UI。
