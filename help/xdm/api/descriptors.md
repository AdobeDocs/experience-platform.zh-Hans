---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;descriptor;Descriptor;descriptors;Descriptors;identity;Identity;friendly name;Friendly name;alternatedisplayinfo;reference;Reference;relationship;Relationship
solution: Experience Platform
title: 描述符
description: 模式注册表API中的/descriptors端点允许您以编程方式管理体验应用程序中的XDM描述符。
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 1%

---


# 描述符端点

模式定义数据实体的静态视图，但不提供关于基于这些模式（例如数据集）的数据如何彼此关联的特定详细信息。 Adobe Experience Platform允许您使用描述符描述模式的这些关系和其他解释性元数据。

模式描述符是租户级元数据，这意味着它们是IMS组织特有的，所有描述符操作都在租户容器中进行。

每个模式可以有一个或多个模式描述符实体应用到它。 每个模式描述符实体都包含一个描述符`@type`和它所应用的`sourceSchema`。 应用这些描述符后，这些描述符将应用于使用该模式创建的所有数据集。

[!DNL Schema Registry] API中的`/descriptors`端点允许您以编程方式管理体验应用程序中的描述符。

## 入门指南

本指南中使用的端点是[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)的一部分。 在继续之前，请查看[入门指南](./getting-started.md)，了解相关文档的链接、阅读此文档中示例API调用的指南，以及成功调用任何Experience PlatformAPI所需的重要头信息。

## 检索描述符{#list}的列表

您可以通过向`/tenant/descriptors`发出列表请求来GET您的组织定义的所有描述符。

**API格式**

