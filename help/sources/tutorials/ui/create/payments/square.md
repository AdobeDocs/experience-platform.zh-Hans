---
keywords: Experience Platform；首頁；熱門主題；方形；方形
title: 在UI中建立方形來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立方形來源連線。
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# 建立 [!DNL Square] ui中的來源連線

本教學課程提供建立 [!DNL Square] 使用Platform使用者介面的來源聯結器。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 收集必要的認證

為了存取您的 [!DNL Square] 帳戶平台，您必須提供下列值：

| 認證 | 描述 |
| --- | --- |
| Host | 的URL [!DNL Square] 執行個體。 |
| 使用者端ID | 與您的關聯的使用者端ID [!DNL Square] 帳戶。 |
| 使用者端密碼 | 與您的關聯的使用者端密碼 [!DNL Square] 帳戶。 |
| 存取權杖 | 存取權杖會用於驗證您的 [!DNL Square] 具有OAuth 2.0驗證的帳戶。 存取權杖可以從 [!DNL Square]. |
| 重新整理Token | 重新整理Token可在您目前的存取Token過期後，用來產生新的存取Token。 重新整理權杖可以從 [!DNL Square]. |

如需這些認證以及如何取得認證的詳細資訊，請參閱 [[!DNL Square] oauth上的檔案](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Square] 至平台的帳戶。

## 連線您的 [!DNL Square] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 付款] 類別，選取 **[!UICONTROL 方形]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/square/catalog.png)

此 **[!UICONTROL 連線至方形]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Square] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/square/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和適合您的專案的適當值。 [!DNL Square] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/square/new.png)

## 后续步骤

依照本教學課程所述，您已驗證並建立您與 [!DNL Square] 帳戶和平台。 您現在可以繼續下一節教學課程和 [建立資料流以將付款資料帶入Platform](../../dataflow/payments.md).
