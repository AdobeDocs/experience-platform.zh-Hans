---
title: 使用架构注册表API将特定字段添加到架构
description: 了解如何使用架构注册表API将预先存在的字段组中的各个字段添加到体验数据模型(XDM)架构。
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# 使用架构注册表API将特定字段添加到架构

Experience Data Model (XDM)架构由一个基类组成，通过使用由Adobe定义的标准字段组和由您的组织定义的自定义字段组，包含其他字段。

在构建架构时，您可能希望使用给定字段组中的某些字段，同时排除同一组中您不需要的其他字段。 本教程向您展示了如何使用架构注册表API将字段组中的各个字段添加到架构中。

>[!NOTE]
>
>有关如何在Adobe Experience Platform UI中添加和移除各个架构字段的信息，请参阅指南，了解有关 [基于字段的工作流](../ui/field-based-workflows.md) （当前为测试版）。

## 先决条件

本教程涉及对 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 在开始之前，请查看 [开发人员指南](../api/getting-started.md) 有关成功调用API所需了解的重要信息，包括 `{TENANT_ID}`、容器的概念以及发出请求所需的标头。

## 了解 `meta:refProperty` 字段

对于任何给定架构，构成其结构的类和字段组在其下引用。 `allOf` 数组。 每个组件表示为一个包含 `$ref` 引用组件URI的属性 `$id`.

以下JSON表示一个使用单个类(`experienceevent`)和字段组(`experienceevent-all`)：

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all"
    }
  ]
}
```

对于中的任何对象 `allOf` 引用字段组的数组，您可以添加同级 `meta:refProperty` 用于指定群组中的哪些字段应包含在架构中的字段。

>[!NOTE]
>
>每个字段都使用JSON指针字符串指定，该字符串表示其相应字段组中的字段路径。 字符串必须以前导斜杠(`/`)且不应包含任何 `properties` 命名空间。 例如：`/_experience/campaign/message/id`。

当作为字符串包含时， `meta:refProperty` 可以引用组中的单个字段。 来自同一组的其他字段可以使用相同的 `$ref` 另一个对象中具有其他值的值 `meta:refProperty` 值。

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/id"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": "/_experience/campaign/message/size"
    }
  ]
}
```

或者， `meta:refProperty` 可作为数组提供，允许您指定在单个字段中从给定组中包括的多个字段 `allOf` 列表项：

```json
{
  "title": "My Sample Schema",
  "description": "An example schema that uses the XDM ExperienceEvent class.",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ]
}
```

## 使用PUT操作添加字段

您可以使用PUT请求重写整个架构，并配置要包含的字段 `allOf`.

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL编码 `$id` 要重写的架构的ID。 |

**请求**

以下请求更新从下的字段组包含的特定字段 `allOf` 数组。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "title": "My Sample Schema",
        "description": "My Sample Description",
        "type": "object",
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
          },
          {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        ]
      }'
```

**响应**

成功响应将返回已更新架构的详细信息。

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>有关架构的PUT请求的更多详细信息，请参阅 [架构端点指南](../api/schemas.md#put).

## 使用PATCH操作添加字段

您可以使用PATCH请求将单个字段添加到架构而不覆盖其他字段。 架构注册表支持所有标准JSON修补程序操作，包括 `add`， `remove`、和 `replace`. 有关JSON修补程序的详细信息，请参见 [API基础知识指南](../../landing/api-fundamentals.md#json-patch).

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL编码 `$id` 要重写的架构的ID。 |

**请求**

以下请求将新对象添加到架构的 `allOf` 数组，指定要添加的字段。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
            "meta:refProperty": [
              "/_experience/campaign/message/id",
              "/_experience/campaign/message/size",
              "/_experience/campaign/message/variant"
            ]
          }
        }
      ]'
```

**响应**

成功响应将返回已更新架构的详细信息。

```json
{
  "title": "My Sample Schema",
  "description": "My Sample Description",
  "type": "object",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/experienceevent"
    },
    {
      "$ref": "https://ns.adobe.com/experience/campaign/experienceevent-all",
      "meta:refProperty": [
        "/_experience/campaign/message/id",
        "/_experience/campaign/message/size",
        "/_experience/campaign/message/variant"
      ]
    }
  ],
  "meta:class": "https://ns.adobe.com/xdm/context/experienceevent",
  "meta:abstract": false,
  "meta:extensible": false,
  "meta:extends": [
      "https://ns.adobe.com/xdm/context/experienceevent",
      "https://ns.adobe.com/xdm/data/time-series"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
  "version": "1.0",
  "meta:resourceType": "schemas",
  "meta:registryMetadata": {
      "repo:createDate": 1552088461236,
      "repo:lastModifiedDate": 1552088470592,
      "xdm:createdClientId": "{CREATED_CLIENT}",
      "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

>[!NOTE]
>
>有关架构的PATCH请求的更多详细信息，请参阅 [架构端点指南](../api/schemas.md#patch).

## 后续步骤

本指南介绍了如何使用API调用将现有字段组中的单个字段添加到架构。 有关如何在Platform UI中执行类似的基于字段的任务的详细信息，请参阅以下指南： [基于字段的工作流](../ui/field-based-workflows.md).

有关架构注册表API功能的更多信息，请参阅 [API概述](../api/overview.md) 以获取完整的端点列表和进程。
