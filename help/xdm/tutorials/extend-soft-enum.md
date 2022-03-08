---
title: 扩展软枚举字段
description: 了解如何扩展模式注册表API中的软枚举字段。
exl-id: 96897a5d-e00a-410f-a20e-f77e223bd8c4
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 扩展软枚举字段

在体验数据模型(XDM)中，枚举字段表示一个字符串字段，该字段受限于预定义的值子集。 枚举字段可以提供验证以确保摄取的数据符合一组可接受的值（称为“硬枚举”），或者它们只能表示一组建议的值而不实施约束（称为“软枚举”）。

在架构注册表API中，硬枚举的受约束值由 `enum` 数组，而 `meta:enum` 对象为这些值提供了友好显示名称：

```json
"sampleHardEnumField": {
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

对于硬枚举字段，架构注册表不允许 `meta:enum` 扩展到 `enum`，因为尝试摄取超出这些约束范围的字符串值将不会通过验证。

相反，软枚举字段不包含 `enum` 数组，且仅使用 `meta:enum` 表示建议值的对象：

```json
"sampleSoftEnumField": {
  "type": "string",
  "meta:enum": {
    "value1": "Value 1",
    "value2": "Value 2",
    "value3": "Value 3"
  },
  "default": "value1"
}
```

由于软枚举与硬枚举没有相同的验证约束，因此其 `meta:enum` 可以扩展属性以包含新值。 本教程介绍如何扩展架构注册API中的标准和自定义软枚举字段。

## 先决条件

本指南假定您熟悉XDM中架构组合的元素，以及如何使用架构注册表API创建和编辑XDM资源。 如果您需要介绍，请参阅以下文档：

* [架构组合的基础知识](../schema/composition.md)
* [架构注册API指南](../api/overview.md)

## 扩展标准软枚举字段

扩展 `meta:enum` 标准字符串字段的 [友好名称描述符](../api/descriptors.md#friendly-name) ，用于特定模式中的相关字段。

>[!NOTE]
>
>标准软枚举只能在架构级别进行扩展。 换句话说，将 `meta:enum` 一个架构中的标准字段不会影响使用相同标准字段的其他架构。

以下请求会向标准枚举值中添加软枚举值 `eventType` 字段(由 [XDM ExperienceEvent类](../classes/experienceevent.md)) `sourceSchema`:

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

## 扩展自定义软枚举字段

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

本指南介绍了如何扩展架构注册API中的软枚举。 请参阅 [在API中定义自定义字段](./custom-fields-api.md) 以了解有关如何创建不同字段类型的详细信息。
