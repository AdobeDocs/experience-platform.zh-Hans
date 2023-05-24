---
solution: Experience Platform
title: 雲端儲存空間目的地的API移轉指南
description: 瞭解工作流程中的變更，以在移轉至具有其他功能的新雲端儲存體目的地卡片時，啟用雲端儲存體目的地。
type: Tutorial
exl-id: 4acaf718-794e-43a3-b8f0-9b19177a2bc0
source-git-commit: 8ca63586855f2c62231662906646eb8abcfdcc0e
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# 雲端儲存空間目的地的API移轉指南

>[!IMPORTANT]
>
>* 已購買Real-Time CDP Prime和Ultimate套件的客戶可以使用本頁所述的功能。 如需詳細資訊，請聯絡您的Adobe代表。


## 移轉內容 {#migration-context}

正在啟動 [2022年10月](/help/release-notes/2022/october-2022.md#new-or-updated-destinations)，則在從Experience Platform匯出檔案時，您可以使用新的檔案匯出功能來存取增強的自訂功能：

* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).
* 可透過以下方式設定匯出檔案中的自訂檔案標頭： [新對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* 能夠選取 [檔案型別](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 匯出檔案的URL。
* 能夠 [自訂匯出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md).

以下列出的Beta版雲端儲存卡支援此功能：

* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

<!--

Commenting out the three net new cloud storage destinations

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)

-->

請注意，目前在Experience PlatformUI中，您可以看到三個目的地的兩個並排目的地卡片。 以下顯示為 [!DNL Amazon S3] 舊版和新的目的地。 在所有情況下，卡片都標有 **Beta** 是新的目的地卡。

![並排檢視中的兩個Amazon S3目的地卡片影像。](../assets/catalog/cloud-storage/amazon-s3/two-amazons3-destination-cards.png)

雖然這些具有增強功能的目的地最初是以測試版的形式提供， *Adobe現在正將所有Real-Time CDP客戶移至新的雲端儲存目的地*. 針對已使用的客戶 [!DNL Amazon S3]， [!DNL Azure Blob]或SFTP，這表示現有資料流將移轉到新卡片。 請閱讀下文，深入瞭解移轉作業中的特定變更。

## 此頁面的適用對象 {#who-this-applies-to}

如果您已使用 [流程服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 若要將設定檔匯出至Amazon S3、Azure Blob或SFTP雲端儲存空間目的地，則本API移轉指南適用於您。

如果您在中執行指令碼， [!DNL Amazon S3]， [!DNL Azure Blob]或是SFTP雲端儲存位置(位於從Experience Platform匯出的檔案上方)，請注意，一些引數會隨著新卡片的連線和流量規格，以及對應步驟而改變。

例如，如果您使用指令碼將目的地資料流篩選至 [!DNL Amazon S3] 目的地，根據 [!DNL Amazon S3] 目的地，請注意，連線規格將會變更，因此您需要更新篩選器。

## 相關檔案連結 {#relevant-documentation-links}

本節包含相關的API教學課程和參考檔案，說明將資料匯出至雲端儲存目的地的增強功能。

<!--

TBD if we keep this link but will likely remove it

[Legacy API tutorial to export data to cloud storage destinations](/help/destinations/api/connect-activate-batch-destinations.md) (outdated, do not use anymore)

-->
* [將區段匯出至雲端儲存空間目的地的API教學課程](/help/destinations/api/activate-segments-file-based-destinations.md)
* [目的地流程服務API參考檔案](https://developer.adobe.com/experience-platform-apis/references/destinations/)

## 回溯不相容變更的摘要 {#summary-backwards-incompatible-changes}

遷移到新目的地後，您所有現有的資料流都將移至 [!DNL Amazon S3]， [!DNL Azure Blob]，和SFTP目的地現在會指派新的目標連線和基本連線。 設定檔對應步驟也會變更。 下文各節針對每個目的地摘要說明與回溯不相容的變更。 同時檢視 [目的地字彙表](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 有關下圖中術語的詳細資訊。

![移轉指南概觀影像](/help/destinations/assets/api/api-migration-guide/migration-guide-diagram.png)

### 對進行與回溯不相容的變更 [!DNL Amazon S3] 目的地 {#changes-amazon-s3-destination}

API使用者適用的回溯不相容變更已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Amazon S3] | 舊版 | 新建 |
|---------|----------|---------|
| 流量規格 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 1a0514a6-33d4-4c7f-aff8-594799c47549 |
| 連線規格 | 4890fc95-5a1f-4983-94bb-e060c08e3f81 | 4fce964d-3f37-408f-9778-e597338a21ee |

檢視完整舊版和新版基本連線和目標連線範例，以瞭解 [!DNL Amazon S3] （位於以下標籤中）。 建立下列專案的基礎連線所需的引數： [!DNL Amazon S3] 目的地不會變更。

同樣地，建立目標連線所需的引數沒有回溯不相容的變更。

>[!BEGINTABS]

>[!TAB 舊版基本連線與目標連線]

+++檢視舊版 [!DNL base connection] 的 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "amazon-s3",
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"640418e2-0000-0200-0000-6359b9ef0000\"",
  "etag": "\"640418e2-0000-0200-0000-6359b9ef0000\""
}
```

+++

+++檢視舊版 [!DNL target connection] 的 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "ee86d122-10d3-434b-81c7-7252e4d747a7",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
    "version": "1.0"
  },
  "params": {
    "mode": "S3",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "etag": "\"1609cd86-0000-0200-0000-63892cbb0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "ee86d122-10d3-434b-81c7-7252e4d747a7",
      "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本連線與目標連線]

+++檢視新增 [!DNL base connection] 的 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Amazon S3",
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Access Key",
    "params": {
      "authorizedDate": "2022-10-26",
      "s3SecretKey": "<your-secret-key>",
      "s3AccessKey": "<your-access-key>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"3708da21-0000-0200-0000-638940b10000\"",
  "etag": "\"3708da21-0000-0200-0000-638940b10000\""
}
```

+++

+++檢視新增 [!DNL target connection] 的 [!DNL Amazon S3]

```json {line-numbers="true" start-line="1" highlight="12, 16-27"}
{
  ...
  "name": "test 121",
  "baseConnectionId": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "path": "testpath",
    "bucketName": "test"
  },
  "version": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "etag": "\"1b0985c6-0000-0200-0000-638940b10000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d114c86f-fd47-4bb6-846c-cb1d15a00fe9",
      "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 對進行回溯不相容的變更 [!DNL Azure Blob] 目的地 {#changes-azure-blob-destination}

API使用者適用的回溯不相容變更已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| [!DNL Azure Blob] | 舊版 | 新建 |
|---------|----------|---------|
| 流量規格 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | 752d422f-b16f-4f0d-b1c6-26e448e3b388 |
| 連線規格 | e258278b-a4cf-43ac-b158-4fa0ca0d948b | 6d6b59bf-fb58-4107-9064-4d246c0e5bb2 |

檢視完整舊版和新版基本連線和目標連線範例，以瞭解 [!DNL Azure Blob] （位於以下標籤中）。 為Azure Blob目的地建立基礎連線所需的引數不會變更。

同樣地，建立目標連線所需的引數沒有回溯不相容的變更。

>[!BEGINTABS]

>[!TAB 舊版基本連線與目標連線]

+++檢視舊版 [!DNL base connection] 的 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "azure-blob",
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  }, 
  "version": "\"d000d23c-0000-0200-0000-6299051c0000\"",
  "etag": "\"d000d23c-0000-0200-0000-6299051c0000\""
}
```

+++

+++檢視舊版 [!DNL target connection] 的 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "d10fcecf-9963-4062-820c-0f878be98805",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
    "version": "1.0"
  },
  "params": {
    "mode": "AZURE_BLOB",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "etag": "\"cb0468ba-0000-0200-0000-631ab0790000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "d10fcecf-9963-4062-820c-0f878be98805",
      "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本連線與目標連線]

+++檢視新增 [!DNL base connection] 的 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "Azure Blob Storage",
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "authorizedDate": "2022-06-02",      
      "connectionString": "<your-connection-string>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"4008a892-0000-0200-0000-6389890d0000\"",
  "etag": "\"4008a892-0000-0200-0000-6389890d0000\""
}
```

+++

+++檢視新增 [!DNL target connection] 的 [!DNL Azure Blob]

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "v1",
  "description": "v2",
  "baseConnectionId": "1329d183-a3ee-4454-ab3f-e2388082bf29",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "Server-to-server",
    "container": "usdasda",
    "path": "v3"
  },
  "version": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "etag": "\"5509fe3f-0000-0200-0000-638a28880000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "1329d183-a3ee-4454-ab3f-e2388082bf29",
      "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### SFTP目的地的回溯不相容變更 {#changes-sftp-destination}

API使用者適用的回溯不相容變更已更新 `connection spec ID` 和 `flow spec ID` 如下表所示：

| SFTP | 舊版 | 新建 |
|---------|----------|---------|
| 流量規格 | 71471eba-b620-49e4-90fd-23f1fa0174d8 | fd36aaa4-bf2b-43fb-9387-43785eeeb799 |
| 連線規格 | 64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0 | 36965a81-b1c6-401b-99f8-22508f1e6a26 |

除了上述更新的流程和連線規格，建立SFTP基本連線時所需的引數也會變更。

* 以前，SFTP目的地的基本連線需要 `host` 引數。 此引數現已重新命名為 `domain`.
* 對於使用SSH金鑰的驗證選項，基礎連線中的驗證引數需要 `port` 選項。 此引數現已棄用，不再需要。

在下列標籤中檢視SFTP的完整舊版和新版基本連線和目標連線範例，並反白顯示變更的行。 為SFTP目的地建立目標連線所需的引數不會變更。

>[!BEGINTABS]

>[!TAB 舊版基本連線與目標連線]

+++檢視舊版 [!DNL base connection] 對於SFTP — 密碼驗證

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "password": "<your-password>",
      "userName": "DPID12345",
      "host": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++檢視舊版 [!DNL base connection] 的 [!DNL SFTP - SSH key] 驗證

```json {line-numbers="true" start-line="1" highlight="5,15"}
{
  ...
  "name": "sftp",
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "sshKey": "<your-ssh-key>",
      "userName": "DPID12345",
      "port": 22
      "domain": "ftp-out.demdex.com"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"d000013c-0000-0200-0000-629903bd0000\"",
  "etag": "\"d000013c-0000-0200-0000-629903bd0000\""
}
```

+++

+++檢視舊版 [!DNL target connection] 適用於SFTP

```json {line-numbers="true" start-line="1" highlight="13"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
    "version": "1.0"
  },
  "params": {
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "etag": "\"8503ab91-0000-0200-0000-629903ce0000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "e6f3a300-0bf7-4755-b7f8-308dc2a99133",
      "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!TAB 新的基本連線與目標連線]

+++檢視新增 [!DNL base connection] 的 [!DNL SFTP - password authentication]

```json {line-numbers="true" start-line="1" highlight="5"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "password": "<your-password>"
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++檢視新增 [!DNL base connection] 的 [!DNL SFTP - SSH key] 驗證

```json {line-numbers="true" start-line="1" highlight="5,12"}
{
  ...
  "name": "SFTP",
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "state": "enabled",
  "auth": {
    "specName": "Basic Authentication for sftp",
    "params": {
      "authorizedDate": "2022-06-02",
      "domain": "ftp-out.demdex.com",
      "username": "DPID12345",
      "sshKey": "<your-ssh-key>",
    }
  },
  "encryption": {
    "specName": "File Encryption",
    "params": {
      "encryptionAlgo": "PGP/GPG",
      "publicKey": "<publicKey>"
    }
  },
  "version": "\"420826cc-0000-0200-0000-638999a60000\"",
  "etag": "\"420826cc-0000-0200-0000-638999a60000\""
}
```

+++

+++檢視新增 [!DNL target connection] 適用於SFTP

```json {line-numbers="true" start-line="1" highlight="13, 17-25"}
{
  ...
  "name": "test sftp 6/2",
  "description": "",
  "baseConnectionId": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
  "state": "enabled",
  "data": {
    "format": "CSV",
    "schema": null,
    "properties": null
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
    "version": "1.0"
  },
  "params": {
    "csvOptions": {
      "nullValue": "null",
      "emptyValue": "",
      "escape": "\\",
      "quote": "",
      "delimiter": ","
    },
    "compression": "NONE",
    "fileType": "CSV",
    "mode": "FTP",
    "remotePath": "test"
  },
  "version": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "etag": "\"5509b5cf-0000-0200-0000-638a2ab60000\"",
  "inheritedAttributes": {
    "baseConnection": {
      "id": "af63fbe1-45ff-4722-a9de-fbbe789dc7b0",
      "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
        "version": "1.0"
      }
    }
  }
}
```

+++

>[!ENDTABS]

### 與下列專案相同的回溯不相容變更： [!DNL Amazon S3]， [!DNL Azure Blob]和SFTP目的地 {#changes-all-destinations}

所有三個目的地的設定檔選擇器步驟都由對應步驟取代，該步驟允許您根據需要重新命名匯出檔案中的欄標題。 請檢視下方的並排影像，左側顯示舊的屬性選取器步驟，右側顯示新的對應步驟。

![移轉指南概觀影像](/help/destinations/assets/api/api-migration-guide/old-and-new-mapping-step.png)

請留意 `profileSelectors` 舊版範例中的物件會取代為新的 `profileMapping` 物件。

尋找關於設定的完整資訊 `profileMapping` 中的物件 [將資料匯出至雲端儲存空間目的地的API教學課程](/help/destinations/api/activate-segments-file-based-destinations.md#attribute-and-identity-mapping).

>[!BEGINTABS]

>[!TAB 舊轉換引數]

+++檢視舊轉換引數的範例

```json{line-numbers="true" start-line="1" highlight="4-40, 45-53"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "profileSelectors": {
    "selectors": [
      {
        "type": "JSON_PATH",
        "value": {
          "path": "CORE",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "CORE",
            "destination": "CORE",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "CORE",
            "destinationXdmPath": "CORE"
          },
          "identity": {
            "namespace": "CORE"
          }
        }
      },
      ...
      {
        "type": "JSON_PATH",
        "value": {
          "path": "segmentMembership.status",
          "operator": "EXISTS",
          "mapping": {
            "sourceType": "text/x.schema-path",
            "source": "segmentMembership.status",
            "destination": "segmentMembership.status",
            "identity": false,
            "primaryIdentity": false,
            "functionVersion": 0,
            "sourceAttribute": "segmentMembership.status",
            "destinationXdmPath": "segmentMembership.status"
          }
        }
      }
    ],
    "mandatoryFields": [
      "CORE",
      "person.name.lastName",
      "personalEmail.address"
    ],
    "primaryFields": [
      {
        "identityNamespace": "CORE",
        "fieldType": "IDENTITY"
      }
    ]
  }
}
```

+++

>[!TAB 新轉換引數]

+++檢視移轉後的轉換引數範例

請注意以下設定範例中如何 `profileSelectors` 欄位已取代為 `profileMapping` 物件。

```json {line-numbers="true" start-line="1" highlight="4-12, 18-20"}
{
  "segmentSelectors": { // shortened for brevity since nothing changes in the segment selectors
  },  
  "mandatoryFields": [
    "CORE",
    "person_name_lastName",
    "personalEmail_address"
  ],
  "primaryFields": [
    {
      "identityNamespace": "CORE",
      "fieldType": "IDENTITY"
    }
  ],
  "identityMapping": {
    "mappings": []
  },
  "profileMapping": {
    "mappingId": "40dfd952fe09498ba65145c7a5de3e07",
    "mappingVersion": 0
  },
  "attributeMapping": {}
}
```

+++

>[!ENDTABS]

## 移轉時間表與動作專案 {#timeline-and-action-items}

將舊式資料流移轉至的新目的地卡 [!DNL Amazon S3]， [!DNL Azure Blob]，而當您的組織準備好進行移轉時，SFTP目標就會立即發生，並且最晚不得晚於 **2023年6月30日**.

當移轉日期臨近時，您將會收到Adobe的提醒電子郵件。 在進行準備時，請閱讀下方的「行動專案」區段，為移轉做好準備。

### 動作專案 {#action-items}

為移轉做準備 [!DNL Amazon S3]， [!DNL Azure Blob]，以及SFTP雲端儲存空間目的地到新卡片，請準備更新您的指令碼和自動化API呼叫，如下所示。

1. 更新任何現有的指令碼或自動化API呼叫 [!DNL Amazon S3]， [!DNL Azure Blob]或SFTP雲端儲存目標。 任何運用舊版連線規格或流量規格的自動化API呼叫或指令碼，都必須更新至新的連線規格或流量規格。
2. 當您的指令碼在6月30日之前更新時，請洽詢您的Adobe客戶代表。
3. 例如， `targetConnectionSpecId` 可作為旗標，判斷資料流是否已移轉至新的目的地卡。 您可以使用以下更新指令碼 `if` 檢視舊版和更新後目標連線規格的條件 `flow.inheritedAttributes.targetConnections[0].connectionSpec.id` 並判斷資料流是否已移轉。 您可以在此頁面的特定區段中，檢視每個目的地的舊有及新連線規格ID。
4. 您的Adobe帳戶團隊將會取得資料流何時移轉的詳細資訊。
5. 6月30日之後，所有資料流都將進行移轉。 所有現有資料流現在都會有新的流量實體（連線規格、流量規格、基本連線和目標連線）。 您這邊使用舊版流量實體的任何指令碼或API呼叫都將停止運作。

## 其他移轉考量事項 {#other-considerations}

請注意，在移轉期間或移轉之後，現有的匯出排程不受影響。

## 后续步骤 {#next-steps}

閱讀本頁面後，您現在瞭解是否需要採取任何動作，才能為雲端儲存空間的移轉做好準備。 當您設定API型工作流程，以將檔案從Experience Platform匯出至您偏好的雲端儲存空間目的地時，您也會知道要參考哪些檔案頁面。 接下來，您可以檢視API教學課程，到 [將資料匯出至雲端儲存目標](/help/destinations/api/activate-segments-file-based-destinations.md).
