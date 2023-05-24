---
title: 在UI中建立Google Ads來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Google Ads來源連線。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ac87434c857a39f4be3714cba57519cbb4fa54a6
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# 在使用者介面中建立Google Ads來源連線

>[!NOTE]
>
>Google Ads來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供使用Google使用者介面建立Adobe Experience Platform Ads來源連線的步驟。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的Google Ads連線，可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/advertising.md)

### 收集必要的認證

若要存取您的Google Ads帳戶平台，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| 使用者端客戶ID | 使用者端客戶ID是對應至您要使用Google Ads API管理的Google Ads使用者端帳戶的帳號。 此ID遵循的範本 `123-456-7890`. |
| 登入客戶ID | 登入客戶ID是與您的Google Ads管理員帳戶對應的帳號，用於從特定的作業客戶擷取報表資料。 如需登入客戶ID的詳細資訊，請閱讀 [Google Ads API檔案](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| 開發人員權杖 | 開發人員權杖可讓您存取Google Ads API。 您可以使用相同的開發人員Token，對所有Google Ads帳戶提出請求。 透過以下方式擷取您的開發人員權杖： [登入您的管理員帳戶](https://ads.google.com/home/tools/manager-accounts/) 然後導覽至「API中心」頁面。 |
| 重新整理Token | 重新整理權杖屬於 [!DNL OAuth2] 驗證。 此權杖可讓您在存取權杖過期後重新產生存取權杖。 |
| 使用者端ID | 使用者端ID會與使用者端密碼搭配使用，作為的一部分 [!DNL OAuth2] 驗證。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |
| 使用者端密碼 | 使用者端密碼會與使用者端ID搭配使用，作為的一部分 [!DNL OAuth2] 驗證。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |

閱讀API概觀檔案，瞭解 [Google Ads快速入門的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview).

## 連線您的Google Ads帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 廣告]** 類別，選取 **[!UICONTROL Google Ads]**，然後選取 **[!UICONTROL 新增資料]**.

![Experience PlatformUI中的來源目錄。](../../../../images/tutorials/create/ads/catalog.png).

此 **[!UICONTROL 連線至Google Ads]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Google Ads帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程中現有帳戶的選擇頁面。](../../../../images/tutorials/create/ads/existing.png).

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明和您的Google Ads認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![來源工作流程中的新帳戶介面。](../../../../images/tutorials/create/ads/new.png).

## 后续步骤

依照本教學課程，您已建立與Google Ads帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流以將廣告資料帶入Platform](../../dataflow/advertising.md).
