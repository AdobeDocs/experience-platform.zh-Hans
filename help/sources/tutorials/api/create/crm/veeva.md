---
keywords: Experience Platform；首頁；熱門主題；veeva crm；Veeva CRM；Veeva；
solution: Experience Platform
title: 使用流量服務API建立Veeva CRM基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Veeva CRM。
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---

# 建立 [!DNL Veeva CRM] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Veeva CRM] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Veeva CRM] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Veeva CRM]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | 您的URL [!DNL Veeva CRM] 執行個體。 |
| `username` | 您的使用者名稱值 [!DNL Veeva CRM] 帳戶。 |
| `password` | 您的的密碼值 [!DNL Veeva CRM] 帳戶。 |
| `securityToken` | 您的的安全性權杖 [!DNL Veeva CRM] 執行個體。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Veeva CRM] 為： `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

如需這些值的詳細資訊，請參閱此 [[!DNL Veeva CRM] 檔案](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Veeva CRM] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Veeva CRM]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --- | --- |
| `name` | 您的名稱 [!DNL Veeva CRM] 基礎連線。 您可以使用此名稱來查詢 [!DNL Veeva CRM] 基礎連線。 |
| `description` | 選用的說明 [!DNL Veeva CRM] 基礎連線。 |
| `auth.specName` | 用於連線的驗證型別。 |
| `auth.params.environmentUrl` | 您的URL [!DNL Veeva CRM] 執行個體。 |
| `auth.params.username` | 您的使用者名稱值 [!DNL Veeva CRM] 帳戶。 |
| `auth.params.password` | 您的的密碼值 [!DNL Veeva CRM] 帳戶。 |
| `auth.params.securityToken` | 您的的安全性權杖 [!DNL Veeva CRM] 執行個體。 |
| `connectionSpec.id` | 的連線規格ID [!DNL Veeva CRM]： `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

## 后续步骤

依照本教學課程，您已建立 [!DNL Veeva CRM] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以將CRM資料帶到Platform，使用 [!DNL Flow Service] API](../../collect/crm.md)
