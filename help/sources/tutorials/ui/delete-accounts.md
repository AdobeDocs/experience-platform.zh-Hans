---
keywords: Experience Platform；首頁；熱門主題；刪除帳戶
description: Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供從「來源」工作區刪除帳戶的步驟。
solution: Experience Platform
title: 刪除UI中的來源連線帳戶
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# 刪除來源連線帳戶

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供從刪除帳戶的步驟。 **[!UICONTROL 來源]** 工作區。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構描述組合基本概念](../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 使用UI刪除帳戶

>[!TIP]
>
>在刪除來源帳戶之前，您必須先刪除與來源帳戶關聯的任何現有資料流。 若要刪除現有的資料流，請參閱上的教學課程 [在UI中刪除來源資料流](./delete.md).

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示各種來源，您可使用這些來源建立帳戶和資料流。 每個來源都會顯示與其相關聯的現有帳戶和資料流數量。

選取 **[!UICONTROL 帳戶]** 存取 **[!UICONTROL 帳戶]** 頁面。

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

現有帳號的清單隨即顯示。 本頁面提供現有帳戶（例如來源、使用者名稱、關聯的資料流和建立日期）的可排序資訊清單。 選取 **漏斗圖示** 以排序。

![資料流 — 清單](../../images/tutorials/delete-accounts/accounts.png)

排序面板會顯示在畫面左側，其中包含可用來源的清單。 您可以使用排序功能選取多個來源。

選取您要存取的來源，並從主介面的帳戶清單中找出您要刪除的帳戶。 在此範例中，選取的來源為 **[!DNL Azure Blob Storage]** 且帳戶名稱為 **[!UICONTROL Blobtectconnector]**. 從排序面板選取多個來源時，您最近建立的帳戶會先出現，因為清單是依建立日期排序。

選取您要刪除的帳戶。

![資料流 — 排序](../../images/tutorials/delete-accounts/sort.png)

此 **[!UICONTROL 屬性]** 面板會出現在畫面的右側，其中包含有關所選帳戶的資訊。

選取省略符號(`...`)的名稱旁。 快顯面板隨即出現，其中提供選項至 **[!UICONTROL 新增資料]**， **[!UICONTROL 編輯詳細資料]**、和 **[!UICONTROL 刪除]**. 選取 **[!UICONTROL 刪除]** 以刪除帳戶。

![資料流 — 排序](../../images/tutorials/delete-accounts/delete.png)

最後確認對話方塊出現，選取 **[!UICONTROL 刪除]** 以完成程式。

![delete](../../images/tutorials/delete-accounts/confirm.png)

## 后续步骤

依照本教學課程，您已成功使用 **[!UICONTROL 來源]** 工作區以刪除現有帳戶。

如需如何以程式設計方式執行這些操作的步驟，請使用 [!DNL Flow Service] API，請參考以下教學課程： [使用流量服務API刪除連線](../../tutorials/api/delete.md)
