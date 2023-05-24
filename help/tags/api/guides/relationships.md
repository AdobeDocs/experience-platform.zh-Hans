---
title: Reactor API中的關係
description: 瞭解如何在Reactor API中建立資源關係，包括每個資源的關係需求。
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 6%

---

# Reactor API中的關係

Reactor API中的資源通常彼此相關。 本檔案概述如何在API中建立資源關係，以及每種資源型別的關係需求。

根據相關資源的型別，需要一些關係。 必要的關聯性表示父資源不能沒有關聯性存在。 所有其他關係都是選擇性的。

無論關聯性是必要還是選擇性的，系統都會在建立相關資源時自動建立，或者必須手動建立。 在手動建立關係的情況下，根據相關資源有兩種可能的方法：

* [依裝載建立](#payload)
* [依URL建立](#url) （僅適用於程式庫）

請參閱以下章節： [關係需求](#requirements) 取得每個資源型別的相容關係清單，以及建立這些關係所需的方法（如適用）。

## 依裝載建立關係 {#payload}

最初建立資源時，必須手動建立某些關係。 若要完成此作業，您必須提供 `relationship` 物件。 這些關係的範例包括：

* [建立資料元素](../endpoints/data-elements.md#create) 含必要的副檔名
* [建立環境](../endpoints/environments.md#create) 具有必要的主機關係

**API格式**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 資源所屬屬性的ID。 |
| `{RESOURCE_TYPE}` | 要建立的資源型別。 |

{style="table-layout:auto"}

**请求**

以下請求會建立新的 `rule_component`，建立關係 `rules` 和 `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `relationships` | 依裝載建立關係時必須提供的物件。 此物件中的每個索引鍵都代表特定的關聯性型別。 在上述範例中， `extension` 和 `rules` 建立關係，這些關係專門 `rule_components`. 如需不同資源的相容關係型別的詳細資訊，請參閱以下章節： [依資源的關係需求](#relationship-requirements-by-resource). |
| `data` | 以下提供的每個關係型別 `relationship` 物件必須包含 `data` 屬性，會參照 `id` 和 `type` 正在與其建立關係的資源。 您可以透過格式化 `data` 屬性做為物件的陣列，每個物件都包含 `id` 和 `type` 適用的資源。 |
| `id` | 資源的唯一識別碼。 每個 `id` 必須搭配同層級 `type` 屬性，指出相關資源的型別。 |
| `type` | 同層級參照的資源型別 `id` 欄位。 接受的值包括 `data_elements`， `rules`， `extensions`、和 `environments`. |

{style="table-layout:auto"}

## 依URL建立關係 {#url}

與其他資源不同，程式庫會透過自己的專屬資源建立關係 `/relationship` 端點。 示例包括：

* [將擴充功能、資料元素和規則新增至程式庫](../endpoints/libraries.md#add-resources)
* [將程式庫指派給環境](../endpoints/libraries.md#environment)

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 程式庫所屬屬性的ID。 |
| `{LIBRARY_ID}` | 您要為其建立關係的資料庫ID。 |
| `{RESOURCE_TYPE}` | 關係所定位的資源型別。 可用的值包括 `environment`， `data_elements`， `extensions`、和 `rules`. |

**请求**

以下請求使用 `/relationships/environment` 用於建立與環境關係的程式庫的端點。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `data` | 參照「 」的物件 `id` 和 `type` 關聯的目標資源。 如果您要建立與相同型別的多個資源的關係(例如 `extensions` 和 `rules`)， `data` 屬性必須格式化為物件陣列，且每個物件包含 `id` 和 `type` 適用的資源。 |
| `id` | 資源的唯一識別碼。 每個 `id` 必須搭配同層級 `type` 屬性，指出相關資源的型別。 |
| `type` | 同層級參照的資源型別 `id` 欄位。 接受的值包括 `data_elements`， `rules`， `extensions`、和 `environments`. |

{style="table-layout:auto"}

## 依資源的關係需求 {#requirements}

下表概述每種資源型別的可用關係（無論這些關係是否必要），以及手動建立關係的可接受方法（如適用）。

>[!NOTE]
>
>如果關係未列為由承載或URL建立，則由系統自動指派。

### 稽核事件

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ (N) |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### 内部版本

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 回呼

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 公司

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### 数据元素

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### 环境

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 扩展

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### 托管

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 库

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style="table-layout:auto"}

### 注释

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### 属性

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### 规则组件

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### 规则

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### 秘密

| 关系 | 必需 | 依裝載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

