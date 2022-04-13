---
title: 向字段添加建议的值
description: 了解如何向架构注册API的字符串字段添加建议的值。
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: 4ce9e53ec420a8c9ba07cdfd75e66d854989f8d2
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 向字段添加建议的值

在体验数据模型(XDM)中，枚举字段表示一个字符串字段，该字段受限于预定义的值子集。 枚举字段可提供验证以确保摄取的数据符合一组已接受的值。 但是，您还可以为字符串字段定义一组建议的值，而不强制将它们作为约束。

在 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)，枚举字段的约束值由 `enum` 数组，而 `meta:enum` 对象为这些值提供了友好显示名称：

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

对于枚举字段，架构注册表不允许 `meta:enum` 扩展到 `enum`，因为尝试摄取超出这些约束范围的字符串值将不会通过验证。

或者，您也可以定义一个不包含 `enum` 数组，且仅使用 `meta:enum` 表示建议值的对象：

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

由于字符串没有 `enum` 数组定义约束，其 `meta:enum` 可以扩展属性以包含新值。 本教程介绍如何向架构注册API中的标准字符串字段和自定义字符串字段添加建议的值。

## 先决条件

本指南假定您熟悉XDM中架构组合的元素，以及如何使用架构注册表API创建和编辑XDM资源。 如果您需要介绍，请参阅以下文档：

* [架构组合的基础知识](../schema/composition.md)
* [架构注册API指南](../api/overview.md)

## 向标准字段添加建议的值

扩展 `meta:enum` 标准字符串字段的 [友好名称描述符](../api/descriptors.md#friendly-name) ，用于特定模式中的相关字段。

>[!NOTE]
>
>只能在架构级别添加字符串字段的建议值。 换句话说，将 `meta:enum` 一个架构中的标准字段不会影响使用相同标准字段的其他架构。

以下请求会将建议的值添加到标准 `eventType` 字段(由 [XDM ExperienceEvent类](../classes/experienceevent.md)) `sourceSchema`:

```curl
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

应用描述符后，架构注册表在检索架构时响应以下内容（响应因空间而被截断）：

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
>如果标准字段已包含 `meta:enum`，则描述符中的新值不会覆盖现有字段，而是会添加在中：
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

## 向自定义字段添加建议的值

扩展 `meta:enum` 在自定义字段中，您可以通过PATCH请求更新字段的父类、字段组或数据类型。

>[!WARNING]
>
>与标准字段相反， `meta:enum` 自定义字段的会影响使用该字段的所有其他架构。 如果您不希望更改跨架构传播，请考虑改为创建新的自定义资源：
>
>* [创建自定义类](../api/classes.md#create)
>* [创建自定义字段组](../api/field-groups.md#create)
>* [创建自定义数据类型](../api/data-types.md#create)


以下请求更新了 `meta:enum` 自定义数据类型提供的“忠诚度级别”字段的值：

```curl
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

应用更改后，架构注册表在检索架构时会响应以下内容（响应因空间而被截断）：

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

本指南介绍了如何向架构注册API中的字符串字段添加建议的值。 请参阅 [在API中定义自定义字段](./custom-fields-api.md) 以了解有关如何创建不同字段类型的详细信息。
