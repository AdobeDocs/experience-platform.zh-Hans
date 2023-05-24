---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制瀏覽
description: 本檔案提供在Adobe Experience Cloud中使用許可權介面的相關資訊
exl-id: 39634bde-8858-44a6-b39a-776846654fc1
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 4%

---

# 許可權指南

[!UICONTROL 許可權] 是Adobe Experience Cloud的區域，管理員可在此定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。

替換為 [!UICONTROL 許可權]，您可以設定：

* [存取原則](./policies.md)
* [标签](./labels.md)
* [权限](./permissions.md)
* [角色](./roles.md)
* [沙盒](./sandboxes.md)
* [用户](./users.md)

為了存取屬性型存取控制許可權 [!DNL Experience Cloud]，您必須是您組織的管理員，該組織訂閱了 [!DNL Experience Cloud]. 雖然Adobe支援組織有彈性的管理員階層，但您必須是Adobe Experience Platform的產品管理員才能設定許可權。 請參閱以下文章中的Adobe Help Center： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以取得詳細資訊。

如果您沒有管理員許可權，請聯絡您的系統管理員以獲得存取權。

取得管理員許可權後，請前往 [Adobe Experience Cloud](https://experience.adobe.com/) 並使用您的Adobe憑證登入。 登入後， **[!UICONTROL 概觀]** 頁面會針對您擁有管理員許可權的組織顯示。 此頁面顯示您的組織已訂閱的產品，以及用於將使用者和管理者新增到整個組織的其他控制項。 選取 **[!UICONTROL 許可權]** 以開啟Platform整合的屬性型存取控制工作區。

![flac-select-product](../../images/flac-ui/flac-select-product.png)

Adobe Experience Cloud的屬性型存取控制工作區隨即出現，並開啟於 **[!UICONTROL 角色]** 頁面。 此頁面可讓您檢視所有角色，並管理本檔案中概述的各種設定。

>[!IMPORTANT]
>
>您的組織啟用屬性式存取控制後，您就可以開始使用Adobe Experience Cloud上的許可權(而不是Adobe Admin Console中的產品設定檔)來管理組織中使用者、功能、標籤和其他資源的許可權。

![flac-select-roles](../../images/flac-ui/flac-select-roles.png)

本使用手冊著重於說明如何使用 [!DNL Experience Cloud] 以指派Platform的存取許可權。 如需如何導覽的詳細一般資訊，請參閱 [!DNL Admin Console]，請參閱 [Admin Console使用手冊](https://helpx.adobe.com/cn/enterprise/using/admin-console.html).

## 后续步骤

在您導覽許可權工作區後，請繼續進行下一個步驟： [建立新角色](roles.md).
