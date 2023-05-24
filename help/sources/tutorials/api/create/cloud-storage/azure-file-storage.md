---
keywords: Experience Platform；首頁；熱門主題；Azure；Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: 使用Flow Service API建立Azure檔案儲存庫連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Azure檔案儲存體連線到Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 建立 [!DNL Azure File Storage] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Azure File Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Azure File Storage]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 的端點 [!DNL Azure File Storag]您正在存取的執行個體。 |
| `userId` | 具有足夠存取許可權的使用者 [!DNL Azure File Storage] 端點。 |
| `password` | 您的密碼 [!DNL Azure File Storage] 例項 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Azure File Storage] 為： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

如需入門的詳細資訊，請參閱 [此Azure檔案儲存體檔案](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Azure File Storage] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Azure File Storage]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的端點 [!DNL Azure File Storage] 您正在存取的執行個體…… |
| `auth.params.userId` | 具有足夠存取許可權的使用者 [!DNL Azure File Storage] 端點。 |
| `auth.params.password` | 此 [!DNL Azure File Storage] 存取金鑰。 |
| `connectionSpec.id` | 此 [!DNL Azure File Storage] 連線規格ID： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Azure File Storage] 使用下列專案的連線： [!DNL Flow Service] API且已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何 [使用Flow Service API探索協力廠商雲端儲存空間](../../explore/cloud-storage.md).
