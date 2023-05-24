---
keywords: Experience Platform；首頁；熱門主題；流程服務；更新帳戶
solution: Experience Platform
title: 使用流程服務API更新帳戶
type: Tutorial
description: 本教學課程涵蓋使用Flow Service API更新帳戶詳細資訊和認證的步驟。
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# 使用流程服務API更新帳戶

在某些情況下，可能需要更新現有來源連線的詳細資料。 [!DNL Flow Service] 讓您能夠新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。

本教學課程涵蓋使用更新連線的詳細資訊和認證的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教學課程需要您具備現有的連線和有效的連線ID。 如果您沒有現有的連線，請從 [來源概觀](../../home.md) 並依照在嘗試本教學課程之前概述的步驟進行。

本教學課程也要求您實際瞭解Adobe Experience Platform的下列元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../landing/api-guide.md).

## 查詢連線詳細資料

更新連線的第一步是使用連線ID擷取其詳細資訊。 GET若要擷取您連線的目前詳細資料，請向 [!DNL Flow Service] 提供您要更新的連線的連線ID時使用的API。

**API格式**

```http
GET /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 唯一 `id` 您要擷取之連線的值。 |

**请求**

以下請求會擷取有關您連線的資訊。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回連線的目前詳細資料，包括其認證、唯一識別碼(`id`)，以及版本來識別。 更新您的連線需要版本值。

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## 更新連線

PATCH若要更新連線的名稱、說明和認證，請對 [!DNL Flow Service] API，並提供您的連線ID、版本以及您想要使用的新資訊。

>[!IMPORTANT]
>
>此 `If-Match` 發出PATCH請求時需要標頭。 此標頭的值是您要更新的連線唯一版本。

**API格式**

```http
PATCH /connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 唯一 `id` 您要更新的連線值。 |

**请求**

以下請求提供新名稱和說明，以及一組新憑證，用於更新您的連線。

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| 参数 | 描述 |
| --------- | ----------- |
| `op` | 用來定義更新連線所需動作的操作呼叫。 作業包括： `add`， `replace`、和 `remove`. |
| `path` | 要更新的引數路徑。 |
| `value` | 您想要用來更新引數的新值。 |

**响应**

成功的回應會傳回您的連線ID和更新的etag。 您可以向發出GET要求以驗證更新 [!DNL Flow Service] API，同時提供您的連線ID。

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 后续步骤

依照本教學課程，您已使用更新與連線相關聯的認證和資訊 [!DNL Flow Service] API。 如需使用來源聯結器的詳細資訊，請參閱 [來源概觀](../../home.md).
