---
keywords: Experience Platform；首頁；熱門主題；電子商務；電子商務
solution: Experience Platform
title: 使用Flow Service API探索電子商務連線
description: 本教學課程使用流量服務API來探索電子商務連線。
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# 探索電子商務連線，使用 [!DNL Flow Service] API

[!DNL Flow Service] 用於收集及集中Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供可連線所有支援來源的使用者介面和RESTful API。

本教學課程使用 [!DNL Flow Service] 用於探索第三方的API **[!UICONTROL 電子商務]** 連線。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Sources]](../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線至所需的其他資訊 **[!UICONTROL 電子商務]** 使用下列專案的連線： [!DNL Flow Service] API。

### 取得連線ID

為了探索您的 **[!UICONTROL 電子商務]** 連線使用 [!DNL Platform] API，您必須擁有有效的連線ID。 如果您還沒有的連線， **[!UICONTROL 電子商務]** 您可在下列教學課程中建立您想要使用的連線：

* [Shopify](../create/ecommerce/shopify.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Flow Service]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 探索您的資料表格

使用您的 **[!UICONTROL 電子商務]** 連線ID，您可以執行GET請求來探索資料表。 使用以下呼叫來尋找您要檢查或擷取的表格路徑 [!DNL Platform].

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{CONNECTION_ID}` | 您的 **[!UICONTROL 電子商務]** 連線ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會從傳回一連串表格， **[!UICONTROL 電子商務]** 連線。 尋找您要加入的表格 [!DNL Platform] 並記下其 `path` 屬性，因為您必須在下一個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表格的結構

若要檢查表格結構，請執行下列步驟： **[!UICONTROL 電子商務]** 連線，在指定表格路徑時執行GET要求 `object` 查詢引數。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您的的連線ID **[!UICONTROL 電子商務]** 連線。 |
| `{TABLE_PATH}` | 您內表格的路徑 **[!UICONTROL 電子商務]** 連線。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回指定資料表的結構。 有關每個表格欄的詳細資訊位於 `columns` 陣列。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## 后续步骤

依照本教學課程，您已探索 **[!UICONTROL 電子商務]** connection，找到您要擷取的表格路徑 [!DNL Platform]，並取得有關其結構的資訊。 您可以在下一個教學課程中使用此資訊來 [收集電子商務資料並將其帶入Platform](../collect/ecommerce.md).
