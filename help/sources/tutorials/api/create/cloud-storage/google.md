---
title: 使用Flow Service API建立Google Cloud Storage基本連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Google雲端儲存空間帳戶。
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 3636b785d82fa2e49f76825650e6159be119f8b4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Google Cloud Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，才能使用成功連線到Google雲端儲存空間帳戶 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線您的 [!DNL Google Cloud Storage] 帳戶，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 至平台的帳戶。 |
| `secretAccessKey` | 40個字元的base-64編碼字串，用於驗證您的 [!DNL Google Cloud Storage] 至平台的帳戶。 |
| `bucketName` | 您的名稱 [!DNL Google Cloud Storage] 貯體。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，您必須指定貯體名稱。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 |

如需這些值的詳細資訊，請參閱 [Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概觀](../../../../connectors/cloud-storage/google-cloud-storage.md).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Google Cloud Storage] 要求引數中的驗證認證。

>[!TIP]
>
>在此步驟中，您還可以定義貯體名稱和子資料夾的路徑，以指定您的帳戶將有權存取的子資料夾。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Google Cloud Storage]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google Cloud Storage connection",
      "description": "Connector for Google Cloud Storage",
      "auth": {
          "specName": "Basic Authentication for google-cloud",
          "params": {
              "accessKeyId": "accessKeyId",
              "secretAccessKey": "secretAccessKey",
              "bucketName": "acme-google-cloud-bucket",
              "folderPath": "/acme/customers/sales"
          }
      },
      "connectionSpec": {
          "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 與您的關聯的存取金鑰ID [!DNL Google Cloud Storage] 帳戶。 |
| `auth.params.secretAccessKey` | 與您的關聯的秘密存取金鑰 [!DNL Google Cloud Storage] 帳戶。 |
| `auth.params.bucketName` | 您的名稱 [!DNL Google Cloud Storage] 貯體。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，您必須指定貯體名稱。 |
| `auth.params.folderPath` | 您要提供存取權的資料夾路徑。 |
| `connectionSpec.id` | 此 [!DNL Google Cloud Storage] 連線規格ID： `32e8f412-cdf7-464c-9885-78184cb113fd` |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Google Cloud Storage] 使用API和唯一ID的連線已取得為回應本文的一部分。 您可以使用此連線ID來 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
