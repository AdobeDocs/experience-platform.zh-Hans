---
title: 在UI中建立SugarCRM帳戶和聯絡人來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立SugarCRM帳戶和聯絡人來源連線。
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# (Beta)建立 [!DNL SugarCRM Accounts & Contacts] ui中的來源連線

>[!NOTE]
>
>此 [!DNL SugarCRM Accounts & Contacts] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL SugarCRM Accounts & Contacts] 使用Adobe Experience Platform使用者介面的來源連線。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL SugarCRM] 帳戶，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/crm.md).

### 收集必要的認證

為了連線 [!DNL SugarCRM Accounts & Contacts] 至Platform，您必須提供下列連線屬性的值：

| 認證 | 描述 | 示例 |
| --- | --- | --- |
| `Host` | 來源所連線的SugarCRM API端點。 | `developer.salesfusion.com` |
| `Username` | 您的SugarCRM開發人員帳戶使用者名稱。 | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | 您的SugarCRM開發人員帳戶密碼。 | `123456789` |

### 建立Platform結構描述

建立之前 [!DNL SugarCRM] 來源連線時，您必須先建立平台結構描述以用於您的來源。 請參閱教學課程，位置如下： [建立平台結構描述](../../../../../xdm/schema/composition.md) 有關如何建立方案的完整步驟。

此 [!DNL SugarCRM Accounts & Contacts] 支援多個API。 這表示您必須根據要運用的物件型別，建立個別的結構描述。 請參閱下列帳戶和連絡人結構描述的範例：

>[!BEGINTABS]

>[!TAB 帐户]

![顯示帳戶範例結構描述的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB 連絡人]

![顯示聯絡人範例結構描述的平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## 連線您的 [!DNL SugarCRM Accounts & Contacts] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 *CRM* 類別，選取 **[!UICONTROL SugarCRM帳戶與連絡人]**，然後選取 **[!UICONTROL 新增資料]**.

![具有SugarCRM帳戶與聯絡人卡片目錄的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

此 **[!UICONTROL 連線SugarCRM帳戶與連絡人帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL SugarCRM Accounts & Contacts] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![與現有帳戶連線SugarCRM帳戶和連絡人帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![使用新帳戶連線SugarCRM帳戶和連絡人帳戶的Platform UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### 选择数据

最後，您必須選取要擷取至Platform的物件型別。

| 物件型別 | 描述 |
| --- | --- |
| `Accounts` | 與您的組織有關聯的公司。 |
| `Contacts` | 與您的組織建立關係的個人。 |

>[!BEGINTABS]

>[!TAB 帐户]

![顯示已選取帳戶選項之設定的SugarCRM帳戶與聯絡人的平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB 連絡人]

![顯示已選取連絡人選項之設定的SugarCRM帳戶與連絡人平台UI熒幕擷圖](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL SugarCRM Accounts & Contacts] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/crm.md).

## 其他资源

以下各節提供其他資源，您可在使用時參照 [!DNL SugarCRM] 來源。

### 护栏 {#guardrails}

此 [!DNL SugarCRM] API節流速率是每分鐘90次呼叫或每天2000次呼叫（以先發生者為準）。 不過，已藉由在連線規格中新增引數來規避此限制，這會延遲要求時間，使速率限制永遠無法達到。

### 验证 {#validation}

驗證您是否已正確設定來源及 [!DNL SugarCRM Accounts & Contacts] 正在擷取資料，請遵循下列步驟：

* 在Platform UI中選取 **[!UICONTROL 檢視資料流]** 旁邊 [!DNL SugarCRM Accounts & Contacts] 來源目錄上的卡片功能表。 接下來，選取 **[!UICONTROL 預覽資料集]** 驗證已擷取的資料。

* 根據您使用的物件型別，您可以根據上顯示的計數來驗證彙總資料 [!DNL SugarMarket] 下面的[帳戶]或[連絡人]頁面：

>[!BEGINTABS]

>[!TAB 帐户]

![SugarMarket帳戶頁面的熒幕擷圖顯示帳戶清單](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB 連絡人]

![SugarMarket連絡人頁面的熒幕擷圖顯示連絡人清單](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>此 [!DNL SugarMarket] 頁面不包含已刪除的物件計數。 不過，透過此來源擷取的資料也將包含已刪除的計數，這些將標示已刪除的旗標。
