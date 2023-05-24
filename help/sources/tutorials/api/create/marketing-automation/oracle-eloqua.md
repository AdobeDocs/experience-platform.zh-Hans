---
title: 使用流程服務API建立OracleEloqua基本連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線到Oracle Eloqua。
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 建立 [!DNL Oracle Eloqua] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Oracle Eloqua] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)：Platform可從各種來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)：Platform提供將單一沙箱分割的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Oracle Eloqua] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Oracle Eloqua]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| --- | --- |
| `endpoint` | 您的的端點 [!DNL Oracle Eloqua]. |
| `username` | 您的使用者名稱 [!DNL Oracle Eloqua] 帳戶。 使用者名稱的格式必須是 `siteName + \\ + username`，其中 `siteName` 是您用來登入的公司名稱 [!DNL Oracle Eloqua] 和 `username` 是您的使用者名稱。 例如，您的登入使用者名稱可以是： `adobe\\emily`. |
| `password` | 與您的對應的密碼 [!DNL Oracle Eloqua] 使用者名稱。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID值 [!DNL Oracle Eloqua] 來源固定為： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

如需下列專案的驗證認證詳細資訊： [!DNL Oracle Eloqua]，請參閱 [[!DNL Oracle Eloqua] 驗證指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Oracle Eloqua] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Oracle Eloqua]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 您的名稱 [!DNL Oracle Eloqua] 基礎連線。 建議您提供描述性名稱，因為您可以使用此值來查詢基礎連線。 |
| `description` | （選擇性）您可以納入的屬性，以提供基礎連線的補充資訊。 |
| `auth.specName` | 用於連線的驗證型別。 |
| `auth.params.endpoint` | 您的的端點 [!DNL Oracle Eloqua] 伺服器。 |
| `auth.params.username` | 包含網站名稱及使用者名稱（與您的網站相對應）的串連認證 [!DNL Oracle Eloqua] 帳戶。 |
| `auth.params.password` | 與您的對應之密碼 [!DNL Oracle Eloqua] 帳戶。 |
| `connectionSpec.id` | 的連線規格ID值 [!DNL Oracle Eloqua] 來源固定為： `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Oracle Eloqua] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以使用將行銷自動化資料帶入Platform [!DNL Flow Service] API](../../collect/marketing-automation.md)
