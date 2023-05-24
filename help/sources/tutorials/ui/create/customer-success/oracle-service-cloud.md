---
keywords: Experience Platform；首頁；熱門主題；Oracle服務雲端；oracle服務雲端
title: 在UI中建立Oracle服務雲端來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Oracle服務雲端來源連線。
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 在UI中建立Oracle服務雲端來源連線

本教學課程提供使用Adobe Experience Platform使用者介面建立Oracle服務雲端來源連線的步驟。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的Oracle服務雲端來源連線，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/customer-success.md)

### 收集必要的認證

若要存取您的Oracle服務雲端帳戶，請前往 [!DNL Platform]，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| Host | oracle服務雲端例項的主機URL。 |
| 用户名 | 您的Oracle服務雲端使用者帳戶使用者名稱。 |
| 密码 | 您的Oracle Service Cloud帳戶密碼。 |

如需驗證Oracle服務雲端帳戶的詳細資訊，請參閱 [[!DNL Oracle] 驗證指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## 連線您的Oracle服務雲端帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示可用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 客戶成功] 類別，選取 **[!UICONTROL oracle服務雲端]** 然後選取 **[!UICONTROL 新增資料]**.

![反白顯示Oracle服務雲端來源的來源目錄。](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

此 **[!UICONTROL 連線至Oracle Service Cloud]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Oracle服務雲端帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有的帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明和您的Oracle服務雲端憑證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![帶有預留位置值的新帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## 后续步骤

依照本教學課程所述，您已建立與您的Oracle Service Cloud帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流，將客戶成功資料匯入Platform](../../dataflow/crm.md).
