---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；架构注册表；架构注册表；描述符；描述符；描述符；身份；身份；友好名称；友好名称；alternatedisplayinfo；引用；引用；关系；关系
solution: Experience Platform
title: 描述符API端点
description: 架构注册API中的/descriptors端点允许您以编程方式管理体验应用程序中的XDM描述符。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 786801975dbde52b5d81a407618ef3b574a6afa3
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 1%

---

# 描述符端点

架构定义了数据实体的静态视图，但未提供基于这些架构（例如数据集）的数据如何相互关联的特定详细信息。 Adobe Experience Platform允许您使用描述符描述这些关系以及有关架构的其他解释性元数据。

架构描述符是租户级别的元数据，这意味着它们对于您的组织是唯一的，并且所有描述符操作都在租户容器中进行。

每个架构可以应用一个或多个架构描述符实体。 每个架构描述符实体包括一个描述符 `@type` 和 `sourceSchema` 适用于此项。 应用后，这些描述符将应用于使用该架构创建的所有数据集。

此 `/descriptors` 中的端点 [!DNL Schema Registry] API允许您以编程方式管理体验应用程序中的描述符。

## 快速入门

本指南中使用的端点是 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关相关文档的链接、阅读本文档中示例API调用的指南，以及有关成功调用任何Experience PlatformAPI所需的所需标头的重要信息。

## 检索描述符列表 {#list}

您可以通过向以下网站发出GET请求，列出贵组织定义的所有描述符： `/tenant/descriptors`.

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

响应格式取决于 `Accept` 标头在请求中发送。 请注意 `/descriptors` 端点使用 `Accept` 与中的所有其他端点不同的标头 [!DNL Schema Registry] API。

>[!IMPORTANT]
>
>描述符需要唯一 `Accept` 替换的标头 `xed` 替换为 `xdm`，并且还提供 `link` 描述符特有的选项。 适当的 `Accept` 标头已包含在下面的示例调用中，但请特别注意，以确保在使用描述符时使用正确的标头。

| `Accept` 标题 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 返回描述符ID的数组 |
| `application/vnd.adobe.xdm-link+json` | 返回描述符API路径的数组 |
| `application/vnd.adobe.xdm+json` | 返回扩展描述符对象的数组 |
| `application/vnd.adobe.xdm-v2+json` | 此 `Accept` 标头必须使用分页功能。 |

{style="table-layout:auto"}

**响应**

响应包括已定义描述符的每个描述符类型的数组。 换言之，如果没有某个 `@type` 定义，注册表将不会返回该描述符类型的空数组。

使用时 `link` `Accept` 标头，每个描述符以格式显示为数组项 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

如果要查看特定描述符的详细信息，可以使用其查找(GET)单个描述符 `@id`.

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 要查找的描述符对应的字段。 |

{style="table-layout:auto"}

**请求**

以下请求通过其检索描述符 `@id` 值。 描述符未进行版本控制，因此不 `Accept` 查找请求中需要标头。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回描述符的详细信息，包括其 `@type` 和 `sourceSchema`以及根据描述符类型而不同的其他信息。 返回的 `@id` 应该匹配描述符 `@id` 在请求中提供。

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

您可以通过向以下对象发出POST请求来创建新的描述符： `/tenant/descriptors` 端点。

