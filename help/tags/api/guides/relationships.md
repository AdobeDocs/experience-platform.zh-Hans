---
title: Reactor API中的关系
description: 了解如何在Reactor API中建立资源关系，包括每个资源的关系要求。
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 10%

---

# Reactor API中的关系

Reactor API中的资源通常彼此相关。 本文档概述了如何在API中建立资源关系，以及每种资源类型的关系要求。

根据相关资源类型，需要一些关系。 必需的关系意味着没有关系父资源不能存在。 所有其他关系都是可选的。

无论是必需关系还是可选关系，在创建相关资源时，系统都会自动建立关系，或者必须手动创建关系。 在手动创建关系时，根据相关资源，可以使用两种方法：

* [按负载创建](#payload)
* [按URL创建](#url) （仅限库）

请参阅 [关系要求](#requirements) 以获取每种资源类型的兼容关系列表，以及在适用时建立这些关系所需的方法。

## 按负载创建关系 {#payload}

在最初创建资源时，必须手动建立某些关系。 要实现此目的，您必须提供 `relationship` 对象。 这些关系的示例包括：

* [创建数据元素](../endpoints/data-elements.md#create) 和所需的扩展
* [创建环境](../endpoints/environments.md#create) 与所需的主机关系

**API格式**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 资源所属的属性的ID。 |
| `{RESOURCE_TYPE}` | 要创建的资源类型。 |

{style=&quot;table-layout:auto&quot;}

**请求**

以下请求会创建新 `rule_component`，与 `rules` 和 `extension`.

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
| `relationships` | 按有效负载创建关系时必须提供的对象。 此对象中的每个键都表示特定的关系类型。 在上述示例中， `extension` 和 `rules` 建立关系，其中 `rule_components`. 有关不同资源的兼容关系类型的更多信息，请参阅 [按资源划分的关系需求](#relationship-requirements-by-resource). |
| `data` | 在 `relationship` 对象必须包含 `data` 属性，引用 `id` 和 `type` 与之建立关系的资源。 您可以通过格式设置 `data` 属性作为对象数组，其中每个对象都包含 `id` 和 `type` 资源。 |
| `id` | 资源的唯一ID。 每个 `id` 必须和兄弟姐妹一起 `type` 属性，指示相关资源的类型。 |
| `type` | 同级引用的资源类型 `id` 字段。 接受的值包括 `data_elements`, `rules`, `extensions`和 `environments`. |

{style=&quot;table-layout:auto&quot;}

## 通过URL创建关系 {#url}

与其他资源不同，图书馆通过自己的专门工作建立关系 `/relationship` 端点。 示例包括：

* [将扩展、数据元素和规则添加到库](../endpoints/libraries.md#add-resources)
* [将库分配到环境](../endpoints/libraries.md#environment)

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 库所属的属性的ID。 |
| `{LIBRARY_ID}` | 要为其创建关系的库的ID。 |
| `{RESOURCE_TYPE}` | 关系所定向的资源类型。 可用值包括 `environment`, `data_elements`, `extensions`和 `rules`. |

**请求**

以下请求使用 `/relationships/environment` 用于库创建与环境关系的端点。

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
| `data` | 引用 `id` 和 `type` 关系的目标资源。 如果您创建的关系涉及多个同一类型的资源(例如 `extensions` 和 `rules`)、 `data` 属性必须格式化为对象数组，每个对象都包含 `id` 和 `type` 资源。 |
| `id` | 资源的唯一ID。 每个 `id` 必须和兄弟姐妹一起 `type` 属性，指示相关资源的类型。 |
| `type` | 同级引用的资源类型 `id` 字段。 接受的值包括 `data_elements`, `rules`, `extensions`和 `environments`. |

{style=&quot;table-layout:auto&quot;}

## 按资源开列的关系要求 {#requirements}

下表概述了每种资源类型的可用关系（无论是否需要这些关系），以及在适用时手动创建关系的已接受方法。

>[!NOTE]
>
>如果某个关系未列为由有效负载或URL创建，则系统会自动为其分配该关系。

### 审核事件

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 内部版本

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 回调

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 公司

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 数据元素

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 环境

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 扩展

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 托管

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 库

| 关系 | 必需 | 按负载创建 | 按URL创建 |
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

{style=&quot;table-layout:auto&quot;}

### 注释

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 属性

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 规则组件

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 规则

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### 秘密

| 关系 | 必需 | 按负载创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

