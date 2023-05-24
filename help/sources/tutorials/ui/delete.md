---
keywords: Experience Platform；首頁；熱門主題；刪除資料流
description: 來源工作區可讓您刪除包含錯誤或已過時的現有批次和串流資料流。
solution: Experience Platform
title: 刪除UI中的資料流
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 刪除UI中的資料流

此 [!UICONTROL 來源] 工作區可讓您刪除包含錯誤或已過時的現有批次和串流資料流。

本教學課程提供使用刪除資料流的步驟。 [!UICONTROL 來源] 工作區。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [來源](../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
- [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

## 刪除資料流

在 [EXPERIENCE PLATFORMUI](https://platform.adobe.com)，選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區，然後選取 **[!UICONTROL 資料流]** 從頂端標題。

![目錄](../../images/tutorials/delete/catalog.png)

此 **[!UICONTROL 資料流]** 頁面便會顯示。 此頁面是可檢視資料流的清單，包括有關其目標資料集、來源、帳戶名稱和建立日期的資訊。

選取篩選圖示(![filter-icon](../../images/tutorials/delete/filter.png))，以啟動「排序」面板。

![資料流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有來源的清單。 您可以從清單中選取多個來源，以存取與您選取的特定來源相關聯的資料流篩選選取專案。

選取您要使用的來源，以檢視其現有資料流的清單。 識別要刪除的資料流後，選取省略符號(`...`)時，不會變更資料流名稱。

![資料流 — 篩選器](../../images/tutorials/delete/dataflows-filter.png)

下拉式功能表隨即顯示，提供您編輯資料流排程、停用資料流或將其完全刪除的選項。

選取 **[!UICONTROL 刪除]** 以刪除資料流。

![delete](../../images/tutorials/delete/delete.png)

最後確認對話方塊隨即顯示。 選取 **[!UICONTROL 刪除]** 以完成程式。

![confirm](../../images/tutorials/delete/confirm.png)

過了一會兒，畫面底部會顯示一個確認方塊，以確認刪除成功。

![已確認](../../images/tutorials/delete/confirmed.png)

## 后续步骤

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區以刪除現有的資料流。

請參閱教學課程，位置如下： [使用流量服務API刪除資料流](../../tutorials/api/delete-dataflows.md) 瞭解如何使用API呼叫以程式設計方式執行這些操作的步驟。
