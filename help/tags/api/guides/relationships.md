---
title: Reactor API中的关系
description: 了解如何在Reactor API中建立资源关系，包括每个资源的关系要求。
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 6%

---

# Reactor API中的关系

Reactor API中的资源通常相互关联。 本文档概述了如何在API中建立资源关系，以及每种资源类型的关系要求。

根据相关资源的类型，需要建立一些关系。 所需的关系意味着父资源不能没有关系而存在。 所有其他关系都是可选的。

无论关系是必需关系还是可选关系，系统都会在创建相关资源时自动建立关系，或者必须手动创建关系。 在手动创建关系的情况下，根据相关资源有两种可能的方法：

* [按有效负荷创建](#payload)
* [按URL创建](#url) （仅适用于库）

请参阅以下部分： [关系要求](#requirements) 以获取每个资源类型的兼容关系列表，以及在适用的情况下建立这些关系所需的方法。

## 按有效负荷创建关系 {#payload}

最初创建资源时，必须手动建立某些关系。 要完成此操作，您必须提供 `relationship` 请求有效负载中的对象。 这些关系的示例包括：

* [创建数据元素](../endpoints/data-elements.md#create) 具有所需的扩展
* [创建环境](../endpoints/environments.md#create) 具有所需的主机关系

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

以下请求创建一个新的 `rule_component`，建立关系 `rules` 和 `extension`.

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
| `relationships` | 按有效负荷创建关系时必须提供的对象。 此对象中的每个键代表特定的关系类型。 在上例中， `extension` 和 `rules` 建立关系，这些关系专门 `rule_components`. 有关不同资源的兼容关系类型的更多信息，请参阅 [按资源列出的关系需求](#relationship-requirements-by-resource). |
| `data` | 以下提供的每个关系类型： `relationship` 对象必须包含 `data` 属性，该属性引用 `id` 和 `type` 正在与其建立关系的资源的。 您可以通过格式化 `data` 属性作为对象的数组，每个对象包含 `id` 和 `type` 适用的资源的ID。 |
| `id` | 资源的唯一ID 每个 `id` 必须随同兄弟姐妹 `type` 属性，指示相关资源的类型。 |
| `type` | 同级资源引用的资源类型 `id` 字段。 接受的值包括 `data_elements`， `rules`， `extensions`、和 `environments`. |

{style="table-layout:auto"}

## 通过URL创建关系 {#url}

与其他资源不同，图书馆通过自己的专属资源建立关系 `/relationship` 端点。 示例包括：

* [将扩展、数据元素和规则添加到库](../endpoints/libraries.md#add-resources)
* [将库分配给环境](../endpoints/libraries.md#environment)

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 参数 | 描述 |
| --- | --- |
| `{PROPERTY_ID}` | 库所属的属性的ID。 |
| `{LIBRARY_ID}` | 要为其创建关系的库的ID。 |
| `{RESOURCE_TYPE}` | 关系所定位的资源类型。 可用值包括 `environment`， `data_elements`， `extensions`、和 `rules`. |

**请求**

以下请求使用 `/relationships/environment` 用于创建与环境关系的库的端点。

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
| `data` | 引用 `id` 和 `type` 关系的目标资源的ID。 如果要创建与多个同类型资源的关系(例如 `extensions` 和 `rules`)，则 `data` 属性必须格式化为对象的数组，每个对象包含 `id` 和 `type` 适用的资源的ID。 |
| `id` | 资源的唯一ID 每个 `id` 必须随同兄弟姐妹 `type` 属性，指示相关资源的类型。 |
| `type` | 同级资源引用的资源类型 `id` 字段。 接受的值包括 `data_elements`， `rules`， `extensions`、和 `environments`. |

{style="table-layout:auto"}

## 按资源列出的关系要求 {#requirements}

下表概述了每种资源类型的可用关系（无论这些关系是否必需），以及在适用的情况下手动创建关系的接受方法。

>[!NOTE]
>
>如果关系未列为由有效负载或URL创建，则由系统自动分配。

### 审核事件

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ “ ”标签 |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### 内部版本

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 回调

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 公司

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### 数据元素

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
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

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 扩展

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
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

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 库

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
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

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### 属性

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
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

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
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

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### 密钥

| 关系 | 必需 | 按有效负荷创建 | 按URL创建 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

