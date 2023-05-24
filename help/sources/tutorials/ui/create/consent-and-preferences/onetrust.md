---
keywords: Experience Platform；首頁；熱門主題；onetrust；OneTrust
solution: Experience Platform
title: 在使用者介面中建立OneTrust來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立OneTrust來源連線。
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# 建立 [!DNL OneTrust Integration] ui中的來源連線

>[!NOTE]
>
>此 [!DNL OneTrust Integration] 來源僅支援擷取同意和偏好設定資料，不支援Cookie。

本教學課程提供建立 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 來源連線，以使用Platform使用者介面將歷史同意資料和排程同意資料擷取到Adobe Experience Platform。

## 先决条件

>[!IMPORTANT]
>
>此 [!DNL OneTrust Integration] 來源聯結器和檔案是由 [!DNL OneTrust Integration] 團隊。 如有任何查詢或更新請求，請聯絡 [[!DNL OneTrust] 團隊](https://my.onetrust.com/s/contactsupport?language=en_US) 直接。

連線之前 [!DNL OneTrust Integration] 對於Platform，您必須先擷取存取權杖。 如需尋找存取權杖的詳細說明，請參閱 [[!DNL OneTrust Integration] OAuth 2指南](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

存取權杖過期後不會自動重新整理，因為系統間重新整理權杖不受支援 [!DNL OneTrust]. 因此，您必須確定您的存取權杖在過期之前已在連線中更新。 存取Token的最大可設定存留期為一年。 若要進一步瞭解如何更新存取權杖，請參閱 [[!DNL OneTrust] 有關管理您的OAuth 2.0使用者端憑證的檔案](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### 收集必要的認證

為了連線 [!DNL OneTrust Integration] 對於Platform，您必須提供下列驗證認證的值：

| 認證 | 描述 | 示例 |
| --- | --- | --- |
| 主機名稱 | 從中建立 [!DNL OneTrust Integration] 需要從中提取資料。 | `app.onetrust.com` |
| 授權測試URL | （選用）建立基本連線時，會使用授權測試URL來驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |  |
| 存取Token | 與您的對應的存取權杖 [!DNL OneTrust Integration] 帳戶。 | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

如需這些認證的詳細資訊，請參閱 [[!DNL OneTrust Integration] 驗證檔案](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## 連線您的 [!DNL OneTrust Integration] 帳戶

>[!NOTE]
>
>此 [!DNL OneTrust Integration] 正在與Adobe共用API規格以擷取資料。

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區以取得Experience Platform中可用的來源目錄。

使用 *[!UICONTROL 類別]* 功能表，依類別篩選來源。 或者，在搜尋列中輸入來源名稱，從目錄中尋找特定來源。

前往 [!UICONTROL 同意與偏好設定] 類別 [!DNL OneTrust Integration] 來源卡。 若要開始，請選取 **[!UICONTROL 新增資料]**.

![Experience PlatformUI來源目錄。](../../../../images/tutorials/create/onetrust/catalog.png)

此 **[!UICONTROL 連線OneTrust整合帳戶]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL OneTrust Integration] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程中的現有帳戶驗證步驟。](../../../../images/tutorials/create/onetrust/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![來源工作流程中的新帳戶驗證步驟。](../../../../images/tutorials/create/onetrust/new.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL OneTrust Integration] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將同意資料匯入Platform](../../dataflow/consent-and-preferences.md).
