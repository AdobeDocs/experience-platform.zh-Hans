---
keywords: Experience Platform；首頁；熱門主題；Salesforce Service Cloud；Salesforce Service Cloud
solution: Experience Platform
title: 使用Flow Service API建立Salesforce Service雲端來源連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 建立 [!DNL Salesforce Service Cloud] 來源連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Salesforce Service Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Salesforce Service Cloud] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Salesforce Service Cloud]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `username` | 您的使用者名稱 [!DNL Salesforce Service Cloud] 使用者帳戶。 |
| `password` | 您的密碼 [!DNL Salesforce Service Cloud] 帳戶。 |
| `securityToken` | 您的的安全性權杖 [!DNL Salesforce Service Cloud] 帳戶。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Salesforce Service Cloud] 為： `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

如需入門的詳細資訊，請參閱 [此Salesforce Service Cloud檔案](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Salesforce Service Cloud] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Salesforce Service Cloud]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Salesforce Service Cloud] 帳戶。 |
| `auth.params.securityToken` | 與您的關聯的安全性權杖 [!DNL Salesforce Service Cloud] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Service Cloud] 連線規格ID： `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**响应**

成功回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Salesforce Service Cloud] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用將客戶成功資料帶入Platform [!DNL Flow Service] API](../../collect/customer-success.md)
