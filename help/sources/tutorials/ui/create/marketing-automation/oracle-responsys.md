---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；oracle；
title: （測試版）使用Platform UI建立OracleResponsys來源連線
description: 瞭解如何使用Platform UI將Adobe Experience Platform連線至OracleResponsys。
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta)建立 [!DNL Oracle Responsys] 使用Platform UI的來源連線

>[!NOTE]
>
>此 [!DNL Oracle Responsys] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

本教學課程提供您建立 [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) 使用Adobe Experience Platform使用者介面的來源連線。

## 快速入门

本指南需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)：Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Platform提供虛擬沙箱，可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

如果您已經驗證 [!DNL Oracle Responsys] 帳戶，然後您可以略過本檔案的其餘部分，並前往上的教學課程 [建立資料流以將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).

### 收集必要的認證

為了連線 [!DNL Oracle Responsys] 對於Platform，您必須提供下列驗證屬性的值：

| 認證 | 描述 |
| --- | --- |
| 端點 | 您的REST驗證端點URL [!DNL Oracle Responsys] 執行個體。 |
| 使用者端ID | 您的使用者端識別碼 [!DNL Oracle Responsys] 執行個體。 |
| 使用者端密碼 | 您的使用者端密碼 [!DNL Oracle Responsys] 執行個體。 |

如需下列專案的驗證認證詳細資訊： [!DNL Oracle Responsys]，請參閱 [[!DNL Oracle Responsys] 驗證指南](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Oracle Responsys] 至平台的帳戶。

## 連線您的 [!DNL Oracle Responsys] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 行銷自動化] 類別，選取 **[!UICONTROL oracleResponsys]**，然後選取 **[!UICONTROL 新增資料]**.

![反白顯示Oracle為Responsys來源的Adobe Experience Platform來源目錄。](../../../../images/tutorials/create/oracle-responsys/catalog.png)

此 **[!UICONTROL 連線OracleResponsys帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Oracle Responsys] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![oracleResponsys的現有帳戶驗證畫面。](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 新帳戶

若要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和適合您的專案的適當值。 [!DNL Oracle Responsys] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![oracleResponsys的新帳戶驗證畫面。](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 后续步骤

依照本教學課程所述，您已驗證並建立您與 [!DNL Oracle Responsys] 帳戶和平台。 您現在可以繼續下一節教學課程和 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).
