---
title: Reactor API中的关系
description: 了解如何在Reactor API中建立资源关系，包括每个资源的关系要求。
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 6%

---

# Reactor API中的关系

Reactor API中的资源通常相互关联。 本文档概述了如何在API中建立资源关系，以及每种资源类型的关系需求。

根据相关资源的类型，需要建立某些关系。 所需的关系意味着父资源不能没有关系而存在。 所有其他关系都是可选的。

无论关系是必需关系还是可选关系，系统都会在创建相关资源时自动建立关系，或者必须手动创建关系。 在手动创建关系的情况下，根据相关资源有两种可能的方法：

* [按有效负荷创建](#payload)
* [通过URL创建](#url)（仅适用于库）

请参阅有关[关系要求](#requirements)的部分，以获取每个资源类型的兼容关系列表，以及在适用的情况下建立这些关系所需的方法。

## 按有效负荷创建关系 {#payload}

最初创建资源时，必须手动建立某些关系。 要完成此操作，您必须在首次创建父资源时在请求有效负载中提供`relationship`对象。 这些关系的示例包括：

* [创建具有所需扩展的数据元素](../endpoints/data-elements.md#create)
* [创建具有所需主机关系的环境](../endpoints/environments.md#create)

**API格式**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 资源所属的属性的ID。 |
| `{RESOURCE_TYPE}` | 要创建的资源的类型。 |

{style="table-layout:auto"}

**请求**

以下请求创建新的`rule_component`，与`rules`和`extension`建立关系。

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
| `relationships` | 按有效负荷创建关系时必须提供的对象。 此对象中的每个键代表特定的关系类型。 在上例中，已建立`extension`和`rules`关系，这些关系特定于`rule_components`。 有关不同资源的兼容关系类型的详细信息，请参阅有关按资源[&#128279;](#relationship-requirements-by-resource)的关系要求的部分。 |
| `data` | 在`relationship`对象下提供的每个关系类型都必须包含一个`data`属性，该属性引用与关系建立的资源的`id`和`type`。 通过将`data`属性格式化为对象数组，使每个对象包含适用资源的`id`和`type`，您可以创建与相同类型的多个资源的关系。 |
| `id` | 资源的唯一ID 每个`id`都必须带有同级`type`属性，以指示相关资源的类型。 |
| `type` | 同级`id`字段引用的资源类型。 接受的值包括`data_elements`、`rules`、`extensions`和`environments`。 |

{style="table-layout:auto"}

## 通过URL创建关系 {#url}

与其他资源不同，库通过自己的专用`/relationship`端点建立关系。 示例包括：

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
| `{RESOURCE_TYPE}` | 关系所定位的资源类型。 可用值包括`environment`、`data_elements`、`extensions`和`rules`。 |

**请求**

以下请求使用库的`/relationships/environment`端点创建与环境的关系。

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
| `data` | 为关系引用目标资源的`id`和`type`的对象。 如果要创建与多个相同类型的资源（如`extensions`和`rules`）的关系，`data`属性必须格式化为对象数组，每个对象都包含适用资源的`id`和`type`。 |
| `id` | 资源的唯一ID 每个`id`都必须带有同级`type`属性，以指示相关资源的类型。 |
| `type` | 同级`id`字段引用的资源类型。 接受的值包括`data_elements`、`rules`、`extensions`和`environments`。 |

{style="table-layout:auto"}

## 按资源列出的关系要求 {#requirements}

下表概述了每种资源类型的可用关系（无论这些关系是否必需），以及在适用的情况下手动创建关系的接受方法。

>[!NOTE]
>
>如果关系未列为由有效负载或URL创建，则由系统自动分配。

### 审核事件

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ {\f13 } | | |
| `entity` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 内部版本

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `data_elements` | | | |
| `extensions` | | | |
| `rules` | | | |
| `environment` | ✓ {\f13 } | | |
| `library` | ✓ {\f13 } | | |
| `property` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 回调

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 公司

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `properties` | | | |

{style="table-layout:auto"}

### 数据元素

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ {\f13 } | | |
| `notes` | | | |
| `property` | ✓ {\f13 } | | |
| `origin` | ✓ {\f13 } | | |
| `extension` | ✓ {\f13 } | ✓ {\f13 } | |
| `updated_with_extension` | ✓ {\f13 } | | |
| `updated_with_extension_package` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 环境

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `library` | | | |
| `builds` | | | |
| `host` | ✓ {\f13 } | ✓ {\f13 } | |
| `property` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 扩展

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ {\f13 } | | |
| `notes` | | | |
| `property` | ✓ {\f13 } | | |
| `origin` | ✓ {\f13 } | | |
| `extension_package` | ✓ {\f13 } | ✓ {\f13 } | |
| `updated_with_extension_package` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 托管

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 库

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `builds` | | | |
| `environment` | | | ✓ {\f13 } |
| `data_elements` | | | ✓ {\f13 } |
| `extensions` | | | ✓ {\f13 } |
| `rules` | | | ✓ {\f13 } |
| `notes` | | | |
| `upstream_library` | ✓ {\f13 } | | |
| `property` | ✓ {\f13 } | | |
| `last_build` | | | |

{style="table-layout:auto"}

### 注释

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 属性

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ {\f13 } | | |
| `callbacks` | | | |
| `environments` | | | |
| `libraries` | | | |
| `data_elements` | | | |
| `extensions` | | | |
| `extensions` | | | |

{style="table-layout:auto"}

### 规则组件

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ {\f13 } | | |
| `updated_with_extension` | ✓ {\f13 } | | |
| `extension` | ✓ {\f13 } | ✓ {\f13 } | |
| `notes` | | | |
| `origin` | ✓ {\f13 } | | |
| `property` | ✓ {\f13 } | | |
| `rules` | ✓ {\f13 } | ✓ {\f13 } | |
| `revisions` | ✓ {\f13 } | | |

{style="table-layout:auto"}

### 规则

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ {\f13 } | | |
| `notes` | | | |
| `property` | ✓ {\f13 } | | |
| `origin` | ✓ {\f13 } | | |
| `rule_components` | | | |

### 密钥

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ {\f13 } | | ✓ {\f13 } |
| `environment` | ✓ {\f13 } | ✓ {\f13 } | |

