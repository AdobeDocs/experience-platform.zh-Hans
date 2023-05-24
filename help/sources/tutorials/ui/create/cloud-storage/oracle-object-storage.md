---
keywords: Experience Platform；首頁；熱門主題；Oracle物件儲存；oracle物件儲存
solution: Experience Platform
title: 在UI中建立Oracle物件儲存來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Oracle物件儲存來源連線。
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 建立 [!DNL Oracle Object Storage] UI中的來源連線

本教學課程提供建立 [!DNL Oracle Object Storage] 來源連線使用Adobe Experience Platform UI。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

在中以連線到 [!DNL Oracle Object Storage]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 此 [!DNL Oracle Object Storage] 驗證所需的端點。 端點格式為： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 此 [!DNL Oracle Object Storage] 驗證所需的存取金鑰ID。 |
| `secretKey` | 此 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `bucketName` | 如果使用者擁有受限制的存取權，則需要允許的bucket名稱。 貯體名稱的長度必須介於3到63個字元之間，開頭和結尾必須是字母或數字，而且只能包含小寫字母、數字或連字型大小(`-`)。 儲存貯體名稱的格式不得類似於IP位址。 |
| `folderPath` | 如果使用者擁有受限存取權，則需要允許的資料夾路徑。 |

如需如何取得這些值的詳細資訊，請參閱 [oracle物件儲存驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

收集完所需的認證後，您可以依照下列步驟建立新的Oracle物件儲存體帳戶以連線至平台。

## 連線到Oracle物件儲存體

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選取 **[!UICONTROL oracle物件儲存]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Oracle Object Storage] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選擇性說明和您的 [!DNL Oracle Object Storage] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/oracle-object-storage/new.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Oracle Object Storage] 帳戶。 您現在可以繼續下一個教學課程： [設定資料流以將雲端儲存空間中的資料帶入Platform](../../dataflow/batch/cloud-storage.md).
