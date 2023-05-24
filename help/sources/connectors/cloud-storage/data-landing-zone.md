---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 資料登陸區域來源
description: 瞭解如何將Data Landing Zone連結至Adobe Experience Platform
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: d57060ddeed64d3863f71ac1ea34ccc5c97265ea
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# [!DNL Data Landing Zone]

>[!IMPORTANT]
>
>此頁面專屬於 [!DNL Data Landing Zone] *source* Experience Platform中的聯結器。 如需有關連線至 [!DNL Data Landing Zone] *目的地* 聯結器，請參閱 [[!DNL Data Landing Zone] 目的地檔案頁面](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存體介面，可授予您存取安全、雲端式的檔案儲存設施，以將檔案帶入Platform。 您可以存取一個 [!DNL Data Landing Zone] 容器，以及所有容器的總資料量，皆以您的Platform產品和服務授權所提供的總資料為限。 Platform及其應用程式服務的所有客戶，例如 [!DNL Customer Journey Analytics]， [!DNL Journey Orchestration]， [!DNL Intelligent Services]、和 [!DNL Adobe Real-Time Customer Data Platform] 已布建一個 [!DNL Data Landing Zone] 每個沙箱的容器。 您可以透過讀取檔案並將檔案寫入容器 [!DNL Azure Storage Explorer] 或您的命令列介面。

[!DNL Data Landing Zone] 支援以SAS為基礎的驗證，其資料受到標準的保護 [!DNL Azure Blob] 存放區安全機制處於閒置狀態及運送中。 SAS式驗證可讓您安全地存取 [!DNL Data Landing Zone] 透過公用網際網路連線的容器。 您不需要變更網路即可存取 [!DNL Data Landing Zone] 容器，這表示您不需要為網路設定任何允許清單或跨區域設定。 Platform對上傳至的所有檔案強制實施嚴格的七天過期時間 [!DNL Data Landing Zone] 容器。 所有檔案會在七天後刪除。

## 檔案和目錄的命名限制

以下是您在命名雲端儲存體檔案或目錄時必須考慮的限制清單。

- 目錄和檔案元件名稱不能超過255個字元。
- 目錄和檔案名稱不能以正斜線(`/`)。 如果提供，則會自動移除。
- 下列保留的URL字元必須正確逸出： `! ' ( ) ; @ & = + $ , % # [ ]`
- 不允許使用下列字元： `" \ / : | < > * ?`.
- 不允許非法URL路徑字元。 程式碼點數類似 `\uE000`雖然在NTFS檔案名稱中有效，但不是有效的Unicode字元。 此外，還有一些ASCII或Unicode字元，例如控制字元(例如 `0x00` 至 `0x1F`， `\u0081`、等等)之外，也不可使用。 如需HTTP/1.1中Unicode字串的相關規則，請參閱 [RFC 2616，第2.2節：基本規則](https://www.ietf.org/rfc/rfc2616.txt) 和 [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- 不允許下列檔案名稱：LPT1、LPT2、LPT3、LPT4、LPT5、LPT6、LPT7、LPT8、LPT9、COM1、COM2、COM3、COM4、COM5、COM6、COM7、COM8、COM9、PRN、AUX、NUL、CON、CLOCK$、點字元(.)，以及兩個點字元(...)。

## 管理內容 [!DNL Data Landing Zone]

您可以使用 [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) 管理您的網站內容： [!DNL Data Landing Zone] 容器。

在 [!DNL Azure Storage Explorer] UI中，選取左側導覽中的連線圖示。 此 **選取資源** 視窗隨即出現，為您提供可連線的選項。 選取 **[!DNL Blob container]** 以連線到 [!DNL Data Landing Zone].

![select-resource](../../images/tutorials/create/dlz/select-resource.png)

接下來，選取 **共用存取權簽章URL (SAS)** 作為您的連線方法，然後選取 **下一個**.

![select-connection-method](../../images/tutorials/create/dlz/select-connection-method.png)

選取連線方法後，您必須接著提供 **顯示名稱** 和 **[!DNL Blob]容器SAS URL** 與您的 [!DNL Data Landing Zone] 容器。

>[!TIP]
>
>您可以擷取 [!DNL Data Landing Zone] 來自Platform UI中來源目錄的認證。

提供您的 [!DNL Data Landing Zone] SAS URL，然後選取 **下一個**

![enter-connection-info](../../images/tutorials/create/dlz/enter-connection-info.png)

此 **摘要** 視窗會出現，為您提供設定的概觀，包括您的設定的 [!DNL Blob] 端點與許可權。 準備就緒後，選擇 **Connect**.

![摘要](../../images/tutorials/create/dlz/summary.png)

成功的連線會更新您的 [!DNL Azure Storage Explorer] 包含您的UI [!DNL Data Landing Zone] 容器。

![dlz-user-container](../../images/tutorials/create/dlz/dlz-user-container.png)

搭配您的 [!DNL Data Landing Zone] 容器已連線至 [!DNL Azure Storage Explorer]，您現在可以開始將檔案上傳至 [!DNL Data Landing Zone] 容器。 若要上傳，請選取 **上傳** 然後選取 **上傳檔案**.

![上傳](../../images/tutorials/create/dlz/upload.png)

選取要上傳的檔案後，您必須識別 [!DNL Blob] 輸入您要上傳的檔案作為和您想要的目的地目錄。 完成後，選取 **上傳**.

| [!DNL Blob] 类型 | 描述 |
| --- | --- |
| 區塊 [!DNL Blob] | 區塊 [!DNL Blobs] 針對以有效率的方式上傳大量資料而最佳化。 區塊 [!DNL Blobs] 為的預設選項 [!DNL Data Landing Zone]. |
| 附加 [!DNL Blob] | 附加 [!DNL Blobs] 已針對在檔案結尾附加資料而最佳化。 |

![upload-file](../../images/tutorials/create/dlz/upload-files.png)

## 上傳檔案至您的 [!DNL Data Landing Zone] 使用命令列介面

您也可以使用裝置的命令列介面，並存取上傳檔案至 [!DNL Data Landing Zone].

### 使用Bash上傳檔案

以下範例使用Bash和cURL將檔案上傳至 [!DNL Data Landing Zone] 使用 [!DNL Azure Blob Storage] REST API：

```shell
# Set Azure Blob-related settings
DATE_NOW=$(date -Ru | sed 's/\+0000/GMT/')
AZ_VERSION="2018-03-28"
AZ_BLOB_URL="<URL TO BLOB ACCOUNT>"
AZ_BLOB_CONTAINER="<BLOB CONTAINER NAME>"
AZ_BLOB_TARGET="${AZ_BLOB_URL}/${AZ_BLOB_CONTAINER}"
AZ_SAS_TOKEN="<SAS TOKEN, STARTING WITH ? AND ENDING WITH %3D>"

# Path to the file we wish to upload
FILE_PATH="</PATH/TO/FILE>"
FILE_NAME=$(basename "$FILE_PATH")

# Execute HTTP PUT to upload file (remove '-v' flag to suppress verbose output)
curl -v -X PUT \
   -H "Content-Type: application/octet-stream" \
   -H "x-ms-date: ${DATE_NOW}" \
   -H "x-ms-version: ${AZ_VERSION}" \
   -H "x-ms-blob-type: BlockBlob" \
   --data-binary "@${FILE_PATH}" "${AZ_BLOB_TARGET}/${FILE_NAME}${AZ_SAS_TOKEN}"
```

### 使用Python上傳檔案

以下範例使用 [!DNL Microsoft's] Python v12 SDK上傳檔案至 [!DNL Data Landing Zone]：

>[!TIP]
>
>雖然下列範例使用完整的SAS URI來連線至 [!DNL Azure Blob] 容器，則可以使用其他方法和操作來進行驗證。 檢視此 [[!DNL Microsoft] Python v12 SDK上的檔案](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-python) 以取得詳細資訊。

```py
import os
from azure.storage.blob import ContainerClient

try:
    # Set Azure Blob-related settings
    sasUri = "<SAS URI>"
    srcFilePath = "<FULL PATH TO FILE>" 
    srcFileName = os.path.basename(srcFilePath)

    # Connect to container using SAS URI
    containerClient = ContainerClient.from_container_url(sasUri)

    # Upload file to Data Landing Zone with overwrite enabled
    with open(srcFilePath, "rb") as fileToUpload:
        containerClient.upload_blob(srcFileName, fileToUpload, overwrite=True)

except Exception as ex:
    print("Exception: " + ex.strerror)
```

### 上傳檔案，使用 [!DNL AzCopy]

以下範例使用 [!DNL Microsoft's] [!DNL AzCopy] 上傳檔案至的公用程式 [!DNL Data Landing Zone]：

>[!TIP]
>
>雖然以下範例是使用 `copy` 命令，您可使用其他命令和選項將檔案上傳至 [!DNL Data Landing Zone]，使用 [!DNL AzCopy]. 檢視此 [[!DNL Microsoft AzCopy] 檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-ref-azcopy?toc=/azure/storage/blobs/toc.json) 以取得詳細資訊。

```bat
set sasUri=<FULL SAS URI, PROPERLY ESCAPED>
set srcFilePath=<PATH TO LOCAL FILE(S); WORKS WITH WILDCARD PATTERNS>

azcopy copy "%srcFilePath%" "%sasUri%" --overwrite=true --recursive=true
```

## Connect [!DNL Data Landing Zone] 至 [!DNL Platform]

以下檔案提供如何從匯入資料的資訊 [!DNL Data Landing Zone] 使用API或使用者介面的Adobe Experience Platform容器。

### 使用API

- [建立 [!DNL Data Landing Zone] 使用流量服務API的來源連線](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [使用流量服務API為雲端儲存空間來源建立資料流](../../tutorials/api/collect/cloud-storage.md)

### 使用UI

- [Connect [!DNL Data Landing Zone] 使用UI移至Platform](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [在UI中建立雲端儲存體連線的資料流](../../tutorials/ui/dataflow/batch/cloud-storage.md)
