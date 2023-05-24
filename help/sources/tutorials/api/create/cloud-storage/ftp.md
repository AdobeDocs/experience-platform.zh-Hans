---
keywords: Experience Platform；首頁；熱門主題；檔案傳輸通訊協定；檔案傳輸通訊協定
solution: Experience Platform
title: 使用流量服務API建立FTP基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至FTP （檔案傳輸通訊協定）伺服器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 建立FTP基本連線，使用 [!DNL Flow Service] API

>[!NOTE]
>
>FTP聯結器為Beta版。 功能和檔案可能會有所變更。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL FTP] （檔案傳輸通訊協定）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線至所需的其他資訊 [!DNL FTP] 伺服器使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線到 [!DNL FTP]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 與您的關聯的名稱或IP位址 [!DNL FTP] 伺服器。 |
| `username` | 您擁有存取許可權的使用者名稱 [!DNL FTP] 伺服器。 |
| `password` | 您的密碼 [!DNL FTP] 伺服器。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL FTP] 為： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL FTP] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL FTP]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.host` | FTP伺服器的主機名稱。 |
| `auth.params.username` | 與您的FTP伺服器相關聯的使用者名稱。 |
| `auth.params.password` | 與您的FTP伺服器關聯的密碼。 |
| `connectionSpec.id` | FTP伺服器連線規格ID： `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 在下一個教學課程中，探索您的FTP伺服器時，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 后续步骤

依照本教學課程，您已使用建立FTP連線： [!DNL Flow Service] API中，且已取得連線的唯一ID值。 您可以使用此連線ID來 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
