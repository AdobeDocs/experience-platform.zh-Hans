---
keywords: 刪除目的地帳戶、目的地帳戶、如何刪除帳戶
title: 刪除目的地帳戶
type: Tutorial
description: 本教學課程列出在Adobe Experience Platform UI中刪除目的地帳戶的步驟
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 2ea56957e122140fbc68c727e36666f8f9a71dd8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 刪除目的地帳戶

## 概述 {#overview}

此 **[!UICONTROL 帳戶]** 索引標籤會顯示您已建立與不同目的地的連線的詳細資訊。 請參閱 [帳戶總覽](../ui/destinations-workspace.md#accounts) 取得每個目的地帳戶的所有資訊。

本教學課程涵蓋使用Experience PlatformUI刪除不再需要的目的地帳戶的步驟。

![帳戶標籤](../assets/ui/update-accounts/destination-accounts.png)

## 刪除帳戶 {#delete}

>[!TIP]
>
>在刪除目的地帳戶之前，您必須先刪除與目的地帳戶相關聯的任何現有資料流。 若要刪除現有的目的地資料流，請參閱上的教學課程 [在UI中刪除目的地資料流](./delete-destinations.md).

請依照下列步驟刪除現有的目的地帳戶。

1. 登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 並選取 **[!UICONTROL 目的地]** 左側導覽列中的。 選取 **[!UICONTROL 帳戶]** 以檢視您現有的帳戶。

   ![帳戶標籤](../assets/ui/delete-accounts/accounts-tab.png)

2. 選取篩選圖示 ![篩選圖示](../assets/ui/update-accounts/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的已篩選帳戶選擇。

   ![篩選目的地](../assets/ui/delete-accounts/filter-accounts.png)

3. 選取省略符號(`...`)的名稱旁。 快顯面板隨即出現，其中提供選項至 **[!UICONTROL 啟用區段]**， **[!UICONTROL 編輯詳細資料]**、和 **[!UICONTROL 刪除]** 帳戶。 選取 ![刪除按鈕](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 刪除]** 按鈕來刪除所需的帳戶。

   ![刪除目的地帳戶](../assets/ui/delete-accounts/delete-accounts.png)

4. 最後確認對話方塊出現，選取 **[!UICONTROL 刪除]** 以完成程式。

![確認帳戶刪除](../assets/ui/delete-accounts/confirm-account-deletion.png)

## 后续步骤

依照本教學課程所述，您已成功使用目的地工作區來刪除現有帳戶。

如需如何以程式設計方式執行這些操作的步驟，請使用 [!DNL Flow Service] API，請參考以下教學課程： [使用流量服務API刪除連線](../api/delete-destination-account.md)
