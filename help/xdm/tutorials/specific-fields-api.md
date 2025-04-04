---
title: 使用架构注册表API将特定字段添加到架构
description: 了解如何使用架构注册表API将预先存在的字段组中的各个字段添加到体验数据模型(XDM)架构。
exl-id: 696cce2b-bbde-416a-9f52-12ab4da9c2c6
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# 使用架构注册表API将特定字段添加到架构

体验数据模型(XDM)架构由一个基类组成，通过使用由Adobe定义的标准字段组和由您的组织定义的自定义字段组，包含其他字段。

构建架构时，您可能要使用给定字段组中的某些字段，而排除同一组中您不需要的其他字段。 本教程将演示如何使用架构注册表API将字段组中的各个字段添加到架构中。

>[!NOTE]
>
>有关如何在Adobe Experience Platform UI中添加和删除各个架构字段的信息，请参阅有关[基于字段的工作流](../ui/field-based-workflows.md)的指南（当前为测试版）。

## 先决条件

本教程涉及调用[架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)。 开始之前，请查看[开发人员指南](../api/getting-started.md)以了解成功调用API所需了解的重要信息，包括您的`{TENANT_ID}`、容器的概念以及发出请求所需的标头。

## 了解`meta:refProperty`字段

对于任何给定架构，构成其结构的类和字段组在其`allOf`数组下引用。 每个组件都表示为一个对象，其中包含引用组件的URI `$id`的`$ref`属性。

以下JSON表示使用单个类(`experienceevent`)和字段组(`experienceevent-all`)的简化架构：

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

对于`allOf`数组中引用字段组的任何对象，可以添加同级`meta:refProperty`字段以指定组中应包含哪些字段到架构中。

>[!NOTE]
>
>每个字段都使用JSON指针字符串指定，该字符串表示其相应字段组中的字段路径。 字符串必须以前导斜杠(`/`)开头，并且不应包含任何`properties`命名空间。 例如： `/_experience/campaign/message/id`。

当作为字符串包含时，`meta:refProperty`可以引用组中的单个字段。 通过在具有不同`meta:refProperty`值的另一个对象中使用相同的`$ref`值，可以包含来自同一组的其他字段。

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

或者，也可以将`meta:refProperty`作为数组提供，从而允许您在单个`allOf`列表项中指定要包含来自给定组的多个字段：

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

您可以使用PUT请求重写整个架构，并配置要包含在`allOf`下的字段。

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要重写的架构的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求更新`allOf`数组下字段组中包含的特定字段。

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

成功的响应将返回已更新架构的详细信息。

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
>有关架构的PUT请求的更多详细信息，请参阅[架构端点指南](../api/schemas.md#put)。

## 使用PATCH操作添加字段

您可以使用PATCH请求将单个字段添加到架构而不覆盖其他字段。 架构注册表支持所有标准JSON修补程序操作，包括`add`、`remove`和`replace`。 有关JSON修补程序的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-patch)。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 要重写的架构的`meta:altId`或URL编码的`$id`。 |

**请求**

以下请求将新对象添加到架构的`allOf`数组，指定要添加的字段。

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

成功的响应将返回已更新架构的详细信息。

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
>有关架构的PATCH请求的更多详细信息，请参阅[架构端点指南](../api/schemas.md#patch)。

## 后续步骤

本指南介绍了如何使用API调用将现有字段组中的单个字段添加到架构。 有关如何在Experience Platform UI中执行类似的基于字段的任务的详细信息，请参阅[基于字段的工作流](../ui/field-based-workflows.md)指南。

有关架构注册表API功能的详细信息，请参阅[API概述](../api/overview.md)，以获取完整的端点和进程列表。
