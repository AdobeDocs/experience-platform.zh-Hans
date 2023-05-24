---
keywords: Experience Platform；首頁；熱門主題；servicenow；ServiceNow
solution: Experience Platform
title: 使用Flow Service API建立ServiceNow基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線到ServiceNow伺服器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 建立 [!DNL ServiceNow] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Google ServiceNow] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線至所需的其他資訊 [!DNL ServiceNow] 伺服器使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線到 [!DNL ServiceNow]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `endpoint` | 的端點 [!DNL ServiceNow] 伺服器。 |
| `username` | 用來連線至的使用者名稱 [!DNL ServiceNow] 用於驗證的伺服器。 |
| `password` | 連線至的密碼 [!DNL ServiceNow] 用於驗證的伺服器。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL ServiceNow] 為： `eb13cb25-47ab-407f-ba89-c0125281c563`. |

如需入門的詳細資訊，請參閱 [此ServiceNow檔案](https://developer.servicenow.com/app.do#!/rest_api_doc？v=new york&amp;id=r_TableAPI-GET).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL ServiceNow] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL ServiceNow]：

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.server` | 您的的端點 [!DNL ServiceNow] 伺服器。 |
| `auth.params.username` | 用來連線至的使用者名稱 [!DNL ServiceNow] 用於驗證的伺服器。 |
| `auth.params.password` | 連線至的密碼 [!DNL ServiceNow] 用於驗證的伺服器。 |
| `connectionSpec.id` | 此 [!DNL ServiceNow] 連線規格ID： `eb13cb25-47ab-407f-ba89-c0125281c563` |

**响应**

成功回應會傳回新建立的連線，包括其唯一識別碼(`id`)。 在下一個步驟中探索您的CRM系統時，需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL ServiceNow] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用將客戶成功資料帶入Platform [!DNL Flow Service] API](../../collect/customer-success.md)
