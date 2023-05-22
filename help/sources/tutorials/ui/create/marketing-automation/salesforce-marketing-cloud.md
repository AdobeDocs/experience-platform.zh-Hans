---
title: 連線您的SalesforceMarketing Cloud帳戶，以透過UIExperience Platform
description: 瞭解如何將您的SalesforceMarketing Cloud帳戶連線至透過UI進行Experience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 1%

---

# 連線您的 [!DNL Salesforce Marketing Cloud] 要透過UIExperience Platform的帳戶

>[!IMPORTANT]
>
>自訂物件擷取目前不支援 [!DNL Salesforce Marketing Cloud] 來源整合。


本教學課程提供如何連線至 [!DNL Salesforce Marketing Cloud] 透過UI將帳戶新增至Adobe Experience Platform。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有 [!DNL Salesforce Marketing Cloud] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [使用UI將行銷自動化資料帶入Experience Platform](../../dataflow/marketing-automation.md).

### 收集必要的認證

為了存取您的 [!DNL Salesforce Marketing Cloud] account on Platform，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| Host | 應用程式的主機伺服器。 這通常是您的子網域。 **注意：** 輸入您的 `host` 值，您只需要指定子網域而不是整個URL。 例如，如果您的主機URL為 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，則您只需輸入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作為您的主機值。 |
| 使用者端ID | 與您的關聯的使用者端ID [!DNL Salesforce Marketing Cloud] 應用程式。 |
| 使用者端密碼 | 與您的關聯的使用者端密碼 [!DNL Salesforce Marketing Cloud] 應用程式。 |

有關下列專案的驗證詳細資訊： [!DNL Salesforce Marketing Cloud]，請造訪 [[!DNL Salesforce] 驗證檔案](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 連線您的 [!DNL Salesforce Marketing Cloud] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 顯示Experience Platform支援的各種來源。

您可以從類別清單中選取適當的類別。 您也可以使用搜尋列來篩選特定來源。

在 [!UICONTROL 行銷自動化] 類別，選取 **[!UICONTROL SalesforceMarketing Cloud]** 然後選取 **[!UICONTROL 設定]**.

![已選取SalesforceMarketing Cloud來源的來源目錄。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

此 **[!UICONTROL 連線到SalesforceMarketing Cloud]** 頁面便會顯示。 您可以在此頁面建立新帳戶或使用現有帳戶。

### 新帳戶

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]** 並提供您帳戶的名稱、選擇性說明，以及與您的帳戶對應的驗證認證 [!DNL Salesforce Marketing Cloud] 帳戶。

完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新帳戶介面，您可在此介面驗證SalesforceMarketing Cloud的新帳戶。](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 現有帳戶

如果您已有帳戶，請選取 **[!UICONTROL 現有帳戶]** 然後從顯示的清單中選取您要使用的帳戶。

![您可以從現有SalesforceMarketing Cloud帳戶清單中選取的現有帳戶介面。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 后续步骤

依照本教學課程所述，您已建立您與 [!DNL Salesforce Marketing Cloud] 帳戶和Experience Platform。 您現在可以繼續下一節教學課程和 [建立資料流以將您的行銷自動化資料帶入Experience Platform](../../dataflow/marketing-automation.md).
