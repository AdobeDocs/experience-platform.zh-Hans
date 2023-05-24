---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 設定自助式來源的探索規格（批次SDK）
description: 本檔案提供使用Self-Serve Sources (Batch SDK)所需準備的設定概觀。
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---

# 設定自助式來源的探索規格（批次SDK）

瀏覽規格定義瀏覽和檢查來源中所包含物件所需的引數。 探索規格也會定義探索及檢查物件時傳回的回應格式。

>[!TIP]
>
>探索規格採用硬式編碼，您只需將下列裝載複製並貼到您的連線規格即可。

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| 探索規格 | 描述 | 示例 |
| --- | --- | --- |
| `name` | 定義瀏覽規格的名稱或識別碼。 | `Resource` |
| `type` | 定義瀏覽規格的型別。 | `Resource` |
| `requestSpec` | 包含探索連線中物件所需的引數。 |
| `requestSpec.type` | 定義要求規格的資料型別。 | `object` |
| `responseSpec` | 包含定義回應訊息（針對探索呼叫傳回）的格式的引數。 |
| `responseSpec.type` | 定義回應規格的資料型別。 | `object` |
| `responseSpec.properties` | 包含與回應訊息的格式相關之資訊。 |
| `responseSpec.properties.format` | 定義回應結構描述的格式。 | `object` |
| `responseSpec.properties.format.type` | 定義屬性的資料型別。 | `string` |
| `responseSpec.schema` | 包含有關回應結構描述格式化的資訊。 |
| `responseSpec.schema.type` | 定義結構描述的資料型別。 | `object` |
| `responseSpec.schema.properties` | 包含有關資料行、型別和結構描述中保留之專案的資訊。 |
| `responseSpec.schema.properties.columns.items.properties.name` | 顯示檔案的名稱。 |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 定義檔案名稱的資料型別。 | `string` |

{style="table-layout:auto"}

## 后续步骤

填入您的瀏覽規格後，您可以繼續使用 [!DNL Flow Service] API。 請參閱 [自助來源（批次SDK） API指南](../api/api-overview.md) 以取得詳細資訊。
