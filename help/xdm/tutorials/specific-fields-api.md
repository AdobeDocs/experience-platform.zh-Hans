---
title: 使用架构注册表API向架构添加特定字段
description: 了解如何使用架构注册表API，将预先存在的字段组中的各个字段添加到体验数据模型(XDM)架构。
source-git-commit: 4bcd949e901c11bb933000f7ae76f17134dda496
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 2%

---

# 使用架构注册API向架构添加特定字段

体验数据模型(XDM)架构由基类组成，其中通过使用由Adobe定义的标准字段组和由您的组织定义的自定义字段组来包含其他字段。

在构建架构时，您可能希望使用给定字段组中的某些字段，同时将不需要的其他字段排除在同一个组中。 本教程将向您展示如何使用架构注册表API将字段组中的各个字段添加到架构中。

>[!NOTE]
>
>有关如何在Adobe Experience Platform UI中添加和删除单个架构字段的信息，请参阅 [基于字段的工作流](../ui/field-based-workflows.md) （目前为测试版）。

## 先决条件

本教程包括调用 [架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 开始之前，请查看 [开发人员指南](../api/getting-started.md) 以了解成功调用API(包括您的 `{TENANT_ID}`、容器的概念以及发出请求所需的标头。

## 了解 `meta:refProperty` 字段

对于任何给定的架构，在其下引用构成其结构的类和字段组 `allOf` 数组。 每个组件都表示为包含 `$ref` 引用组件URI的属性 `$id`.

以下JSON表示使用单个类(`experienceevent`)和字段组(`experienceevent-all`):

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

对于 `allOf` 引用字段组的数组，可以添加同级 `meta:refProperty` 字段，以指定架构中应包含组中的哪些字段。

>[!NOTE]
>
>每个字段都使用JSON指针字符串指定，表示相应字段组内字段的路径。 字符串必须以前导斜杠(`/`)和不应包含任何 `properties` 命名空间。 例如：`/_experience/campaign/message/id`。

作为字符串包含时， `meta:refProperty` 可以引用组中的单个字段。 使用同一组可以包含来自同一组的其他字段 `$ref` 值 `meta:refProperty` 值。

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

或者， `meta:refProperty` 可以作为数组提供，允许您指定多个字段以包含在单个内的给定组中 `allOf` 列表项：

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

您可以使用PUT请求重写整个架构，并配置要在下包含的字段 `allOf`.

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 要重写的架构。 |

**请求**

以下请求会更新 `allOf` 数组。

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

成功的响应会返回更新架构的详细信息。

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
>有关架构PUT请求的更多详细信息，请参阅 [schema endpoint指南](../api/schemas.md#put).

## 使用PATCH操作添加字段

您可以使用PATCH请求将单个字段添加到架构，而不会覆盖其他字段。 架构注册表支持所有标准JSON修补程序操作，包括 `add`, `remove`和 `replace`. 有关JSON修补程序的更多信息，请参阅 [API基础知识指南](../../landing/api-fundamentals.md#json-patch).

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 的 `meta:altId` 或URL编码 `$id` 要重写的架构。 |

**请求**

以下请求会向架构的 `allOf` 数组，指定要添加的字段。

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

成功的响应会返回更新架构的详细信息。

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
>有关架构PATCH请求的更多详细信息，请参阅 [schema endpoint指南](../api/schemas.md#patch).

## 后续步骤

本指南介绍了如何使用API调用将现有字段组中的各个字段添加到架构。 有关如何在平台UI中执行类似基于字段的任务的详细信息，请参阅 [基于字段的工作流](../ui/field-based-workflows.md).

有关模式注册表API功能的更多信息，请参阅 [API概述](../api/overview.md) 获取端点和进程的完整列表。
