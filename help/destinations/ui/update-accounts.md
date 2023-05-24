---
keywords: 更新目的地帳戶、目的地帳戶、如何更新帳戶、更新目的地
title: 更新目的地帳戶
type: Tutorial
description: 本教學課程列出在Adobe Experience Platform UI中更新目的地帳戶的步驟
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 更新目的地帳戶

## 概述 {#overview}

此 **[!UICONTROL 帳戶]** 索引標籤會顯示您已建立與不同目的地的連線的詳細資訊。 請參閱 [帳戶總覽](../ui/destinations-workspace.md#accounts) 取得每個目的地帳戶的所有資訊。

本教學課程涵蓋使用Experience PlatformUI更新目的地帳戶詳細資訊的步驟。

您可以更新目的地帳戶詳細資料，以重新整理和重新驗證您目前使用之目的地的目前或過期帳戶的認證。 通常，OAuth和持有人權杖的期限有限，具體取決於目的地平台。 當這些Token過期時，您可以在下面進一步說明的工作流程中重新整理它們。 此工作流程會指導您完成OAuth工作流程或重新插入權杖。 同樣地，如果密碼或使用者存取權在下游平台中變更，您可以重新整理認證。

對於批次目的地，您可以更新存取權或秘密金鑰（如果其中任何一項已變更）。 此外，如果您想要繼續加密檔案，可以插入RSA公開金鑰，而且您匯出的檔案將會繼續加密。

![帳戶標籤](../assets/ui/update-accounts/destination-accounts.png)

## 更新帳戶 {#update}

請依照下列步驟，將連線詳細資料更新至現有目的地。

1. 登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 並選取 **[!UICONTROL 目的地]** 左側導覽列中的。 選取 **[!UICONTROL 帳戶]** 以檢視您現有的帳戶。

   ![帳戶標籤](../assets/ui/update-accounts/accounts-tab.png)

2. 選取篩選圖示 ![篩選圖示](../assets/ui/update-accounts/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的已篩選帳戶選擇。

   ![篩選目的地帳戶](../assets/ui/update-accounts/filter-accounts.png)

3. 選取省略符號(`...`)的名稱旁。 快顯面板隨即出現，其中提供選項至 **[!UICONTROL 啟用區段]**， **[!UICONTROL 編輯詳細資料]**、和 **[!UICONTROL 刪除]** 帳戶。 選取 ![編輯詳細資訊按鈕](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 編輯詳細資料]** 按鈕以編輯帳戶資訊。

   ![編輯帳戶](../assets/ui/update-accounts/accounts-edit.png)

4. 輸入更新後的帳戶認證。

   * 針對使用 `OAuth1` 或 `OAuth2` 連線型別，選取 **[!UICONTROL 重新連線OAuth]** 以更新您的帳戶認證。 您也可以更新帳戶的名稱和說明。

   ![編輯詳細資料OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * 針對使用 `Access Key` 或 `ConnectionString` 連線型別，您可以編輯帳戶驗證資訊，包括存取ID、秘密金鑰或連線字串等資訊。 您也可以更新帳戶的名稱和說明。

   ![編輯詳細資料存取金鑰](../assets/ui/update-accounts/edit-details-key.png)

   * 針對使用 `Bearer token` 連線型別，您可以視需要輸入新的持有人權杖。 您也可以更新帳戶的名稱和說明。

   ![編輯詳細資訊持有人權杖](../assets/ui/update-accounts/edit-details-bearer.png)

   * 針對使用 `Server to server` 連線型別，您可以更新帳戶的名稱和說明。

   ![編輯伺服器對伺服器的詳細資訊](../assets/ui/update-accounts/edit-details-s2s.png)

5. 選取 **[!UICONTROL 儲存]** 以完成帳戶詳細資訊更新。

## 后续步骤

依照本教學課程，您已成功使用 **[!UICONTROL 目的地]** 工作區以更新現有帳戶。

如需有關目的地的詳細資訊，請參閱 [目的地概觀](../catalog/overview.md).