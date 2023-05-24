---
keywords: Experience Platform；首頁；熱門主題；Oracle物件儲存；oracle物件儲存
solution: Experience Platform
title: 使用Flow Service API建立Oracle物件儲存基礎連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線到Oracle物件儲存。
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# 建立 [!DNL Oracle Object Storage] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Oracle Object Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Oracle Object Storage] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線到 [!DNL Oracle Object Storage]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `serviceUrl` | 此 [!DNL Oracle Object Storage] 驗證所需的端點。 端點格式為： `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | 此 [!DNL Oracle Object Storage] 驗證所需的存取金鑰ID。 |
| `secretKey` | 此 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `bucketName` | 如果使用者擁有受限制的存取權，則需要允許的bucket名稱。 貯體名稱的長度必須介於3到63個字元之間，開頭和結尾必須是字母或數字，而且只能包含小寫字母、數字或連字型大小(`-`)。 儲存貯體名稱的格式不得類似於IP位址。 |
| `folderPath` | 如果使用者擁有受限存取權，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Oracle Object Storage] 為： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

如需如何取得這些值的詳細資訊，請參閱 [oracle物件儲存驗證指南](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Oracle Object Storage] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Oracle Object Storage]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.serviceUrl` | 此 [!DNL Oracle Object Storage] 驗證所需的端點。 |
| `auth.params.accessKey` | 此 [!DNL Oracle Object Storage] 驗證所需的存取金鑰ID。 |
| `auth.params.secretKey` | 此 [!DNL Oracle Object Storage] 驗證所需的密碼。 |
| `auth.params.bucketName` | 如果使用者擁有受限制的存取權，則需要允許的bucket名稱。 |
| `auth.params.folderPath` | 如果使用者擁有受限存取權，則需要允許的資料夾路徑。 |
| `connectionSpec.id` | 此 [!DNL Oracle Object Storage] 連線規格ID： `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**响应**

成功的回應會傳回新建立連線的連線ID。 在下一個教學課程中，探索您的雲端儲存空間資料時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Oracle Object Storage] 使用下列專案的連線： [!DNL Flow Service] API，並已取得其唯一的連線ID。 您可以使用此連線ID來 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
