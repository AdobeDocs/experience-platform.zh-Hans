---
keywords: Experience Platform；首頁；熱門主題；Microsoft Dynamics；microsoft dynamics；Dynamics；dynamics
solution: Experience Platform
title: 在使用者介面中建立Microsoft Dynamics來源連線
type: Tutorial
description: 瞭解如何使用Microsoft UI建立Adobe Experience Platform Dynamics來源連線。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 建立 [!DNL Microsoft Dynamics] ui中的來源連線

本教學課程提供建立 [!DNL Microsoft Dynamics] (以下稱&quot;[!DNL Dynamics]&quot;)來源連線使用Adobe Experience Platform UI。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Dynamics] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [為CRM來源設定資料流](../../dataflow/crm.md).

### 收集必要的認證

| 認證 | 描述 |
| ---------- | ----------- |
| `serviceUri` | 您的服務URL [!DNL Dynamics] 執行個體。 |
| `username` | 您的使用者名稱 [!DNL Dynamics] 使用者帳戶。 |
| `password` | 您的密碼 [!DNL Dynamics] 帳戶。 |
| `servicePrincipalId` | 您的使用者端識別碼 [!DNL Dynamics] 帳戶。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和基於金鑰的驗證時，需要此認證。 |

如需入門的詳細資訊，請參閱 [此 [!DNL Dynamics] 檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## 連線您的 [!DNL Dynamics] 帳戶

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Dynamics] 至平台的帳戶。

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL CRM]** 類別，選取 **[!UICONTROL Microsoft Dynamics]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 以建立新的 [!DNL Dynamics] 聯結器。

![目錄](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此 **[!UICONTROL 連線到Dynamics]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，為您的新輸入提供名稱和選擇性說明 [!DNL Dynamics] 帳戶。

此 [!DNL Dynamics] connector提供您不同的驗證型別以進行存取。 下 [!UICONTROL 帳戶驗證] 選取 **[!UICONTROL 基本驗證]** 以使用以密碼為基礎的認證。

完成後，選取 **[!UICONTROL 連線到來源]** 然後留出時間建立新帳戶。

![basic-authentication](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

或者，您可以選取 **[!UICONTROL 服務主體和金鑰驗證]** 並連線您的 [!DNL Dynamics] 帳戶使用以下專案的組合： [!UICONTROL 服務主體ID] 和 [!UICONTROL 服務主體金鑰].

>[!IMPORTANT]
>
> 中的基本驗證 [!DNL Dynamics] 雙因素驗證可能會加以封鎖，目前Platform不支援雙因素驗證。 在這種情況下，建議使用金鑰式驗證來建立來源聯結器，使用 [!DNL Dynamics].

![金鑰型驗證](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 認證 | 描述 |
| ---------- | ----------- |
| [!UICONTROL 服務主體ID] | 您的使用者端識別碼 [!DNL Dynamics] 帳戶。 使用服務主體和金鑰式驗證時，需要此ID。 |
| [!UICONTROL 服務主體金鑰] | 服務主體秘密金鑰。 使用服務主體和基於金鑰的驗證時，需要此認證。 |

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Dynamics] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 前往右上角以繼續。

![現有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Dynamics] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/crm.md).
