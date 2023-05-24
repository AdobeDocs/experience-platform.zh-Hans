---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制管理角色許可權
description: 本檔案提供透過Adobe Experience Cloud中的許可權介面設定角色許可權的相關資訊
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 9515527f5a2c250b0a9057aa37769431e3b6fa07
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 4%

---

# 管理角色的許可權

>[!IMPORTANT]
>
>存取控制使用使用者ID （指派給使用者的內部唯一ID）來授予許可權。 當組織從Adobe ID移轉至Business ID時，為其使用者設定的所有許可權都將遺失，因為使用者ID變更，且存取控制將使用新產生的使用者ID。 如果您的組織移轉至Business ID，請聯絡您的Adobe代表，以將您的使用者ID從Adobe ID移轉至Business ID。

許可權是Experience Cloud的區域，管理員可以在其中定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。

通过 权限，您可以创建和管理角色，并为这些角色分配所需的资源权限。权限还允许您管理与特定角色关联的标签、沙盒和用户。

緊接在 [建立新角色](#create-a-new-role)，您會回到 **[!UICONTROL 角色]** 標籤。 如果您正在編輯現有角色的許可權，請從 **[!UICONTROL 角色]** 標籤。 或者，使用篩選選項來篩選結果以尋找角色。

## 篩選角色

選取漏斗圖示(![篩選圖示](../../images/icon.png))來顯示篩選控制項清單，以協助縮小結果範圍。

![flac篩選器](../../images/flac-ui/flac-filters.png)

以下篩選器適用於UI中的角色：

| 过滤器 | 描述 |
| --- | --- |
| [!UICONTROL 建立時間介於] | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 |
| [!UICONTROL 创建者] | 從下拉式選單中選取使用者，依角色建立者篩選。 |
| [!UICONTROL 修改時間介於] | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 |
| [!UICONTROL 修改者] | 從下拉式清單中選取使用者，依角色修飾元篩選。 |

若要移除篩選條件，請針對有問題的篩選條件，選取藥丸圖示上的「X」，或選取 **[!UICONTROL 全部清除]** 以移除所有篩選器。

![濾鏡 — 清除 — 濾鏡](../../images/flac-ui/flac-clear-filters.png)

## 角色詳細資料

從中選擇角色 **[!UICONTROL 角色]** 標籤，這會開啟角色的詳細資訊頁面。

![flac-details](../../images/flac-ui/flac-details.png)

詳細資訊標籤提供角色的概觀。 概述會顯示角色名稱、角色說明、建立和修改角色的使用者名稱、建立和修改角色的時間，以及附加至角色的許可權。 如有需要，可修改角色名稱和角色說明。

## 管理角色的標籤

選取 **[!UICONTROL 標籤]** 標籤以開啟角色標籤頁面，然後選取 **[!UICONTROL 新增標籤]** 以指派標籤給角色。

![flac標籤](../../images/flac-ui/flac-labels.png)

標籤會列在此頁面上。 清單會顯示標簽名稱、易記名稱、類別及其說明。

從清單中選取您要新增至角色的標籤，然後選取 **[!UICONTROL 儲存]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

新增的標籤會顯示在下方 **[!UICONTROL 標籤]** 標籤。

![flac-added-labels](../../images/flac-ui/flac-added-labels.png)

若要從角色中移除標籤，請選取 **X** 圖示加以識別。

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 管理角色的沙箱

選取 **[!UICONTROL 沙箱]** 標籤以開啟「角色：沙箱」頁面。 您可以在此處檢視新增至角色的沙箱清單。

![flac-sandbox](../../images/flac-ui/flac-sandboxes.png)

若要新增更多沙箱至角色，請選取 **[!UICONTROL 編輯]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

下一個畫面會提示您使用下拉式清單，選擇沙箱中要包含在角色中的資源許可權。 完成後，選取 **[!UICONTROL 儲存並退出]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 管理角色的使用者

選取 **[!UICONTROL 使用者]** 標籤以開啟「角色使用者」頁面，然後選取 **[!UICONTROL 新增使用者]** 以將使用者指派給角色。

![flac-users](../../images/flac-ui/flac-users.png)

從清單中選取您要新增至角色的使用者。 或者，使用搜尋列輸入使用者的名稱或電子郵件地址來搜尋使用者，然後選取 **[!UICONTROL 儲存]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

新增的使用者會出現在 **[!UICONTROL 使用者]** 標籤。

![flac-added-users](../../images/flac-ui/flac-added-users.png)

若要從角色中移除使用者，請選取 **X** 圖示加以識別。

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

## 管理角色的API認證

選取 **[!UICONTROL API認證]** 標籤以開啟「角色API認證」頁面，然後選取 **[!UICONTROL 新增API認證]** 以指派API認證給角色。

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

從清單中選取您要新增至角色的API認證，然後選取 **[!UICONTROL 儲存]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

新增的API認證會顯示在下方 **[!UICONTROL API認證]** 標籤。

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

若要從角色中移除API認證，請選取 **X** 圖示加以識別。

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

此 **[!UICONTROL 移除API認證]** 對話方塊隨即顯示，提示您確認刪除。

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

您將會返回 **[!UICONTROL API認證]** 標籤。

## 管理角色的使用者群組

使用者群組是多個使用者，這些使用者已分組在一起，並且有權執行相同的功能。

選取 **[!UICONTROL 使用者群組]** 標籤以開啟「角色」使用者群組頁面，然後選取 **[!UICONTROL 新增群組]** 將使用者群組指派給角色。

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

從清單中選取您想要新增至角色的使用者群組。 或者，使用搜尋列，輸入群組名稱來搜尋使用者群組，然後選取 **[!UICONTROL 儲存]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

新增的使用者群組會出現在 **[!UICONTROL 使用者群組]** 標籤。

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

若要從角色中移除使用者群組，請選取 **X** 圖示加以識別。

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

此 **[!UICONTROL 移除使用者群組]** 對話方塊隨即顯示，提示您確認刪除。

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您將會返回 **[!UICONTROL 使用者群組]** 標籤。

## 透過產品設定檔新增使用者至Experience Platform

若要將使用者新增至產品設定檔，請登入Admin Console並選取 **[!UICONTROL 新增使用者]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

此 **[!UICONTROL 新增使用者至您的團隊]** 對話方塊隨即顯示。 輸入使用者的電子郵件地址、名字（選用）和姓氏（選用）。

選取鉛筆圖示以選取產品和使用者群組，然後選取 **[!UICONTROL Adobe Experience Platform]**，然後選取 **[!UICONTROL AEP-Default-All-Users]**，然後選取  **[!UICONTROL 儲存]**.

![product-profile](../../images/flac-ui/product-profile.png)

## 后续步骤

建立許可權後，您可以繼續下一步以 [管理使用者](users.md).
