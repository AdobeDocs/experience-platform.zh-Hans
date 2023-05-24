---
title: 加密的資料擷取
description: Adobe Experience Platform可讓您透過雲端儲存批次來源內嵌加密的檔案。
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: 8531459da97be648d0a63ffc2af77ce41124585d
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# 加密的資料擷取

Adobe Experience Platform可讓您透過雲端儲存批次來源內嵌加密的檔案。 透過加密的資料擷取，您可以運用非對稱的加密機制，將批次資料安全地傳輸至Experience Platform。 目前，支援的非對稱加密機製為PGP和GPG。

加密的資料擷取程式如下：

1. [使用Experience PlatformAPI建立加密金鑰組](#create-encryption-key-pair). 加密金鑰組由私密金鑰和公開金鑰組成。 建立後，您可以複製或下載公開金鑰，以及其對應的公開金鑰ID和到期時間。 在此過程中，私密金鑰將由Experience Platform儲存在安全的儲存庫中。 **注意：** 回應中的公開金鑰以Base64編碼，且必須在使用前解密。
2. 使用公開金鑰來加密您要擷取的資料檔案。
3. 將加密檔案放入雲端儲存空間。
4. 加密檔案準備就緒後， [為您的雲端儲存空間來源建立來源連線和資料流](#create-a-dataflow-for-encrypted-data). 在流程建立步驟中，您必須提供 `encryption` 並包含您的公開金鑰ID。
5. Experience Platform會從安全儲存庫中擷取私密金鑰，以在擷取資料時解密資料。

>[!IMPORTANT]
>
>單一加密檔案的大小上限為1 GB。 例如，您可以在單一資料流執行中擷取價值2 GB的資料，但該資料中的任何個別檔案不能超過1 GB。

本檔案提供的步驟說明如何產生加密金鑰組，以加密您的資料，並使用雲端儲存來源將加密的資料擷取到Experience Platform。

## 快速入门

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
   * [雲端儲存空間來源](../api/collect/cloud-storage.md)：建立資料流，將雲端儲存空間來源中的批次資料帶入Experience Platform。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 建立加密金鑰組 {#create-encryption-key-pair}

將加密資料擷取至Experience Platform的第一步，是透過向發出POST要求來建立您的加密金鑰組。 `/encryption/keys` 的端點 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/encryption/keys
```

**请求**

下列要求會使用PGP加密演演算法產生加密金鑰組。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `encryptionAlgorithm` | 您使用的加密演演算法型別。 支援的加密型別包括 `PGP` 和 `GPG`. |
| `params.passPhrase` | 密碼可為您的加密金鑰提供額外的保護層。 建立後，Experience Platform會將複雜密碼與公開金鑰儲存在不同的安全儲存庫中。 您必須提供非空白字串作為複雜密碼。 |

**响应**

成功回應會傳回Base64編碼的公開金鑰、公開金鑰ID和金鑰的到期時間。 到期時間會自動設定為金鑰產生日期後的180天。 到期時間目前無法設定。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## 使用將您的雲端儲存空間來源連線至Experience Platform [!DNL Flow Service] API

擷取加密金鑰組後，您現在可以繼續並為雲端儲存空間來源建立來源連線，並將加密的資料帶到Platform。

首先，您必須建立基礎連線，以針對Platform驗證您的來源。 若要建立基本連線並驗證您的來源，請從下列清單中選取您要使用的來源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure檔案儲存體](../api/create/cloud-storage/azure-file-storage.md)
* [数据登陆区](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google雲端儲存空間](../api/create/cloud-storage/google.md)
* [oracle物件儲存](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

建立基礎連線後，您必須遵循的教學課程中概述的步驟 [為雲端儲存空間來源建立來源連線](../api/collect/cloud-storage.md) 以建立來源連線、目標連線和對應。

## 為加密的資料建立資料流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>您必須具備下列條件，才能建立資料流以進行加密的資料擷取：
>* [公開金鑰ID](#create-encryption-key-pair)
>* [來源連線ID](../api/collect/cloud-storage.md#source)
>* [目標連線ID](../api/collect/cloud-storage.md#target)
>* [映射 ID](../api/collect/cloud-storage.md#mapping)


若要建立資料流，請向以下發出POST請求： `/flows` 的端點 [!DNL Flow Service] API。 若要內嵌加密的資料，您必須新增 `encryption` 區段至 `transformations` 屬性並包含 `publicKeyId` 之前步驟中建立的其他檔案。

**API格式**

```http
POST /flows
```

**请求**

以下請求會建立資料流，以擷取雲端儲存空間來源的加密資料。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 與雲端儲存空間來源對應的流量規格ID。 |
| `sourceConnectionIds` | 來源連線識別碼。 此ID代表資料從來源傳輸至Platform的過程。 |
| `targetConnectionIds` | 目標連線ID。 此ID代表資料傳至Platform後著陸的位置。 |
| `transformations[x].params.mappingId` | 對應ID。 |
| `transformations.name` | 擷取加密檔案時，您必須提供 `Encryption` 作為資料流的其他轉換引數。 |
| `transformations[x].params.publicKeyId` | 您建立的公開金鑰ID。 此ID是用來加密雲端儲存體資料的加密金鑰組的一半。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間計）。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`， `minute`， `hour`， `day`，或 `week`. |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔值應為非零整數。 當頻率設定為時，不需要間隔 `once` 和應大於或等於 `15` （其他頻率值）。 |

**响应**

成功的回應會傳回ID (`id`)中，所有新增的已加密資料流都會顯示這個訊息。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 后续步骤

依照本教學課程所述，您已針對雲端儲存空間資料建立加密金鑰組，並使用來擷取加密資料的資料流 [!DNL Flow Service API]. 如需資料流完整性、錯誤和量度的狀態更新，請閱讀以下指南： [使用監控資料流 [!DNL Flow Service] API](./monitor.md).
