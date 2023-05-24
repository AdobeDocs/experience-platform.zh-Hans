---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM；zoho crm；Zoho；zoho
solution: Experience Platform
title: 在使用者介面中建立Zoho CRM來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Zoho CRM來源連線。
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 建立 [!DNL Zoho CRM] ui中的來源連線

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的CRM資料。 本教學課程提供建立 [!DNL Zoho CRM] 來源聯結器使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Zoho CRM] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/crm.md).

### 收集必要的認證

為了連線 [!DNL Zoho CRM] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| --- | --- |
| 端點 | 的端點 [!DNL Zoho CRM] 您向其提出要求的伺服器。 |
| 帳戶URL | 帳戶URL可用來產生存取和重新整理Token。 URL必須是網域專屬的。 |
| 使用者端ID | 與您的對應之使用者端ID [!DNL Zoho CRM] 使用者帳戶。 |
| 使用者端密碼 | 與您的對應之使用者端密碼 [!DNL Zoho CRM] 使用者帳戶。 |
| 存取Token | 存取權杖會授權您對的安全及臨時存取 [!DNL Zoho CRM] 帳戶。 |
| 重新整理Token | 重新整理權杖是在您的存取權杖過期後，用來產生新存取權杖的權杖。 |

如需這些憑證的詳細資訊，請參閱以下檔案： [[!DNL Zoho CRM] 驗證](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## 連線您的 [!DNL Zoho CRM] 帳戶

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Zoho CRM] 帳戶至 [!DNL Platform].

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL CRM] 類別，選取 **[!UICONTROL Zoho CRM]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/zoho/catalog.png)

此 **[!UICONTROL 連線Zoho CRM帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Zoho CRM] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/zoho/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的 [!DNL Zoho CRM] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

>[!TIP]
>
>您的帳戶URL網域必須與適當的網域位置相對應。 以下是各種網域及其對應的帳戶URL：<ul><li>美國： https://accounts.zoho.com</li><li>澳洲： https://accounts.zoho.com.au</li><li>歐洲： https://accounts.zoho.eu</li><li>印度： https://accounts.zoho.in</li><li>中國： https://accounts.zoho.com.cn</li></ul>

![新](../../../../images/tutorials/create/zoho/new.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Zoho CRM] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/crm.md).
