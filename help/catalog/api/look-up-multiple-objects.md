---
keywords: Experience Platform；首頁；熱門主題；目錄；多物件查閱；API
solution: Experience Platform
title: 查詢多個目錄物件
description: 如果您想要檢視數個特定物件，而不是針對每個物件提出一項要求，Catalog會提供簡單的捷徑，讓您請求相同型別的多個物件。 您可以使用單一GET要求，包含以逗號分隔的ID清單來傳回多個特定物件。
exl-id: b2329b32-6139-4557-aff3-a584e03b09f3
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 1%

---

# 查詢多個目錄物件

如果您想要檢視數個特定物件，而不是針對每個物件提出一項要求， [!DNL Catalog] 為請求相同型別的多個物件提供簡單的捷徑。 您可以使用單一GET要求，包含以逗號分隔的ID清單來傳回多個特定物件。

>[!NOTE]
>
>即使請求特定 [!DNL Catalog] 物件，最佳做法仍是 `properties` 查詢引數以僅傳回您需要的屬性。

**API格式**

```http
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}
GET /{OBJECT_TYPE}/{ID_1},{ID_2},{ID_3},{ID_4}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要擷取的物件。 有效物件包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{ID}` | 您要擷取的特定物件之一的識別碼。 |

**请求**

以下請求包含以逗號分隔的資料集ID清單，以及要為每個資料集傳回的以逗號分隔的屬性清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5bde21511dd27b0000d24e95,5bda3a4228babc0000126377,5bceaa4c26c115000039b24b,5bb276b03a14440000971552,5ba9452f7de80400007fc52a?properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回指定資料集清單，其中僅包含要求的屬性(`name`， `description`、和 `files`)表示。

>[!NOTE]
>
>如果傳回的物件不包含下列專案所指示的一或多個要求屬性： `properties` 查詢時，回應只會傳回所請求的屬性，如所示 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 下方的。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```
