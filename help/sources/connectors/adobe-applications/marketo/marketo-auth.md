---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: 驗證您的Marketo來源聯結器
description: 本檔案提供如何產生Marketo驗證憑證的相關資訊。
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# 驗證您的 [!DNL Marketo Engage] 來源聯結器

建立之前 [!DNL Marketo Engage] (以下稱&quot;[!DNL Marketo]&quot;)來源聯結器，您必須先透過 [!DNL Marketo] 介面，以及擷取Munchkin ID、使用者端ID和使用者端密碼的值。

以下檔案提供如何取得驗證認證以建立 [!DNL Marketo] 來源聯結器。

## 設定新角色

取得驗證認證的第一步，是透過 [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) 介面。

登入 [!DNL Marketo] 並選取 **[!DNL Admin]** 從頂端導覽列取得。

![新角色的管理員](../images/marketo/home.png)

此 *[!DNL Users & Role]s* 頁面包含使用者、角色和登入歷程記錄的相關資訊。 若要建立新角色，請選取 **[!DNL Roles]** 從頂端標題中，然後選取 **[!DNL New Role]**.

![new-role](../images/marketo/new-role.png)

此时会显示 **[!DNL Create New Role]** 对话框。提供名稱和說明，然後選取您要授予此角色的許可權。 許可權僅限於特定工作區，使用者只能在其擁有許可權的工作區中執行動作。

選取要授與的許可權後，請選取「 」 **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

透過建立角色時，您可以管理API上受限制的許可權 [!DNL Marketo]. 除了選取「存取API」之外，您還可以透過選取以下許可權來提供具有最低存取層級的角色：

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## 設定新使用者

與角色類似，您可以透過以下連結設定新使用者： **[!DNL Users & Roles]** 頁面。 此 **[!DNL Users]** 頁面提供目前布建在Marketo中的作用中使用者清單。 選取 **[!DNL Invite New User]** 以布建新使用者。

![invite-new-user](../images/marketo/invite-new-user.png)

彈出視窗對話方塊選單出現。 為您的電子郵件、名字、姓氏和原因提供適當的資訊。 在此步驟中，您還可以建立您邀請的新使用者帳戶存取權的到期日。 完成後，選取 **[!DNL Next]**.

>[!IMPORTANT]
>
>設定新使用者時，您必須將存取權指派給嚴格依照您正在建立的自訂服務專屬的使用者。

![user-info](../images/marketo/new-user-info.png)

選取中適當的欄位 **[!DNL Permissions]** 步驟，然後選取 **[!DNL API Only]** 核取方塊以向新使用者提供API角色。 選取 **[!DNL Next]** 以繼續進行。

![許可權](../images/marketo/permissions.png)

若要完成程式，請選取 **[!DNL Send]**.

![message](../images/marketo/message.png)

## 設定自訂服務

建立新使用者後，您可以設定自訂服務以擷取新的認證。 在管理頁面中，選取 **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

此 **[!DNL Installed services]** 頁面包含現有服務的清單，若要建立新的自訂服務，請選取 **[!DNL New]** 然後選取 **[!DNL New Service]**.

![新服務](../images/marketo/new-service.png)

為您的新服務提供描述性顯示名稱，然後選取 **[!DNL Custom]** 從 **[!DNL Service]** 下拉式功能表。 提供適當的說明，然後從中選擇要布建的使用者 **[!DNL API Only User]** 下拉式功能表。 填入必要的詳細資料後，請選取 **[!DNL Create]** 以建立新的自訂服務。

![create](../images/marketo/create.png)

## 取得您的使用者端ID和使用者端密碼

建立新的自訂服務後，您現在可以擷取使用者端ID和使用者端密碼的值。 從 **[!DNL Installed Services]** 功能表，找到您要存取的自訂服務，然後選取 **[!DNL View Details]**.

![view-details](../images/marketo/view-details.png)

會出現一個對話方塊，其中包含您的使用者端ID和使用者端密碼。

![認證](../images/marketo/credentials.png)

## 取得您的Munchkin ID

您必須完成的最後一個步驟，才能驗證您的 [!DNL Marketo] 來源聯結器是擷取您的Munchkin ID。 在管理頁面中，選取 **[!DNL Munchkin]** 在 **[!DNL Integration]** 面板。

![admin-munchkin](../images/marketo/admin-munchkin.png)

此 *[!DNL Munchkin]* 頁面隨即顯示，您的唯一Munchkin ID會列在面板頂端。

![munchkin-Id](../images/marketo/munchkin-id.png)

結合您的使用者端ID和使用者端密碼，您可以使用Munchkin ID設定新帳戶和 [建立新的 [!DNL Marketo] 來源連線](../../../tutorials/ui/create/adobe-applications/marketo.md) 在Experience Platform上。
