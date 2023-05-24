---
title: 搜尋端點
description: 瞭解如何在Reactor API中呼叫/search端點。
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 1%

---

# 搜尋端點

此 `/search` Reactor API中的端點提供尋找符合所需條件的資源的方法，以查詢表示。

下列API資源型別可供搜尋，其資料結構與透過API傳回的資源型檔案相同：

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

所有查詢的範圍皆為您目前的公司和可存取的屬性。

>[!IMPORTANT]
>
>搜尋功能具有下列注意事項和例外：
>* 中繼無法搜尋，且未在搜尋結果中傳回。
>* 擴充功能套件委派的結構描述欄位（動作、條件等） 可當作文字搜尋，而非巢狀資料結構搜尋。
>* 範圍查詢目前僅支援整數。


如需如何使用此功能的詳細資訊，請參閱 [搜尋指南](../guides/search.md).

## 快速入门

本指南中使用的端點是 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 有關如何向API驗證的重要資訊。

## 執行搜尋 {#perform}

您可以發出POST要求來執行搜尋。

**API格式**

```http
POST /search
```

**请求**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `from` | 要位移回應的結果數目。 |
| `size` | 要傳回的結果數量上限。 結果不能超過100個專案。 |
| `query` | 代表搜尋查詢的物件。 對於此物件中的每個屬性，索引鍵必須代表查詢依據的欄位路徑，而且值必須是其子屬性決定要查詢什麼的物件。<br><br>對於每個欄位路徑，您可以使用以下子屬性：<ul><li>`exists`：如果資源中存在欄位，則傳回true。</li><li>`value`：如果欄位的值符合此屬性的值，則傳回true。</li><li>`value_operator`：布林值邏輯，用於判斷 `value` 應處理查詢。 允許值為 `AND` 和 `OR`. 排除時， `AND` 會假設邏輯。 請參閱以下小節： [值運運算元邏輯](#value-operator) 以取得詳細資訊。</li><li>`range` 如果欄位的值落在特定的數字範圍內，則傳回true。 範圍本身由以下子屬性決定：<ul><li>`gt`：大於提供的值（非包含）。</li><li>`gte`：大於或等於提供的值。</li><li>`lt`：小於提供的值，不含。</li><li>`lte`：小於或等於提供的值。</li></ul></li></ul> |
| `sort` | 一個物件陣列，指示排序結果的順序。 每個物件都必須包含單一屬性：索引鍵代表排序依據的欄位路徑，值代表排序順序(`asc` 若為升序， `desc` （遞減）。 |
| `resource_types` | 字串陣列，指出要搜尋的特定資源型別。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回查詢的相符資源清單。 如需API如何判斷符合特定值的詳細資訊，請參閱 [比對慣例](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## 附录

下節包含有關使用的其他資訊 `/search` 端點。

### 值運運算元邏輯 {#value-operator}

搜尋查詢值會分割成字詞，以比對已編制索引的檔案。 在每個字詞之間， `AND` 會假設為關聯性。

使用時 `AND` 作為 `value_operator`，的查詢值 `My Rule Holiday Sale` 會解譯為包含下列欄位的檔案： `My AND Rule AND Holiday AND Sale`.

使用時 `OR` 作為 `value_operator`，的查詢值 `My Rule Holiday Sale` 會解譯為包含下列欄位的檔案： `My OR Rule OR Holiday OR Sale`. 相符的字詞越多，字詞越多 `match_score`. 由於部分字詞比對的性質，當沒有任何字元與所需值幾乎相符時，您可以取得只符合非常基本層級的值（例如幾個文字字元）的結果集。

### 比對慣例 {#conventions}

搜尋著重於回答檔案與所提供查詢的相關程度。 檔案資料的分析和索引方式會直接影響這一點。

下表劃分常見欄位型別的比對慣例：

| 欄位型別 | 比對慣例 |
| --- | --- |
| 字符串 | 含有部分詞語分析的文字，不區分大小寫 |
| 列舉值 | 完全相符，區分大小寫 |
| 整數 | 完全相符 |
| 浮動 | 完全相符 |
| 時間戳記 | 完全相符（日期時間格式） |
| 顯示名稱 | 含有部分詞語分析的文字，不區分大小寫 |

API中出現的特定欄位還有其他慣例：

| 字段 | 比對慣例 |
| --- | --- |
| `id` | 完全相符，區分大小寫 |
| `delegate_descriptor_id` | 完全相符、區分大小寫、字詞分割於 `::` |
| `name` | 完全相符，區分大小寫 |
| `settings` | 含有部分詞語分析的文字，不區分大小寫 |
| `type` | 完全相符，區分大小寫 |
