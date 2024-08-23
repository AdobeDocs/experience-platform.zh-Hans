---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；架构注册表；架构注册表；描述符；描述符；描述符；身份；身份；友好名称；友好名称；alternatedisplayinfo；引用；引用；关系；关系
solution: Experience Platform
title: 描述符API端点
description: 架构注册API中的/descriptors端点允许您以编程方式管理体验应用程序中的XDM描述符。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 866e00459c66ea4678cd98d119a7451fd8e78253
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 1%

---

# 描述符端点

架构定义了数据实体的静态视图，但未提供基于这些架构（例如数据集）的数据如何相互关联的特定详细信息。 Adobe Experience Platform允许您使用描述符描述这些关系以及有关架构的其他解释性元数据。

架构描述符是租户级别的元数据，这意味着它们对于您的组织是唯一的，并且所有描述符操作都在租户容器中进行。

每个架构可以应用一个或多个架构描述符实体。 每个架构描述符实体包括描述符`@type`及其适用的`sourceSchema`。 应用后，这些描述符将应用于使用该架构创建的所有数据集。

[!DNL Schema Registry] API中的`/descriptors`端点允许您以编程方式管理体验应用程序中的描述符。

## 快速入门

本指南中使用的终结点是[[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)，以获取相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索描述符列表 {#list}

通过向`/tenant/descriptors`发出GET请求，您可以列出贵组织定义的所有描述符。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

响应格式取决于请求中发送的`Accept`标头。 请注意，`/descriptors`端点使用的`Accept`标头与[!DNL Schema Registry] API中的所有其他端点不同。

>[!IMPORTANT]
>
>描述符需要将`xed`替换为`xdm`的唯一`Accept`标头，并且还提供描述符唯一的`link`选项。 以下示例调用中已包含正确的`Accept`标头，但请格外小心，以确保在使用描述符时使用正确的标头。

| `Accept`标头 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的数组 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路径的数组 |
| `application/vnd.adobe.xdm+json` | 返回扩展描述符对象的数组 |
| `application/vnd.adobe.xdm-v2+json` | 此`Accept`标头必须使用分页功能。 |

{style="table-layout:auto"}

**响应**

响应包括已定义描述符的每个描述符类型的数组。 换言之，如果没有定义特定`@type`的描述符，则注册表将不会为该描述符类型返回空数组。

使用`link` `Accept`标头时，每个描述符都显示为格式为`/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`的数组项

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

## 查找描述符 {#lookup}

如果要查看特定描述符的详细信息，可以使用其`@id`查找(GET)单个描述符。

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要查找的描述符的`@id`。 |

{style="table-layout:auto"}

**请求**

以下请求按其`@id`值检索描述符。 描述符未进行版本控制，因此查找请求中不需要任何`Accept`标头。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回描述符的详细信息，包括其`@type`和`sourceSchema`，以及根据描述符类型而异的其他信息。 返回的`@id`应与请求中提供的描述符`@id`匹配。

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
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 创建描述符 {#create}

您可以通过向`/tenant/descriptors`端点发出POST请求来创建新的描述符。

>[!IMPORTANT]
>
>[!DNL Schema Registry]允许您定义多个不同的描述符类型。 每个描述符类型都需要在请求正文中发送其自身的特定字段。 有关描述符的完整列表以及定义描述符所需的字段，请参阅[附录](#defining-descriptors)。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在示例架构中的“电子邮件地址”字段中定义标识描述符。 这告知[!DNL Experience Platform]使用电子邮件地址作为标识符以帮助拼接有关个人的信息。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应返回HTTP状态201 （已创建）以及新创建的描述符的详细信息，包括其`@id`。 `@id`是由[!DNL Schema Registry]分配的只读字段，用于引用API中的描述符。

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

## 更新描述符 {#put}

您可以通过在PUT请求的路径中包含描述符的`@id`来更新描述符。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要更新的描述符的`@id`。 |

{style="table-layout:auto"}

**请求**

此请求基本上重写描述符，因此请求正文必须包含定义该类型的描述符所需的所有字段。 换句话说，用于更新(PUT)描述符的请求有效负载与用于[创建(POST)相同类型的描述符](#create)的有效负载相同。

>[!IMPORTANT]
>
>与使用POST请求创建描述符一样，每种描述符类型都需要在PUT请求负载中发送其自己的特定字段。 有关描述符的完整列表以及定义描述符所需的字段，请参阅[附录](#defining-descriptors)。

以下示例将标识描述符更新为引用其他`xdm:sourceProperty` (`mobile phone`)，并将`xdm:namespace`更改为`Phone`。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

成功的响应返回HTTP状态201 （已创建）和更新描述符的`@id`（应与请求中发送的`@id`匹配）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

执行[查找(GET)请求](#lookup)以查看描述符时，显示字段现已更新以反映PUT请求中发送的更改。

## 删除描述符 {#delete}

有时您可能需要从[!DNL Schema Registry]中删除已定义的描述符。 这是通过发出引用要删除的描述符的`@id`的DELETE请求来完成的。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 要删除的描述符的`@id`。 |

{style="table-layout:auto"}

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）和一个空白正文。

要确认该描述符已被删除，您可以对该描述符`@id`执行[查找请求](#lookup)。 响应返回HTTP状态404 （未找到），因为描述符已从[!DNL Schema Registry]中删除。

## 附录

以下部分提供了有关在[!DNL Schema Registry] API中使用描述符的其他信息。

### 定义描述符 {#defining-descriptors}

>[!NOTE]
>
>可应用于组织沙盒的描述符的最大数量为4000。

以下部分概述了可用的描述符类型，包括用于定义每种类型的描述符的必填字段。

>[!IMPORTANT]
>
>您不能为租户命名空间对象添加标签，因为系统将通过该沙盒将该标签应用于每个自定义字段。 相反，您必须在该对象下指定需要标记的叶节点。

#### 身份描述符

标识描述符指示“[!UICONTROL sourceSchema]”的“[!UICONTROL sourceProperty]”是[Adobe Experience Platform Identity Service](../../identity-service/home.md)描述的[!DNL Identity]字段。

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
| `@type` | 正在定义的描述符类型。 对于标识描述符，此值必须设置为`xdm:descriptorIdentity`。 |
| `xdm:sourceSchema` | 正在定义描述符的架构的`$id` URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 将成为标识的特定属性的路径。 路径应该以“/”开头，而不是以开头。 不要在路径中包含“properties”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:namespace` | 身份命名空间的`id`或`code`值。 可以使用[[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service)找到命名空间列表。 |
| `xdm:property` | `xdm:id`或`xdm:code`，具体取决于使用的`xdm:namespace`。 |
| `xdm:isPrimary` | 可选的布尔值。 如果为true，则指示字段作为主标识。 架构只能包含一个主标识。 |

{style="table-layout:auto"}

#### 友好名称描述符 {#friendly-name}

友好名称描述符允许用户修改核心库架构字段的`title`、`description`和`meta:enum`值。 在使用“eVar”和您希望标记为包含特定于您的组织的信息的其他“通用”字段时特别有用。 UI可以使用这些显示更友好的名称或仅显示具有友好名称的字段。

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
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在定义的描述符类型。 对于友好名称描述符，此值必须设置为`xdm:alternateDisplayInfo`。 |
| `xdm:sourceSchema` | 正在定义描述符的架构的`$id` URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 要修改其详细信息的特定属性的路径。 路径应以斜杠(`/`)开头，而不是以斜杠结尾。 不要在路径中包含`properties`（例如，使用`/personalEmail/address`而不是`/properties/personalEmail/properties/address`）。 |
| `xdm:title` | 您希望为此字段显示的新标题，以字首大写字母表示。 |
| `xdm:description` | 可以在标题中添加可选描述。 |
| `meta:enum` | 如果`xdm:sourceProperty`指示的字段为字符串字段，则可以使用`meta:enum`在分段UI中为字段添加建议值。 需要注意的是，`meta:enum`不会为XDM字段声明枚举或提供任何数据验证。<br><br>这只能用于Adobe定义的核心XDM字段。 如果源属性是由贵组织定义的自定义字段，则应直接通过对该字段父资源的PATCH请求编辑该字段的`meta:enum`属性。 |
| `meta:excludeMetaEnum` | 如果由`xdm:sourceProperty`指示的字段是一个字符串字段，该字段具有在`meta:enum`字段下提供的现有建议值，则可以在友好名称描述符中包含此对象，以从分段中排除这些值的部分或全部。 每个条目的键和值必须与字段的原始`meta:enum`中包含的键和值匹配，才能排除该条目。 |

{style="table-layout:auto"}

#### 关系描述符

关系描述符描述两个不同架构之间的关系，它们以`sourceProperty`和`destinationProperty`中描述的属性作为密钥。 有关详细信息，请参阅有关[定义两个架构](../tutorials/relationship-api.md)之间关系的教程。

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
| `@type` | 正在定义的描述符类型。 对于关系描述符，此值必须设置为`xdm:descriptorOneToOne`。 |
| `xdm:sourceSchema` | 正在定义描述符的架构的`$id` URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 要定义关系的源架构中字段的路径。 应该以“/”开头，而不是以开头。 不要在路径中包含“properties”（例如，“/personalEmail/address”而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:destinationSchema` | 此描述符正在定义关系的参考架构的`$id` URI。 |
| `xdm:destinationVersion` | 引用架构的主要版本。 |
| `xdm:destinationProperty` | 引用架构中目标字段的可选路径。 如果忽略此属性，则包含匹配引用标识描述符的任何字段都会推断目标字段（请参阅下文）。 |

{style="table-layout:auto"}

#### 引用身份描述符

引用身份描述符为架构字段的主要身份提供引用上下文，允许其他架构中的字段引用该上下文。 引用架构必须先定义主标识字段，其他架构才能通过此描述符引用该字段。

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
| `@type` | 正在定义的描述符类型。 对于引用标识描述符，此值必须设置为`xdm:descriptorReferenceIdentity`。 |
| `xdm:sourceSchema` | 正在定义描述符的架构的`$id` URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 源架构中用于引用引用架构的字段的路径。 应该以“/”开头，而不是以开头。 不要在路径中包含“properties”（例如，`/personalEmail/address`而不是`/properties/personalEmail/properties/address`）。 |
| `xdm:identityNamespace` | 源属性的身份命名空间代码。 |

{style="table-layout:auto"}

#### 已弃用的字段描述符

您可以[弃用自定义XDM资源](../tutorials/field-deprecation-api.md#custom)中的字段，方法是向相关字段添加设置为`deprecated`的`meta:status`属性。 但是，如果要弃用由架构中的标准XDM资源提供的字段，可向相关架构分配已弃用的字段描述符，以实现相同的效果。 通过使用[正确的`Accept`标头](../tutorials/field-deprecation-api.md#verify-deprecation)，您可以在API中查找架构时查看该架构已弃用的标准字段。

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 描述符的类型。 对于字段弃用描述符，此值必须设置为`xdm:descriptorDeprecated`。 |
| `xdm:sourceSchema` | 要应用描述符的架构的URI `$id`。 |
| `xdm:sourceVersion` | 要将描述符应用于的架构的版本。 应设置为`1`。 |
| `xdm:sourceProperty` | 架构中要将描述符应用于的属性的路径。 如果要将描述符应用于多个属性，则可以提供数组形式的路径列表（例如，`["/firstName", "/lastName"]`）。 |

{style="table-layout:auto"}
