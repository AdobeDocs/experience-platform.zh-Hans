---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制建立角色
description: 本檔案提供透過Adobe Experience Cloud中的許可權介面管理角色的資訊
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# 管理角色

角色定義管理員、專家或一般使用者對貴組織資源的存取權。 在基於角色的存取控制環境中，使用者存取布建是透過共同責任和需求進行分組。 一个角色具有一组给定的权限，可将您组织的成员分配给一个或多个角色，具体取决于他们需要的查看或写入访问权限的范围。

## 创建新角色

若要建立新角色，請選取 **[!UICONTROL 角色]** 索引標籤並選取「 」 **[!UICONTROL 建立角色]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

此 **[!UICONTROL 建立新角色]** 對話方塊隨即顯示，提示您輸入名稱及說明（選擇性）。

完成後，選取 **[!UICONTROL 確認]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

接下來，使用下拉式選單選取您要包含在角色中的資源許可權。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

若要新增其他資源，請選取 **[!UICONTROL Adobe Experience Platform]** 左側導覽面板中，顯示資源清單。 或者，在左側導覽面板的搜尋列中輸入資源名稱。

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

按一下並拖曳相關資源，然後放置至主面板。

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

使用下拉式選單選取您要包含在角色中的資源許可權。 對您要納入角色的所有資源重複此步驟。 完成後，選取 **[!UICONTROL 儲存並退出]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

新角色已成功建立，您將會被重新導向至 **[!UICONTROL 角色]** 頁面，您會看到新建立的角色出現在清單中。

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

請參閱以下小節： [管理角色的許可權](#manage-permissions-for-a-role) 以取得建立角色許可權後如何管理角色許可權的詳細資訊。

## 複製角色

若要複製現有角色，請從 **[!UICONTROL 角色]** 標籤。 或者，使用篩選選項來篩選結果，以尋找您要複製的角色。

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

接下來，選取 **[!UICONTROL 複製]** 從畫面的右上角。

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

此 **[!UICONTROL 複製角色]** 對話方塊隨即顯示，提示您確認複製。

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

接著，您會前往角色的詳細資訊頁面，您可在此變更角色的名稱和許可權。 詳細資訊、標籤和沙箱與上一個角色重複。 使用者需要透過使用者索引標籤新增。 您可以檢視 [管理角色的許可權](permissions.md) 檔案，進一步瞭解將詳細資訊、標籤、沙箱和使用者新增至角色。

按一下向左箭頭返回 **[!UICONTROL 角色]** 標籤。

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

新角色將顯示在 **[!UICONTROL 角色]** 頁面。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 刪除角色

選取省略符號(`…`)，下拉式清單則會顯示可編輯、刪除或複製角色的控制項。 從下拉式清單中選取刪除。

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

此 **[!UICONTROL 刪除使用者角色]** 對話方塊隨即顯示，提示您確認刪除。

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

您將會返回 **[!UICONTROL 角色]** 標籤。

## 后续步骤

建立新角色後，您可以繼續下一步以 [管理角色的許可權](permissions.md).
