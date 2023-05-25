---
title: 在API中弃用XDM字段
description: 了解如何弃用架构注册表API中的Experience Data Model (XDM)字段。
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 2%

---

# 在API中弃用XDM字段

在Experience Data Model (XDM)中，您可以使用来弃用架构或自定义资源中的字段 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 弃用字段会导致在下游UI中隐藏该字段，例如 [!UICONTROL 配置文件] 工作区和Customer Journey Analytics，但在其他情况下，它是一项无中断的更改，不会对现有数据流产生负面影响。

本文档介绍了如何为不同的XDM资源弃用字段。 有关在Experience Platform用户界面中使用架构编辑器来弃用XDM字段的步骤，请参阅以下教程： [在UI中弃用XDM字段](./field-deprecation-ui.md).

## 快速入门

本教程需要调用架构注册表API。 请查看 [开发人员指南](../api/getting-started.md) 有关发出这些API调用所需了解的重要信息。 这包括您的 `{TENANT_ID}`、“容器”的概念以及发出请求所需的标头(请特别注意 `Accept` 标头及其可能值)。

## 弃用自定义字段 {#custom}

要弃用自定义类、字段组或数据类型中的字段，请通过PUT或PATCH请求更新自定义资源并添加属性 `meta:status: deprecated` 到有问题的领域。

>[!NOTE]
>
>有关更新XDM中自定义资源的一般信息，请参阅以下文档：
>
>* [更新类](../api/classes.md#patch)
>* [更新字段组](../api/field-groups.md#patch)
>* [更新数据类型](../api/data-types.md#patch)


下面的示例API调用弃用了自定义数据类型中的字段。

**API格式**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**请求**

以下请求弃用 `expansionArea` 用于描述房地产属性的数据类型的字段。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**响应**

成功响应将返回自定义资源的更新详细信息，已弃用的字段包含 `meta:status` 值 `deprecated`. 下面的示例响应因空间而被截断。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 弃用架构中的标准字段 {#standard}

不能直接弃用标准类、字段组和数据类型中的字段。 相反，您可以在使用这些标准资源的各个架构中，通过使用描述符来弃用它们。

### 创建字段弃用描述符 {#create-descriptor}

POST要为要弃用的架构字段创建描述符，请向 `/tenant/descriptors` 端点。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 描述符的类型。 对于字段弃用描述符，该值必须设置为 `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` 将描述符应用于的架构的ID。 |
| `xdm:sourceVersion` | 将描述符应用于的架构的版本。 应设置为 `1`. |
| `xdm:sourceProperty` | 将描述符应用于的架构中属性的路径。 如果要将描述符应用于多个属性，则可以提供数组形式的路径列表(例如， `["/firstName", "/lastName"]`)。 |

**响应**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### 验证已弃用的字段 {#verify-deprecation}

应用描述符后，您可以通过在使用适当时查找相关架构来验证字段是否已被弃用 `Accept` 标头。

>[!NOTE]
>
>当前不支持在列出架构时显示已弃用的字段。

**API格式**

```http
GET /tenant/schemas
```

**请求**

要在API响应中包含有关已弃用字段的信息，您必须设置 `Accept` 标头到 `application/vnd.adobe.xed-deprecatefield+json; version=1`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**响应**

成功响应将返回架构的详细信息，已弃用的字段包含 `meta:status` 值 `deprecated`. 下面的示例响应因空间而被截断。

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## 后续步骤

本文档介绍了如何使用架构注册表API弃用XDM字段。 有关为自定义资源配置字段的更多信息，请参阅 [在API中定义XDM字段](./custom-fields-api.md). 有关管理描述符的更多信息，请参见 [描述符端点指南](../api/descriptors.md).