>[!IMPORTANT]
>
>此 [!DNL Schema Registry] 允许您定义几种不同的描述符类型。 每个描述符类型都需要在请求正文中发送其自身的特定字段。 请参阅 [附录](#defining-descriptors) 以获取描述符的完整列表以及定义这些描述符所需的字段。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下请求在示例架构中的“电子邮件地址”字段中定义标识描述符。 这说明 [!DNL Experience Platform] 将电子邮件地址用作标识符以帮助拼接有关个人的信息。

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

成功的响应返回HTTP状态201 （已创建）以及新创建的描述符的详细信息，包括其 `@id`. 此 `@id` 是由分配的只读字段 [!DNL Schema Registry] 和用于引用API中的描述符。

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

您可以通过包含其描述符来更新描述符 `@id` 在PUT请求的路径中。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 要更新的描述符的。 |

{style="table-layout:auto"}

**请求**

此请求基本上重写描述符，因此请求正文必须包含定义该类型的描述符所需的所有字段。 换句话说，用于更新(PUT)描述符的请求有效负载与要更新的有效负载相同 [创建(POST)描述符](#create) 相同类型的。

>[!IMPORTANT]
>
>与使用POST请求创建描述符一样，每种描述符类型都需要在PUT请求负载中发送其自己的特定字段。 请参阅 [附录](#defining-descriptors) 以获取描述符的完整列表以及定义这些描述符所需的字段。

以下示例将标识描述符更新为引用其他 `xdm:sourceProperty` (`mobile phone`)并更改 `xdm:namespace` 到 `Phone`.

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

成功的响应返回HTTP状态201（已创建），并且 `@id` 的匹配项(该匹配项 `@id` （已在请求中发送）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

执行 [查找(GET)请求](#lookup) 要查看描述符，则表明字段现已更新，以反映在PUT请求中发送的更改。

## 删除描述符 {#delete}

有时，您可能需要从删除已定义的描述符 [!DNL Schema Registry]. DELETE这是通过发出引用 `@id` 要移除的描述符的。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 要删除的描述符的ID。 |

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

要确认描述符已被删除，您可以执行 [查找请求](#lookup) 针对描述符 `@id`. 响应返回HTTP状态404 （未找到），因为描述符已从 [!DNL Schema Registry].

## 附录

以下部分提供了有关在中使用描述符的其他信息 [!DNL Schema Registry] API。

### 定义描述符 {#defining-descriptors}

以下部分概述了可用的描述符类型，包括用于定义每种类型的描述符的必填字段。

>[!IMPORTANT]
>
>您不能为租户命名空间对象添加标签，因为系统将通过该沙盒将该标签应用于每个自定义字段。 相反，您必须在该对象下指定需要标记的叶节点。

#### 身份描述符

身份描述符表示“[!UICONTROL sourceproperty]的“[!UICONTROL sourceschema]”是一个 [!DNL Identity] 字段，如所述 [Adobe Experience Platform Identity服务](../../identity-service/home.md).

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
| `@type` | 正在定义的描述符类型。 对于标识描述符，该值必须设置为 `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 正在定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 将成为标识的特定属性的路径。 路径应该以“/”开头，而不是以开头。 不要在路径中包含“properties”（例如，使用“/personalEmail/address”而不是“/properties/personalEmail/properties/address”） |
| `xdm:namespace` | 此 `id` 或 `code` 身份命名空间的值。 命名空间列表可以使用 [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | 或者 `xdm:id` 或 `xdm:code`，具体取决于 `xdm:namespace` 已使用。 |
| `xdm:isPrimary` | 可选的布尔值。 如果为true，则指示字段作为主标识。 架构只能包含一个主标识。 |

{style="table-layout:auto"}

#### 友好名称描述符 {#friendly-name}

友好名称描述符允许用户修改 `title`， `description`、和 `meta:enum` 核心库架构字段的值。 在使用“eVar”和您希望标记为包含特定于您的组织的信息的其他“通用”字段时特别有用。 UI可以使用这些显示更友好的名称或仅显示具有友好名称的字段。

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
| `@type` | 正在定义的描述符类型。 对于友好名称描述符，必须将此值设置为 `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | 此 `$id` 正在定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 要修改其详细信息的特定属性的路径。 路径应以斜杠(`/`)，并且不是以一个结尾。 不包括 `properties` 在路径中(例如，使用 `/personalEmail/address` 而不是 `/properties/personalEmail/properties/address`)。 |
| `xdm:title` | 您希望为此字段显示的新标题，以字首大写字母表示。 |
| `xdm:description` | 可以在标题中添加可选描述。 |
| `meta:enum` | 如果字段由 `xdm:sourceProperty` 是字符串字段， `meta:enum` 可用于在分段UI中为字段添加建议值。 请务必注意 `meta:enum` 不会为XDM字段声明枚举或提供任何数据验证。<br><br>这应当仅用于Adobe定义的核心XDM字段。 如果源属性是由您的组织定义的自定义字段，则应编辑该字段的 `meta:enum` 属性直接通过PATCH请求发送到字段的父资源。 |
| `meta:excludeMetaEnum` | 如果字段由 `xdm:sourceProperty` 是一个字符串字段，其下提供了现有的建议值 `meta:enum` 字段中，您可以将此对象包含在友好名称描述符中，以从分段中排除其中的部分或全部值。 每个条目的键和值必须与原始条目中包含的键和值匹配 `meta:enum` 字段，以便排除条目。 |

{style="table-layout:auto"}

#### 关系描述符

关系描述符描述两个不同架构之间的关系，它们基于中所述的属性 `sourceProperty` 和 `destinationProperty`. 请参阅上的教程 [定义两个架构之间的关系](../tutorials/relationship-api.md) 以了解更多信息。

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
| `@type` | 正在定义的描述符类型。 对于关系描述符，该值必须设置为 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 此 `$id` 正在定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 要定义关系的源架构中字段的路径。 应该以“/”开头，而不是以开头。 不要在路径中包含“properties”（例如，“/personalEmail/address”而不是“/properties/personalEmail/properties/address”）。 |
| `xdm:destinationSchema` | 此 `$id` 此描述符正在定义与其关系的参考架构的URI。 |
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
| `@type` | 正在定义的描述符类型。 对于引用身份描述符，必须将此值设置为 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 正在定义描述符的架构的URI。 |
| `xdm:sourceVersion` | 源架构的主要版本。 |
| `xdm:sourceProperty` | 源架构中用于引用引用架构的字段的路径。 应该以“/”开头，而不是以开头。 不要在路径中包含“properties”(例如， `/personalEmail/address` 而不是 `/properties/personalEmail/properties/address`)。 |
| `xdm:identityNamespace` | 源属性的身份命名空间代码。 |

{style="table-layout:auto"}

#### 已弃用的字段描述符

您可以 [弃用自定义XDM资源中的字段](../tutorials/field-deprecation-api.md#custom) 通过添加 `meta:status` 属性设置为 `deprecated` 到有问题的领域。 但是，如果要弃用由架构中的标准XDM资源提供的字段，可向相关架构分配已弃用的字段描述符，以实现相同的效果。 使用 [正确 `Accept` 标题](../tutorials/field-deprecation-api.md#verify-deprecation)后，您可以在API中查找架构时，查看该架构已弃用的标准字段。

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
| `@type` | 描述符的类型。 对于字段弃用描述符，必须将此值设置为 `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` 描述符应用于的架构的ID。 |
| `xdm:sourceVersion` | 要将描述符应用于的架构的版本。 应设置为 `1`. |
| `xdm:sourceProperty` | 架构中要将描述符应用于的属性的路径。 如果要将描述符应用于多个属性，则可以提供数组形式的路径列表(例如， `["/firstName", "/lastName"]`)。 |

{style="table-layout:auto"}
