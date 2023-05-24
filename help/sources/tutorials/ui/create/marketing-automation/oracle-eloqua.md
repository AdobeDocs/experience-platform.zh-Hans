---
title: 使用Platform UI建立OracleEloqua來源連線
description: 瞭解如何使用Platform UI將Adobe Experience Platform連結至Oracle Eloqua。
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# 建立 [!DNL Oracle Eloqua] 使用Platform UI的來源連線

本教學課程提供建立 [!DNL Oracle Eloqua] 使用Adobe Experience Platform使用者介面的來源連線。

## 快速入门

本指南需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)：Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Platform提供虛擬沙箱，可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

如果您已經驗證 [!DNL Oracle Eloqua] 帳戶，然後您可以略過本檔案的其餘部分，並前往上的教學課程 [建立資料流以將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).

### 收集必要的認證

為了連線 [!DNL Oracle Eloqua] 對於Platform，您必須提供下列驗證屬性的值：

| 認證 | 描述 |
| --- | --- |
| 端點 | 您的的端點 [!DNL Oracle Eloqua] 伺服器。 [!DNL Oracle Eloqua] 支援多個資料中心。 若要尋找您的端點，請登入 [[!DNL Oracle Eloqua] 介面](https://login.eloqua.com) ，然後從重新導向URL複製基本URL部分。 URL模式的格式為 `xxx.xx.eloqua.com` 且輸入時應不包含 `http` 或 `https`. |
| 用户名 | 您的使用者名稱 [!DNL Oracle Eloqua] 伺服器。 使用者名稱的格式必須是 `siteName + \\ + username`，其中 `siteName` 是您用來登入的公司名稱 [!DNL Oracle Eloqua] 和 `username` 是您的使用者名稱。 例如，您的登入使用者名稱可以是： `Eloqua\Andy`. **注意**：您必須使用單一反斜線(`\`)使用UI時，因為Experience PlatformUI會自動新增額外的反斜線(`\`)時，輸入使用者名稱。 |
| 密码 | 與您的對應的密碼 [!DNL Oracle Eloqua] 使用者名稱。 |

如需下列專案的驗證認證詳細資訊： [!DNL Oracle Eloqua]，請參閱 [[!DNL Oracle Eloqua] 驗證指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Oracle Eloqua] 至平台的帳戶。

## 連線您的 [!DNL Oracle Eloqua] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 行銷自動化] 類別，選取 **[!UICONTROL oracleEloqua]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

此 **[!UICONTROL 連線Oracle Eloqua帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Oracle Eloqua] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和適合您的專案的適當值。 [!DNL Oracle Eloqua] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 后续步骤

依照本教學課程所述，您已驗證並建立您與 [!DNL Oracle Eloqua] 帳戶和平台。 您現在可以繼續下一節教學課程和 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).
