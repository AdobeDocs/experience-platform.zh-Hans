---
title: 使用流量服務API建立串流SDK的新連線規格
description: 以下檔案提供如何使用「流程服務API」建立連線規格，以及透過「自助來源」整合新來源的步驟。
hide: true
hidefromtoc: true
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# 使用建立新的連線規格 [!DNL Flow Service] API

連線規格代表來源的結構。 它包含有關來源的驗證需求的資訊，定義如何探索和檢查來源資料，並提供有關給定來源屬性的資訊。 此 `/connectionSpecs` 中的端點 [!DNL Flow Service] API可讓您以程式設計方式管理組織內的連線規格。

以下檔案提供如何建立連線對規格的步驟。 [!DNL Flow Service] API並透過自助來源（串流SDK）整合新來源。

## 快速入门

在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 收整合品

若要使用自助式來源建立新的串流來源，您必須先協調Adobe、請求私人Git存放庫，並對齊有關來源標籤、說明、類別和圖示詳細資訊的Adobe。

提供後，您必須建構您的私人Git存放庫，如下所示：

* 源
   * {your_source}
      * 成品
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 成品（檔案名稱） | 描述 | 示例 |
| --- | --- | --- |
| {your_source} | 來源的名稱。 此資料夾應包含您的私人Git存放庫中與您的來源相關的所有成品。 | `medallia` |
| {your_source}-category.txt | 您的來源所屬的類別，格式為文字檔。 **注意**：如果您認為您的來源不符合上述任何類別，請聯絡您的Adobe代表以進行討論。 | `medallia-category.txt` 在檔案內，請指定來源的類別，例如： `streaming`. |
| {your_source}-description.txt | 來源的簡短說明。 | [!DNL Medallia] 是行銷自動化來源，可用來提供 [!DNL Medallia] 要Experience Platform的資料。 |
| {your_source}-icon.svg | 用來在Experience Platform來源目錄中表示來源的影像。 此圖示必須是SVG檔案。 |
| {your_source}-label.txt | 您應顯示在Experience Platform來源目錄中的來源名稱。 | 梅迪亞文 |
| {your_source}-connectionSpec.json | 包含您來源之連線規格的JSON檔案。 一開始不需要此檔案，因為當您完成本指南時，會填入您的連線規格。 | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>在連線規格的測試期間，您可以使用 `text` 在連線規格中。

將必要的檔案新增至私人Git存放庫後，您必須建立提取請求(PR)供Adobe檢閱。 您的PR獲得核准並合併後，將會為您提供一個ID，可用於您的連線規格，以參考來源的標籤、說明和圖示。

接下來，請依照下列步驟設定您的連線規格。 如需可新增至來源的不同功能（例如進階排程、自訂結構描述或不同分頁型別）的額外指引，請檢閱以下指南： [設定來源規格](../config/sourcespec.md).

## 複製連線規格範本

收集到所需的成品後，請將下方的連線規格範本複製並貼到您選擇的文字編輯器中，然後更新方括弧中的屬性 `{}` ，其中包含與您特定來源相關的資訊。

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## 建立連線規格 {#create}

取得連線規格範本後，您現在可以填入與來源對應的適當值，開始編寫新的連線規格。

連線規格可分成兩個不同的部分：來源規格和探索規格。

請參閱下列檔案，以取得有關連線規格各節的詳細資訊：

* [設定您的來源規格](../config/sourcespec.md)
* [設定您的瀏覽規格](../config/explorespec.md)

更新您的規格資訊後，您可以透過向以下發出POST請求來提交新的連線規格： `/connectionSpecs` 的端點 [!DNL Flow Service] API。

**API格式**

```http
POST /connectionSpecs
```

**请求**

以下請求是串流來源的完整編寫連線規格的範例：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**响应**

成功的回應會傳回新建立的連線規格，包括其唯一的 `id`.

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## 后续步骤

現在您已建立新的連線規格，您必須將其對應的連線規格ID新增至現有的流程規格。 請參閱教學課程，位置如下： [更新流程規格](./update-flow-specs.md) 以取得詳細資訊。

若要修改您建立的連線規格，請參閱以下教學課程： [更新連線規格](./update-connection-specs.md).
