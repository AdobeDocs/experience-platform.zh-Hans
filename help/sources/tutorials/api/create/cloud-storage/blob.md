---
title: 使用流量服務API建立Azure Blob基本連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Azure Blob。
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# 建立 [!DNL Azure Blob] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Azure Blob] (以下稱&quot;[!DNL Blob]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功建立所需的其他資訊 [!DNL Blob] 來源連線使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線您的 [!DNL Blob] 儲存，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `connectionString` | 包含驗證所需授權資訊的字串 [!DNL Blob] 以Experience Platform。 此 [!DNL Blob] 連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. 如需有關連線字串的詳細資訊，請參閱此 [!DNL Blob] 檔案於 [設定連線字串](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | 共用存取簽章URI，您可將其作為替代驗證型別來連線 [!DNL Blob] 帳戶。 此 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` 如需詳細資訊，請參閱此 [!DNL Blob] 檔案於 [共用存取權簽章URI](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | 您要指定存取權的容器名稱。 使用建立新帳戶時 [!DNL Blob] 來源，您可以提供容器名稱，以指定使用者對所選子資料夾的存取權。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Blob] 為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

此 [!DNL Blob] 來源支援連線字串和共用存取簽章(SAS)驗證。 共用存取簽章(SAS) URI允許將安全授權委派給您的 [!DNL Blob] 帳戶。 您可以使用SAS建立具有不同存取許可權的驗證認證，因為以SAS為基礎的驗證可讓您設定許可權、開始和到期日，以及特定資源的布建。

在此步驟中，您還可以定義容器的名稱和子資料夾的路徑，以指定您的帳戶將有權存取的子資料夾。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Blob] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

>[!BEGINTABS]

>[!TAB 連線字串]

下列要求會建立 [!DNL Blob] 使用連線字串型驗證：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
              "container": "acme-blob-container",
              "folderPath": "/acme/customers/salesData"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 存取Blob儲存體中的資料所需的連線字串。 Blob連線字串模式為： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Blob儲存體連線規格ID是： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!TAB SAS URI驗證]

若要建立 [!DNL Blob] 使用共用存取簽名URI的blob連線，向發出POST要求 [!DNL Flow Service] API同時為您的提供值 [!DNL Blob] `sasUri`.

下列要求會建立 [!DNL Blob] 使用共用存取權簽章URI：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
      "auth": {
          "specName": "SAS URI Authentication",
          "params": {
              "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
              "container": "acme-blob-container",
              "folderPath": "/acme/customers/salesData"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 存取中資料所需的SAS URI [!DNL Blob] 儲存。 此 [!DNL Blob] SAS URI模式為： `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | 此 [!DNL Blob] 儲存體連線規格ID為： `4c10e202-c428-4796-9208-5f1f5732b1cf` |

>[!ENDTABS]

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Blob] 使用API和唯一ID的連線已取得為回應本文的一部分。 您可以使用此連線ID來 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
