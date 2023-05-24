---
keywords: Experience Platform；首頁；熱門主題；購物；購物；電子商務
solution: Experience Platform
title: 使用Flow Service API建立Shopify聯結器基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Shopify連線至Adobe Experience Platform。
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 2%

---

# 建立 [!DNL Shopify] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Shopify] (以下稱&quot;[!DNL Shopify]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Sources]](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Shopify] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Shopify]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 您的專案的終點 [!DNL Shopify] 伺服器。 |
| `accessToken` | 您的存取權杖 [!DNL Shopify] 使用者帳戶。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Shopify] 為： `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

如需入門的詳細資訊，請參閱此 [Shopify驗證檔案](https://shopify.dev/concepts/about-apis/authentication).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Shopify] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Shopify]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的端點 [!DNL Shopify] 伺服器。 |
| `auth.params.accessToken` | 您的存取權杖 [!DNL Shopify] 使用者帳戶。 |
| `connectionSpec.id` | 此 [!DNL Shopify] 連線規格ID： `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**响应**

成功回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Shopify] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以使用將電子商務資料帶入Platform [!DNL Flow Service] API](../../collect/ecommerce.md)
