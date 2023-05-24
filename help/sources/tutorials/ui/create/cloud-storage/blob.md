---
title: 在使用者介面中建立Azure Blob來源連線
description: 瞭解如何使用Platform使用者介面建立Azure Blob來源聯結器。
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# 建立 [!DNL Azure Blob] ui中的來源連線

本教學課程提供建立 [!DNL Azure Blob] (以下稱&quot;[!DNL Blob]&quot;)來源連線使用Platform使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：以Experience Platform組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Blob] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 支持的文件格式

Experience Platform支援從外部儲存體擷取下列檔案格式：

* 分隔符號分隔值(DSV)：您可以使用任何單一欄分隔符號（例如定位字元、逗號、垂直號、分號或雜湊）來收集任何格式的平面檔案。
* JavaScript物件標籤法(JSON)： JSON格式資料檔案必須符合XDM規範。
* Apache Parquet： Parquet格式資料檔案必須符合XDM標準。

### 收集必要的認證

為了存取您的 [!DNL Blob] 存放於Platform時，您必須提供下列認證的有效值：

| 認證 | 描述 |
| ---------- | ----------- |
| 連線字串 | 包含驗證所需授權資訊的字串 [!DNL Blob] 以Experience Platform。 此 [!DNL Blob] 連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 如需有關連線字串的詳細資訊，請參閱此 [!DNL Blob] 檔案於 [設定連線字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| SAS URI | 共用存取簽章URI，您可將其作為替代驗證型別來連線 [!DNL Blob] 帳戶。 此 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 如需詳細資訊，請參閱此 [!DNL Blob] 檔案於 [共用存取權簽章URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| 容器 | 您要指定存取權的容器名稱。 使用建立新帳戶時 [!DNL Blob] 來源，您可以提供容器名稱，以指定使用者對所選子資料夾的存取權。 |
| 文件夹路径 | 您要提供存取權的資料夾路徑。 |

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Blob] 至平台的帳戶。

## 連線您的 [!DNL Blob] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選取 **[!UICONTROL Azure Blob儲存體]**，然後選取 **[!UICONTROL 新增資料]**.

![已選取Azure Blob儲存體來源的Experience Platform來源目錄。](../../../../images/tutorials/create/blob/catalog.png)

此 **[!UICONTROL 連線到Azure Blob儲存體]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Blob] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/blob/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後為您的新提供名稱和說明（選用） [!DNL Blob] 帳戶。

![Azure Blob儲存體來源的新帳戶畫面。](../../../../images/tutorials/create/blob/new.png)

此 [!DNL Blob] 來源支援帳戶金鑰驗證和共用存取簽章(SAS)驗證。 帳戶金鑰型驗證需要連線字串來進行驗證，而SAS驗證則使用URI，允許對您的帳戶進行安全委派的授權。

在此步驟中，您還可以定義容器的名稱和子資料夾的路徑，以指定您的帳戶將有權存取的子資料夾。

>[!BEGINTABS]

>[!TAB 連線字串]

若要使用帳戶金鑰進行驗證，請選取 **[!UICONTROL 帳戶金鑰驗證]** 並提供您的連線字串。 在此步驟中，您也可以指定容器名稱和要存取的子資料夾路徑。 完成後，選取 **[!UICONTROL 連線到來源]**.

![連線字串](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB SAS URI]

您可以使用SAS建立具有不同存取許可權的驗證認證，因為以SAS為基礎的驗證可讓您設定許可權、開始和到期日，以及特定資源的布建。

若要使用共用存取權簽名進行驗證，請選取 **[!UICONTROL 共用存取權簽名驗證]** 然後提供您的SAS URI。 在此步驟中，您也可以指定容器名稱和要存取的子資料夾路徑。 完成後，選取 **[!UICONTROL 連線到來源]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Blob] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流，將雲端儲存空間中的資料匯入Platform](../../dataflow/batch/cloud-storage.md).
