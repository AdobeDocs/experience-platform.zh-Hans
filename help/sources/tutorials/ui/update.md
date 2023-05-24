---
keywords: Experience Platform；首頁；熱門主題；更新帳戶
description: 在某些情況下，可能需要更新現有來源帳戶的詳細資料。 來源工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。
solution: Experience Platform
title: 在UI中更新來源連線帳戶詳細資料
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 在UI中更新帳戶詳細資料

在某些情況下，可能需要更新現有來源帳戶的詳細資料。 此 [!UICONTROL 來源] 工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。

本教學課程提供步驟，說明如何從更新現有帳戶的詳細資訊和認證。 [!UICONTROL 來源] 工作區。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
- [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 更新帳戶

登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 選取 **[!UICONTROL 帳戶]** 以檢視現有帳戶。

![目錄](../../images/tutorials/update/catalog.png)

此 **[!UICONTROL 帳戶]** 頁面便會顯示。 此頁面是可檢視帳戶的清單，包括有關其來源、使用者名稱、資料流數量和建立日期的資訊。

選取篩選圖示 ![篩選](../../images/tutorials/update/filter.png) 以啟動「排序」面板。

![accounts-list](../../images/tutorials/update/accounts-list.png)

排序面板提供所有來源的清單。 您可以從清單中選取多個來源，以存取與不同來源關聯的已篩選帳戶選擇。

選取您要使用的來源，以檢視其現有帳戶的清單。 識別要更新的帳戶後，請選取省略符號(`...`)。

![帳戶排序](../../images/tutorials/update/accounts-sort.png)

下拉式選單隨即出現，為您提供以下選項： **[!UICONTROL 新增資料]**， **[!UICONTROL 編輯詳細資料]**、和 **[!UICONTROL 刪除]**. 選取 **[!UICONTROL 編輯詳細資料]** 從功能表更新您的帳戶。

![update](../../images/tutorials/update/update.png)

此 **[!UICONTROL 編輯帳戶詳細資料]** 對話方塊可讓您更新帳戶的名稱、說明和驗證認證。 更新所需的資訊後，請選取 **[!UICONTROL 儲存]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

過了一會兒，畫面底部會顯示一個確認方塊，以確認更新成功。

![已確認更新](../../images/tutorials/update/update-confirmed.png)

## 后续步骤

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區以更新現有來源帳戶的資訊。

如需如何以程式設計方式執行這些操作的步驟，請使用 [!DNL Flow Service] API，請參考以下教學課程： [使用流量服務API更新連線資訊](../../tutorials/api/update.md).
