---
title: 在API中管理建议值
description: 了解如何将建议值添加到架构注册表API中的字符串字段。
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 在API中管理建议值

对于体验数据模型(XDM)中的任何字符串字段，您可以定义 **枚举** 该参数会限制字段可以摄取到预定义集合的值。 如果您尝试将数据摄取到枚举字段，并且该值与其配置中定义的任何值都不匹配，则将拒绝摄取。

与枚举相反，添加 **建议值** 字符串字段不会限制它可以摄取的值。 相反，建议值会影响中提供的预定义值 [分段UI](../../segmentation/ui/overview.md) 将字符串字段包含为属性时。

>[!NOTE]
>
>字段的更新建议值大约会延迟5分钟，以便反映在分段UI中。

本指南介绍如何使用管理建议值 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 有关如何在Adobe Experience Platform用户界面中执行此操作的步骤，请参阅 [有关枚举和建议值的UI指南](../ui/fields/enum.md).

## 先决条件

本指南假定您熟悉XDM中架构组合的元素以及如何使用架构注册表API创建和编辑XDM资源。 如果您需要获取简介，请参阅以下文档：

* [模式组合基础](../schema/composition.md)
* [架构注册表API指南](../api/overview.md)

此外，还强烈建议您查看 [枚举和建议值的演化规则](../ui/fields/enum.md#evolution) 如果您正在更新现有字段。 如果您正在管理参与合并的架构的建议值，请参阅 [合并枚举和建议值的规则](../ui/fields/enum.md#merging).

## 合成

在API中， **枚举** 字段由 `enum` 数组，而 `meta:enum` 对象为以下值提供友好的显示名称：

```json
"exampleStringField": {
  "type": "string",
  "enum": [
    "value1",
    "value2",
    "value3"
  ],
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

对于枚举字段，架构注册表不允许 `meta:enum` 将扩展到 `enum`，因为尝试在这些约束之外引入字符串值将不会通过验证。

或者，您可以定义一个不包含 `enum` 数组，并且仅使用 `meta:enum` 要表示的对象 **建议值**：

```json
"exampleStringField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

由于该字符串没有 `enum` 数组，用于定义约束 `meta:enum` 属性可以扩展以包含新值。

<!-- ## Manage suggested values for standard fields

For existing standard fields, you can [add suggested values](#add-suggested-standard) or [remove suggested values](#remove-suggested-standard). -->

## 将建议值添加到标准字段 {#add-suggested-standard}

要扩展 `meta:enum` 对于标准字符串字段，您可以创建 [友好名称描述符](../api/descriptors.md#friendly-name) 用于特定架构中相关字段。

>[!NOTE]
>
>字符串字段的建议值只能在架构级别添加。 换句话说，扩展 `meta:enum` 一个架构中某个标准字段的设置不会影响使用同一标准字段的其他架构。

以下请求将建议值添加到标准 `eventType` 字段(由 [XDM ExperienceEvent类](../classes/experienceevent.md))下ID为的架构 `sourceSchema`：

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "sourceProperty": "/eventType",
        "title": {
            "en_us": "Enum Event Type"
        },
        "description": {
            "en_us": "Event type field with soft enum values"
        },
        "meta:enum": {
          "eventA": {
            "en_us": "Event Type A"
          },
          "eventB": {
            "en_us": "Event Type B"
          }
        }
      }'
```

应用描述符后，架构注册表在检索架构时使用以下内容进行响应（响应因空间而被截断）：

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "eventType": {
      "type":"string",
      "title": "Enum Event Type",
      "description": "Event type field with soft enum values.",
      "meta:enum": {
        "customEventA": "Custom Event Type A",
        "customEventB": "Custom Event Type B"
      }
    }
  }
}
```

>[!NOTE]
>
>如果标准字段已包含下列值 `meta:enum`时，描述符中的新值不会覆盖现有字段，而是添加到上：
>
>
```json
>"standardField": {
>   "type":"string",
>   "title": "Example standard enum field",
>   "description": "Standard field with existing enum values.",
>   "meta:enum": {
>       "standardEventA": "Standard Event Type A",
>       "standardEventB": "Standard Event Type B",
>       "customEventA": "Custom Event Type A",
>       "customEventB": "Custom Event Type B"
>   }
>}
>```

<!-- ### Remove suggested values {#remove-suggested-standard}

If a standard string field has predefined suggested values, you can remove any values that you do not wish to see in segmentation. This is done through by creating a [friendly name descriptor](../api/descriptors.md#friendly-name) for the schema that includes an `xdm:excludeMetaEnum` property.

**API format**

```http
POST /tenant/descriptors
```

**Request**

The following request removes the suggested values "[!DNL Web Form Filled Out]" and "[!DNL Media ping]" for `eventType` in a schema based on the [XDM ExperienceEvent class](../classes/experienceevent.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:alternateDisplayInfo",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/xdm:eventType",
        "xdm:excludeMetaEnum": {
          "web.formFilledOut": "Web Form Filled Out",
          "media.ping": "Media ping"
        }
      }'
```

| Property | Description |
| --- | --- |
| `@type` | The type of descriptor being defined. For a friendly name descriptor, this value must be set to `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | The `$id` URI of the schema where the descriptor is being defined. |
| `xdm:sourceVersion` | The major version of the source schema. |
| `xdm:sourceProperty` | The path to the specific property whose suggested values you want to manage. The path should begin with a slash (`/`) and not end with one. Do not include `properties` in the path (for example, use `/personalEmail/address` instead of `/properties/personalEmail/properties/address`). |
| `meta:excludeMetaEnum` | An object that describes the suggested values that should be excluded for the field in segmentation. The key and value for each entry must match those included in the original `meta:enum` of the field in order for the entry to be excluded.  |

{style="table-layout:auto"}

**Response**

A successful response returns HTTP status 201 (Created) and the details of the newly created descriptor. The suggested values included under `xdm:excludeMetaEnum` will now be hidden from the Segmentation UI.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out"
  },
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
``` -->

## 管理自定义字段的建议值 {#suggested-custom}

要管理 `meta:enum` 对于自定义字段，您可以通过PATCH请求更新该字段的父类、字段组或数据类型。

>[!WARNING]
>
>与标准字段相反，它将 `meta:enum` 影响使用该字段的所有其他架构。 如果不希望更改在架构之间传播，请考虑改为创建新的自定义资源：
>
>* [创建自定义类](../api/classes.md#create)
>* [创建自定义字段组](../api/field-groups.md#create)
>* [创建自定义数据类型](../api/data-types.md#create)


以下请求将更新 `meta:enum` 由自定义数据类型提供的“忠诚度级别”字段的读者群：

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "replace",
          "path": "/loyaltyLevel/meta:enum",
          "value": {
            "ultra-platinum": "Ultra Platinum",
            "platinum": "Platinum",
            "gold": "Gold",
            "silver": "Silver",
            "bronze": "Bronze"
          }
        }
      ]'
```

应用更改后，架构注册表在检索架构时使用以下内容进行响应（响应因空间而被截断）：

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "title": "Example Schema",
  "properties": {
    "loyaltyLevel": {
      "type":"string",
      "title": "Loyalty Level",
      "description": "The loyalty program tier that this customer qualifies for.",
      "meta:enum": {
        "ultra-platinum": "Ultra Platinum",
        "platinum": "Platinum",
        "gold": "Gold",
        "silver": "Silver",
        "bronze": "Bronze"
      }
    }
  }
}
```

## 后续步骤

本指南介绍了如何管理架构注册表API中字符串字段的建议值。 请参阅指南，网址为 [在API中定义自定义字段](./custom-fields-api.md) 有关如何创建不同字段类型的更多信息。