```http
GET /tenant/descriptors
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

响应格式取决于请求中发送的`Accept`头。 请注意，`/descriptors`端点使用的`Accept`头与[!DNL Schema Registry] API中的所有其他端点不同。

>[!IMPORTANT]
>
>描述符需要唯一的`Accept`标头，用`xdm`替换`xed`，还要优惠描述符特有的`link`选项。 以下示例调用中已包含正确的`Accept`标头，但要确保在使用描述符时使用正确的标头，请格外小心。

| `Accept` 标题 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的数组 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路径的数组 |
| `application/vnd.adobe.xdm+json` | 返回扩展描述符对象的数组 |
| `application/vnd.adobe.xdm-v2+json` | 必须使用此`Accept`头才能使用分页功能。 |

**响应**

该响应包括每个具有定义描述符的描述符类型的数组。 换言之，如果未定义某个`@type`的描述符，则注册表将不会为该描述符类型返回空数组。

使用`link` `Accept`头时，每个描述符都显示为格式为`/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`的数组项

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## 查找描述符{#lookup}

如果要视图特定描述符的详细信息，可以使用其`@id`查找(GET)单个描述符。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要查找的描述符的`@id`。 |

**请求**

以下请求按其`@id`值检索描述符。 描述符未版本化，因此在查找请求中不需要`Accept`头。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回描述符的详细信息，包括`@type`和`sourceSchema`，以及根据描述符的类型而有所不同的其他信息。 返回的`@id`应与请求中提供的描述符`@id`匹配。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 创建描述符{#create}

可以通过向`/tenant/descriptors`端点发出POST请求来创建新描述符。

>[!IMPORTANT]
>
>[!DNL Schema Registry]允许您定义几种不同的描述符类型。 每个描述符类型都需要在请求主体中发送其自己的特定字段。 请参见[附录](#defining-descriptors)，以获得描述符的完整列表以及定义它们所需的字段。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在示例模式的“电子邮件地址”字段上定义标识描述符。 这会告知[!DNL Experience Platform]使用电子邮件地址作为标识符来帮助拼合有关个人的信息。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**响应**

成功的响应返回HTTP状态201（已创建）和新创建描述符的详细信息，包括其`@id`。 `@id`是由[!DNL Schema Registry]分配的只读字段，用于在API中引用描述符。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 更新描述符{#put}

可以通过在PUT请求的路径中包含描述符`@id`来更新描述符。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要更新的描述符的`@id`。 |

**请求**

此请求实质上重写描述符，因此请求主体必须包括定义该类型的描述符所需的所有字段。 换言之，要更新(PUT)描述符的请求有效负荷与创建(POST)相同类型的描述符](#create)的有效负荷相同。[

>[!IMPORTANT]
>
>与使用POST请求创建描述符一样，每个描述符类型都要求在PUT请求负载中发送其自己的特定字段。 请参见[附录](#defining-descriptors)，以获得描述符的完整列表以及定义它们所需的字段。

以下示例更新标识描述符以引用不同的`xdm:sourceProperty`(`mobile phone`)并将`xdm:namespace`更改为`Phone`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**响应**

成功的响应返回HTTP状态201（已创建）和更新描述符的`@id`（应与请求中发送的`@id`匹配）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

执行[查找(GET)请求](#lookup)视图描述符将显示字段现已更新以反映在PUT请求中发送的更改。

## 删除描述符{#delete}

有时您可能需要从[!DNL Schema Registry]中删除已定义的描述符。 这是通过引用要删除的描述符的`@id`进行DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要删除的描述符的`@id`。 |

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和空白正文。

要确认描述符已被删除，可以对描述符`@id`执行[查找请求](#lookup)。 该响应返回HTTP状态404（未找到），因为描述符已从[!DNL Schema Registry]中删除。

## 附录

下节提供有关在[!DNL Schema Registry] API中使用描述符的其他信息。

### 定义描述符{#defining-descriptors}

以下各节概述了可用的描述符类型，包括定义每种类型的描述符所需的字段。

#### 标识描述符

标识描述符表示“[!UICONTROL sourceSchema]”的“[!UICONTROL sourceProperty]”是[!DNL Identity]字段，如[Adobe Experience Platform标识服务](../../identity-service/home.md)所述。

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定义描述符的模式的`$id` URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 将作为标识的特定属性的路径。 路径应以“/”开头，而不以“/”结尾。 不要在路径中包含“属性”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:namespace` | 标识命名空间的`id`或`code`值。 使用[[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)可以找到列表。 |
| `xdm:property` | 根据使用的`xdm:namespace`，可选择`xdm:id`或`xdm:code`。 |
| `xdm:isPrimary` | 可选布尔值。 如果为true，则将字段指示为主标识。 模式只能包含一个主标识。 |

#### 友好名称描述符

友好的名称描述符允许用户修改核心库模式字段的`title`、`description`和`meta:enum`值。 在处理“eVar”和您希望标记为包含特定于您组织的信息的其他“通用”字段时特别有用。 UI可以使用这些字段显示更友好的名称或仅显示具有友好名称的字段。

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定义描述符的模式的`$id` URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 将作为标识的特定属性的路径。 路径应以“/”开头，而不以“/”结尾。 不要在路径中包含“属性”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:title` | 要为此字段显示的新标题，用标题大小写写写。 |
| `xdm:description` | 可以随标题一起添加可选描述。 |
| `meta:enum` | 如果由`xdm:sourceProperty`指示的字段是字符串字段，则`meta:enum`将在[!DNL Experience Platform] UI中确定该字段的建议值的列表。 请务必注意，`meta:enum`不声明明细列表或为XDM字段提供任何数据验证。<br><br>这应仅用于由Adobe定义的核心XDM字段。如果源属性是您的组织定义的自定义字段，则应直接通过对字段的父资源的PATCH请求编辑该字段的`meta:enum`属性。 |

#### 关系描述符

关系描述符描述了两种不同模式之间的关系，这些描述符根据`sourceProperty`和`destinationProperty`中描述的属性进行键控。 有关详细信息，请参阅[中定义两个模式之间的关系的教程](../tutorials/relationship-api.md)。

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定义描述符的模式的`$id` URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 源模式中定义关系的字段的路径。 应以“/”开头，而不以“/”结尾。 路径中不要包含“properties”（例如，“/personalEmail/address”，而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:destinationSchema` | 此描述符正在定义关系的目标模式的`$id` URI。 |
| `xdm:destinationVersion` | 目标模式的主版本。 |
| `xdm:destinationProperty` | 目标目标中模式字段的可选路径。 如果忽略此属性，则目标字段由包含匹配引用标识描述符的任何字段推断出来（请参阅下文）。 |


#### 引用标识描述符

引用标识描述符提供对模式字段主标识的引用上下文，允许其被其他模式中的字段引用。 字段必须已用标识描述符进行标记，然后才能将引用描述符应用于这些字段。

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 要定义的描述符的类型。 |
| `xdm:sourceSchema` | 定义描述符的模式的`$id` URI。 |
| `xdm:sourceVersion` | 源模式的主版本。 |
| `xdm:sourceProperty` | 源模式中定义描述符的字段的路径。 应以“/”开头，而不以“/”结尾。 路径中不要包含“properties”（例如，“/personalEmail/address”，而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:identityNamespace` | 源属性的标识命名空间代码。 |